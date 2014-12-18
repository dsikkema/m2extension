# Reference Extension

Thank you for trying the Magento reference extension! We created it to get you started with module development as quickly as possible. Right now it simply displays a list of Magento modules but you can use it to:

*	See the basic components of a Magento module and where they belong
*	Do a quick installation
*	See it work




## Installing and verifying the reference module

You can install the reference module in any of the following ways:

*	By copying the code to your `<magento install dir>/app/code/<VendorName>/<ModuleName>` directory.

	This method requires some manual tasks but it easy.

*	Using `composer update`.

### Installing the module by copying code

Any Magento module requires a particular directory structure under `<your Magento install dir>/app/code`. The structure starts with:

	<VendorName>\<ModuleName>

The reference module requires the following structure:

	M2demo/M2Extension

To add the module to your Magento installation:

1.	Log in to your Magento server as a user with privileges to write to the web server docroot (typically either the `root` user or the web server user).
2.	Enter the following commands in the order shown:

	<pre>cd <your Magento install dir>/app/code
	mkdir -p M2demo/M2Extension</pre>

3.	Go to the <a href="https://github.com/coldgreentea/m2extension" target="_blank">reference module GitHub</a>.
4.	Click **Download Zip**.
5.	Copy the `.zip` file you downloaded to your Magento server's `<magento install dir>/app/code/m2demo/module-m2-extension` directory.
6.	Enter the following commands in the order shown:

	<pre>unzip m2extension-master.zip
	mv m2extension-master/* .
	rm -rf m2extension-master</pre>

6.	Open `<your Magento install dir>/app/config.php` in a text editor.
7.	Add the following anywhere under: `'modules' => array (`:

	 <pre>'M2Demo_M2Extension' => 1</pre>

8.	Save your changes and exit the text editor.

### Installing the module using Composer

To install any module using `composer update`, you must modify the Magento 2 `composer.json`. The changes required for the reference module are simple, and after that it installs automatically.

To use Composer to install the module:

1.	Log in to your Magento server as a user with `root` privileges.

	**Note**: On Ubuntu, you might need to use the `sudo su` command.

2.	Change to your Magento installation directory.
3.	Open `composer.json` in a text editor.
4.	Add the following line in the `"require":` section:

	<pre>"m2demo/module-m2-extension": "*"</pre>

	**Note**: Make sure the preceding line ends with a comma character.

5.	In the `autoload": { "psr-4"` section, add the following line:

	<pre>"M2Demo\\": "app/code/M2Demo/"</pre>

	**Note**: Make sure the preceding line ends with a comma character.

6.	Save your changes and exit the text editor.
7.	From your Magento installation directory, enter the following commands in the order shown:

	composer dump-autoload
	composer update

6.	Open `<your Magento install dir>/app/config.php` in a text editor.
7.	Add the following anywhere under: 'modules' => array (`:

	 <pre>'M2Demo_M2Extension'</pre> => 1,
8.	Save your changes and exit the text editor.


### Verifying the reference module

1.	Log in to your Magento server as a user with `root` privileges.

2.	Enter the following commands in the order shown to clear the Magento cache:

	<pre>cd <your Magento install dir>/var
	rm -rf cache page_cache</pre>


9.	If you're currently logged in to the Magento Admin, log out.
10.	Log in to the Magento Admin as an administrator.
11.	Click **Stores** > **Configuration** > ADVANCED > **Advanced** > **Disable Modules Output**.

	If **m2demo_module-m2-extension** displays in alphabetical order, you successfully installed the reference module!

To see the reference module at work, enter the following URL in your browser's address or location field:

	http[s]://<your web server IP or host name>/<your Magento base dir>/demo_extension/index/sayhello

For example,

	http://www.example.com/magento/demo_extension/index/sayhello

A list of Magento modules displays. That's it! You're done!


## Components

### composer.json

#### Root

To autoload classes in the module more quickly, the root composer.json must be updated. Place the following line in the autoload->psr-4 section:
"M2Demo\\": "app/code/M2Demo/"

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
The controller class is in app/code/M2Demo/M2Extension/Controller/Index/SayHello.php. 

#### URL
The controller is accessed at the URL <magento-base-url>/demo_extension/index/sayhello

- **demo_extension** is the frontname of the module
- **index** is the namespace of the controller (slightly different from the namespace of the class but related).
- **sayhello** is the action name.
 
#### Code
The controller class extends \Magento\Framework\App\Action\Action. It implements an **execute()** method, which contains the controller's business logic. In this case, it prints out a short message and a list of active modules. If it renders output, the output must go into the **\_response** object.

#### Response
The **\_response** object stores the information that is sent back to the client. It is a protected member of the class defined by a parent.
 
#### Parent
The parent's **dispatch()** method calls **execute()**, and then returns the **\_response** back to the system, which delivers it to the client.
