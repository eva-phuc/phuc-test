phuc-test
=========


### Setup staging environment

```
$ cd vagrant
$ vagrant up
```


Set /etc/hosts like below

```
dev.btob-market.com  192.168.33.104
```

Then you can staging environment

```
http://dev.btob-market.com
```


### Install Prepros tool

1.  Download Prepros and install it.

    -	Download link

    ```
    https://prepros.io/downloads
    ```

    -	Choose OS that you use.
    ![](img/prepros.png)
    -	Install it to your computer.

2.  Create new folder.

    -	Create your new folder (ex: sass folder).
    -	Copy file css or image to this folder.

3.  Start using Prepros.

    -	Open up Prepros.
    -	Add project on Prepros.
    ![](img/add_project.png)
    -	Choose the new folder above (ex: sass folder).
    -	Choose one file that you want compress.
    -	Click "Process File".
    ![](img/use_prepros.png)
    -	Prepros will compress your file.


### Install Grunt on Windows

1.  Download and install Node.js

    -   Download link (choose .msi version)

    ```
    http://nodejs.org/download/
    ```

    -   Install Node.js, change directory to ``` C:\nodejs ```
    -   Check npm work:

    ```cmd
    > npm -v
    1.4.28
    ```

2.  Install Grunt
    
    ```cmd
    > npm install -g grunt-cli
    ```

    -   Check Grunt work:

    ```cmd
    > grunt -V
    grunt-cli v0.1.13
    ```

3.  Setup Grunt into btob-market repository

    -   Go to the project's root directory.

    ```
    \apache\vhosts\www.btob-market.com\htdocs
    ```

    -   Create package.json file

    ```
    {
        "name": "btob-market",
        "version": "0.1.0",
        "description": "A packaged for btob-market",
        "private": true,
        "repository": {
            "type": "svn",
            "url": ""
        },
        "engines": {
            "node": ">= 0.8.0"
        },
        "devDependencies": {
            "grunt": "~0.4.5",
            "grunt-contrib-concat": "~0.5.0",
            "grunt-contrib-uglify": "~0.6.0",
            "grunt-contrib-watch": "~0.6.1"
        }
    }
    ```

    -   Open cmd and cd to root directory.
    -   Run cmd ``` npm install ``` to install package module
    -   Create Gruntfile.js file

    ```
    module.exports = function (grunt) {
        var pkg = grunt.file.readJSON('package.json');
        grunt.initConfig({
            concat: {
                files: {
                    src : 'js/*.js',
                    dest: 'js/concat/hogehoge.js'
                }
            },

            uglify: {
                dist: {
                    files: {
                        'js/min/sample.min.js': 'js/concat/hogehoge.js'
                    }
                }
            },

            watch: {
                js: {
                    files: 'js/*.js',
                    tasks: ['concat', 'uglify']
                }
            }
        });

        grunt.loadNpmTasks('grunt-contrib-uglify');
        grunt.loadNpmTasks('grunt-contrib-concat');
        grunt.loadNpmTasks('grunt-contrib-watch');
        grunt.registerTask('default', ['concat', 'uglify']);
    };
    ```

    -   Run grunt.

    ```cmd
    > grunt
    Running "concat:files" (concat) task
    File js/concat/hogehoge.js created.

    Running "uglify:dist" (uglify) task
    >> 1 file created.

    Done, without errors.
    ```
    
