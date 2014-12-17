


## Installing and verifying the reference module

You can install the reference module in any of the following ways:

*	By copying the code to your `<magento install dir>/app/code/<VendorName>/<ModuleName>` directory.

	This method requires some manual tasks but it easy.

*	Using `composer update`.

### Installing the module by copying code

Any Magento module requires a particular directory structure under `<your Magento install dir>/app/code`. The structure starts with:

	<VendorName>\<ModuleName>

The reference module requires the following structure:

	m2demo/module-m2-extension

To add the module to your Magento installation:

1.	Log in to your Magento server as a user with privileges to write to the web server docroot (typically either the `root` user or the web server user).
2.	Enter the following commands in the order shown:

	cd <your Magento install dir>/app/code
	mkdir -p m2demo/module-m2-extension

3.	Go to the <a href="https://github.com/coldgreentea/m2extension" target="_blank">reference module GitHub</a>.
4.	Click **Download Zip**.
5.	Copy the `.zip` file you downloaded to your Magento server's <magento install dir>/app/code/m2demo/module-m2-extension` directory.
6.	Enter the following commands in the order shown:

	unzip unzip m2extension-master.zip
	mv m2extension-master/* .
	rm -rf m2extension-master

6.	Open `<your Magento install dir>/app/config.php` in a text editor.
7.	Add the following anywhere under: 'modules' => array (`:

	 'M2Demo_M2Extension' => 1,
8.	Save your changes and exit the text editor.

### Installing the module using Composer

To install any module using `composer update`, you must modify the Magento 2 `composer.json`. The changes required for the reference module are simple, and after that it installs automatically.

To use Composer to install the module:

1.	Log in to your Magento server as a user with `root` privileges.

	**Note**: On Ubuntu, you might need to use the `sudo su` command.

2.	Change to your Magento installation directory.
3.	Open `composer.json` in a text editor.
4.	Add the following line in the `"require":` section:

	"m2demo/module-m2-extension": "*"

	**Note**: Make sure the preceding line ends with a comma character.

5.	In the `"psr-4":` section, add the following line:

	"M2Demo\\": "app/code/M2Demo/"

	**Note**: Make sure the preceding line ends with a comma character.

6.	Save your changes and exit the text editor.
7.	From your Magento installation directory, enter the following commands in the order shown:

	composer dump-autoload
	composer update

6.	Open `<your Magento install dir>/app/config.php` in a text editor.
7.	Add the following anywhere under: 'modules' => array (`:

	 'M2Demo_M2Extension' => 1,
8.	Save your changes and exit the text editor.


### Verifying the reference module

1.	Log in to your Magento server as a user with `root` privileges.

2.	Enter the following commands in the order shown to clear the Magento cache:

	cd <your Magento install dir>/var
	rm -rf cache page_cache

9.	If you're currently logged in to the Magento Admin, log out.
10.	Log in to the Magento Admin as an administrator.
11.	Click **Stores** > **Configuration** > ADVANCED > **Advanced** > **Disable Modules Output**.

	If **m2demo_module-m2-extension** displays in alphabetical order, you successfully installed the reference module!

To see the reference module at work, enter the following URL in your browser's address or location field:

	http[s]://<your web server IP or host name>/<your Magento base dir>/demo_extension/index/sayhello

A list of Magento modules displays. That's it! You're done!