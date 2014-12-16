# Demo Extension

Access extension at this url: <magento-base-url>/hello_extension/index/sayhello
## Components

### composer.json

#### Root

To autoload classes in the module, the root composer.json must be updated. Place the following line in the autoload->psr-4 section:
"Hello\\": "app/code/Hello/"

For reference, see [Composer's autoloading documentation.](https://getcomposer.org/doc/01-basic-usage.md#autoloading)

#### Module

To integrate the module with composer, a composer.json file must be placed in the root of the extension.

### Routing
A router takes the given request and determines which controller and action should handle it. Routing options are configured in "etc/**<area-code>**routes.xml" (relative to extension root).

#### Router
The **router** element's **id** attribute determines which router to use for this module.

#### Route
The **route** element's **id** attribute provides a unique name for the router and module pair. Used for merging config information of multiple routers.

#### Frontname
The **module** element's **frontname** attribute is what will show up in the url corresponding to the module.

#### Area
During runtime, one of several **areas** is always active, depending on the type of user and code being executed. This module is meant for the **frontend** area. The directory structure is:
Extension/etc/**area**/routes.xml

### module.xml
The module.xml file defines the name of the module. If any of the module's dependencies need to be loaded in a particular sequence, this file can also store that sequence.

### Controller
The controller class is in Hello/Extension/Controller/Index/SayHello.php. 

#### URL
The controller is accessed at the URL <magento-base-url>/hello_extension/index/sayhello

- **hello_extension** is the frontname of the module
- **index** is the namespace of the controller (slightly different from the namespace of the class but related).
- **sayhello** is the action name.
 
#### Code
The controller class extends \Magento\Framework\App\Action\Action. It implements an **execute()** method, which contains the controller's business logic. In this case, it prints out a short message and a list of active modules. If it renders output, the output must go into the **\_response** object.

#### Response
The **\_response** object stores the information that is sent back to the client. It is a protected member of the class defined by a parent.
 
#### Parent
The parent's **dispatch()** method calls **execute()**, and then returns the **\_response** back to the system, which delivers it to the client.