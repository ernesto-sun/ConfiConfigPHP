# Confi Config PHP

A small PHP script to manage your project-configuration comfortably.

Made to be integrated into any kind of PHP-project. 
 
Developed in the context of [Total.HTM Easy](https://github.com/ernesto-sun/Total.HTM-Easy). 

*Confi Config PHP* is Open Source.

## Why this project?

A one-script solution for all those ever-repeating steps needed to set up 
a kind-of-safe configuration file structure - it saves me boring time!   

Because it is boring to set up a configuration at each specific web-server
for each of my clients. 

Because it is boring to look up its own configuration of each of my 
PHP-projects done somehow somewhere different each time. 


## Who is it for?

Confi Config PHP is made for developers, hackers, coders, etc. 

## Getting Started

### Prerequisites

* PHP (>=5) running on a web-server like Apache
* File-Access for PHP-scripts (read and write)

  
### Installing

Copy the project files (as download-able here) to your desired location.

```
Example-location: http://my-server.com/my-folder/
```

## How to Use 

### Creating a new Config 

See the file: 'config_script.php'. It is a stand-alone PHP-script.

The files that start with 'config_set_...' are your simple setting-files.   

1) Text-edit 'config_script.php' and change API_KEY to some random new value.

2) Create and modify the setting files as you need it for your project.

3) Copy config_script.php and the setting-files to your intended location. 

4) Call config_script.php for the first time. Example: 

```
http://my-server.com/my-folder/config_script.php?ak=xxx (xxx is the API_KEY)

```

Now, some 'kind-of-secret' file structure has been set up. You know it worked
if the file 'config_dont_touch.php' was created.

In some cases, 'the config_script.php' can not find any write-able folder, and 
or you want to set some specific folder hardcoded. You can do that at the top
of the file 'config_script.php' by setting PATH_HARDCODED to an absolute path.  

If you want to reset your current config or create a completely new one, just
remove the file 'config_dont_touch.php' and start over. 


### Using a Config within my PHP code

The following PHP-snippet includes your Config info:

```
$ok_come_from_api=1;
include('config_dont_touch.php');
 
```

See the values you have at your hands. You can output the complete Config
e.g. by this bit of code:

```
echo json_encode($GLOBALS['config']);

```

Some kind-of-secret folders have been created for you. Here you can put your 
kind-of-secret files. 

* $GLOBALS['config']['dir_sec_l']  for your log-files
* $GLOBALS['config']['dir_sec_u']  for user-accounts
* $GLOBALS['config']['dir_sec_d']  for any other data 


A simple example for writing a file to the data-folder:

```
file_put_contents($GLOBALS['config']['dir_sec_d'].'my_filename.y7');   

```

Its recommended to use the extension .y7 for your kind-of-secret files, just 
because that extension is further protected from being shown online by some
htaccess-files that have been automatically created.  

Some meta-information was created as well, accessible like this:

```
include($GLOBALS['config']['dir_sec']."meta.y7");
echo json_encode($GLOBALS['meta']);

```

### Changing Settings

The config_script reads all files that match 'config_set_\*.php'. That means,
you can just create new setting-files, useful for grouping if you have lots
of settings. However, within one setting file can be an unlimited number of
setting values. 

The one file called 'config_set_sec.php' is here for secrets. After each call
of the config_script the values in this file are emptied. 

Use setting-names only once. (Later ones overwrite earlier ones.)

**IMPORTANT**: To set a setting-value to empty "" does NOT clear the value! 
Empty settings are ignored and keep set! Instead use these special keywords 
to clear or completely remove settings: "\_\_CLEAR\_\_" and "\_\_DELETE\_\_"
	
Here an example setting file such as 'config_set_test.php'; 
	
``` 
<?php if(!isset($ok_come_from_config_script)) die();
$set_config = array (
  'bool_custom' => 1,
  'minify_css' => 1,
  'double_custom' => 2.23,
  'string_custom' => 'Hello user!',  
);
	
``` 	
		
IMPORTANT: After changing settings the config_script needs to be called once, 
in order to write the changes into the 'kind-of-secret' Config. 		
	
## Deployment

Just add the config_script to your PHP-project. There is not much that can 
go wrong, because there is not much code at all.

I usually put the config_script.php and the setting-files into the root
directory of the PHP-project the Config belongs to. 

Each of my PHP-project just has it's own config_script delivered with it. 
When I install a project at some server, the first thing I do after copying
it all online, is, adapt the settings and call the config_script. 


## Built With

Confi Config PHP is a one-script solution not including any library. It uses
basic PHP-functions what might work even with older PHP-versions than 5. Also 
no special PHP packages needed. It's all about file-read and -write really. 

I want to give big thanks to the developers of PHP, and special thanks for the
version PHP 7, that is so much faster, saves cost and energy. What I hear 
about upcoming version 8 is promising as well. E.g. 'Just in Time Compiling' 

Thank You, PHP team! https://www.php.net/credits.php


## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) if you want to be part of this project. 
You are welcome! Also with your harsh critics or a very strange idea.  


## Versioning

We use version numbers like V02, V03 for public releases. Internally we use
timestamps to identify versions. Such as '20201221' for 21. Dec, 2020. 


## Authors

* **[Ernesto Sun](http://ernesto-sun.com)** 
* *You are welcome!*


## License

This project is licensed under the JSON License - see the [LICENSE.md](LICENSE.md) file for details

The JSON License is same same to the MIT License, plus one ethical clause. I love it!


## Acknowledgments

Thank you, many sources of inspiration. Among them:

* The INNOQ podcast (and spirit): https://www.innoq.com/en/podcast/ (German only)
* ROCA style and the man behind it, Stefan Tilkov: https://roca-style.org/
* The Working Draft podcast: https://workingdraft.de/  (German only)




