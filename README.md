#UecodeDaemonBundle #
##Overview##
UecodeDaemonBundle is a wrapper for the PEAR library System_Daemon which was created by Kevin Vanzonneveld.

This will enable you to install the symfony bundle and easily convert your Symfony2 console scripts into system daemons.

pcntl is required to be configured in your PHP binary to use this. On my Ubuntu server I was able to install pcntl easily with the following command:

    sudo apt-get install php-5.3-pcntl-zend-server 

##System_Daemon PEAR package##
System_Daemon is a PHP class that allows developers to create their own daemon 
applications on Linux systems. The class is focussed entirely on creating & 
spawning standalone daemons

More info at:

- [Blog Article: Create daemons in PHP][1]
- [Report Issues][2]
- [Package Statistics][3]
- [Package Home][4]

  [1]: http://kevin.vanzonneveld.net/techblog/article/create_daemons_in_php/
  [2]: http://pear.php.net/bugs/report.php?package=System_Daemon
  [3]: http://pear.php.net/package-stats.php?pid=798&cid=37
  [4]: http://pear.php.net/package/System_Daemon


##DaemonBundle Config##
Place Uecode\Daemonbundle in your src directory and do the following:


### appKernel.php ###
Add The UecodeDaemonBundle to your kernel bootstrap sequence

    public function registerBundles()
    {
        $bundles = array(
            //...
            new Uecode\Bundle\UecodeDaemonBundle\UecodeDaemonBundle(),
        );
        //...

        return $bundles;
    }

### config.yml ###
By Default, system daemons have a sensible configuration. If you need to change any configuration setting , you could do it by adding this configuration to your project config. Only the values that need to be changed should be added, the bundle extension will merge your daemon configs into its defaults.

    app/config.yml

    #UecodeDaemonBundle Configuration Example
    code_meme_daemon:
        daemons:
            #creates a daemon using default options
            example: ~

            #an example of all the available options
            explicitexample:
                appName: example
                appDir: %kernel.root_dir%
                appDescription: Example of how to configure the DaemonBundle
                logLocation: %kernel.logs_dir%/%kernel.environment%.example.log
                authorName: Aaron Scherer
                authorEmail: aequasi@gmail.com
                appPidLocation: %kernel.cache_dir%/example/example.pid
                sysMaxExecutionTime: 0
                sysMaxInputTime: 0
                sysMemoryLimit: 1024M
                appUser: apache
                appGroup: apache
                appRunAsGID: 1000
                appRunAsUID: 1000

##Creating a Daemon##

##Usage##
Once you have Daemonized your symfony Console Commands, you can simply run them from the command line like so:

    aequasi@ue:~/example$ php app/console queue:start

    aequasi@ue:~/example$ php app/console queue:stop

    aequasi@ue:~/example$ php app/console queue:restart
