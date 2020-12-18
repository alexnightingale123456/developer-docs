+++
prev = "/advanced/json-file/"
title = "Module Class Autoloading"
weight = 70

+++

Module class autoloading enables the automatic loading of classes when stored in a prescribed way within WHMCS modules.

It is provided as a tool that makes it easier for module developers to create helper classes that they can call on and load throughout the WHMCS product from modules, hooks and other custom integration code.

## Supported Module Types

The following module types support autoloading. 

* **Addon**
* **Fraud**
* **Gateway**
* **Registrar**
* **Report** 
* **Server** 
* **Widget** 

## Usage

Locate your class file(s) in a sub-directory named 'lib' relative to the deployed module. For example: 

```
/path/to/whmcs/modules/{ModuleType}/{ModuleName}/lib/{ClassName}.php
```
Add the module namespace to the top of your class file(s): 

```
namespace WHMCS\Module\{ModuleType}\{ModuleName};
```
To invoke the class, simply add the use statement and invoke as normal: 

```
use WHMCS\Module\{ModuleType}\{ModuleName}\{ClassName};

$hello = new {ClassName}();
```

For module types that do not have a directory per module by default (for example gateways and reports), you will need to create the directory and sub-directory 'lib' to utilise autoloading.

## Example Usage

The following example demonstrates use of the module namespace autoloading for a class named 'HelloWorld' within the addon module 'Sample Addon Module': 

Filename: /modules/addons/sample_addon_module/lib/HelloWorld.php

```
namespace WHMCS\Module\Addon\SampleAddonModule;

/**
 * Hello World Class
 * 
 * @copyright Copyright (c) 
 * @license http://www.whmcs.com/license/ WHMCS Eula
 */
class HelloWorld {

    /**
     * Print hello world.
     */
    public function printHello()
    {
        print 'Hello World';
    }

}
```
Filename: /modules/addons/sample_addon_module/sample_addon_module.php 

```
use WHMCS\Module\Addon\SampleAddonModule\HelloWorld;

// Other code goes here...

function sample_addon_module_output() {
    $hello = new HelloWorld();
    $hello->printHello();
}
```
