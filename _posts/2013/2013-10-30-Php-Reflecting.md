---
layout: post
title: PHP反射API
category: PHP
---

以前没有看PHP手册，在编程的时候遇到了一个问题：如何用字符串变量动态访问对象的属性或者方法。因为对象的概念大多数来自于Java，所以我猜想PHP应该有类似于get的方法，这样才能使用变量来访问吧。但其实这个问题很简单，使用 $obj->$attr 就行了，可见PHP真的是特别灵活。PHP中也提供了动态调用的系列方法

* get_class 返回类名
* instanceof 
* get_class_methods。可以用 in_array($method, get_class_methods($obj)) 来监测对象是否有$method方法
* is_callable/method_exists。区别在于方法存在，如果是private也不能调用
* get_class_vars
* get_parent_class/is_subclass_of
* call_user_func/call_user_func_array

除了上述方法外，PHP也完全支持类似于Java的反射机制。反射API中的部分类： Reflection, ReflectionClass, ReflectionMethod, ReflectionParameter, ReflectionFunction ……反射在模板的使用中肯定是挺多的。一个例子如下

    /*
    创建一个类类动态加载Module对象。所有Module的子类必须实现execute方法。可以允许用户在XML配置文件中列出所有的Module类，系统使用配置加载这些类然后执行execute
    子类可以提供setter方法并在配置中配置属性
    */
    class Person {
        public $name;
        function __construct($name){
            $this->name = $name;
        }
    }

    interface Module{
        function execute();
    }

    class FtpModule implements Module{
        function setHost($host){
            print "FtpModule::setHost（）：$host\n";
        }

        function setUser($user){
        }
        
        function execute(){
            //....
        }
    }

    class PersonModule implements Module{
        function setPerson(Person $person){
            //...
        }
        function execute(){
            //...
        }
    }

    class ModuleRunner{
        private $config = array(
            "PersonModule" => array("person" => "bob"),
            "FtpModule" => array("host" => "127.0.0.1", "user" => "admin")
        );
        private $modules = array();

        function init(){
            $inteface = new ReflectionClass('Module');
            foreach($config as $moduleName => $params){
                $moduleClass = new ReflectionClass($moduleName);
                if(!$moduleClass->isSubclassOf($interface)){
                    throw new Exception("Unknown module type: $moduleName");
                }
                $module = $moduleClass->newInstance();
                foreach($moduleClass->getMethods() as $method){
                    $this->handleMethod($module, $method, $params);
                }
                array_push($modules, $module);
            }
        }

        function handleMethod(Module $module, ReflactionMethod $method, $params){
            $name = $method->getName();
            $args = $method->getParameters();
            if(count($args) != 1 || substr($name, 0, 3) != 'set'){
                return false;
            }

            $property = strtolower(substr($name, 3));
            if(!isset($params[$property])){
                return false;
            }

            $argClass = $args[0]->getClass();
            if(empty($argClass)){
                $method->invoke($module, $params[$property]);
            }
            else{
                $method->invoke($module, $argClass->newInstance($params[$property]));
            }
        }
    }
