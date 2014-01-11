# Grunt.js

[Grunt](http://gruntjs.com) is an indispensable tool for automating many of the repetitive tasks that we web developers perform every day. Although it can take some time to setup in the beginning, the time saved through using Grunt well outweighs the cost.

If you've never used Grunt before, don't worry! [Grunt for People Who Think Things Like Grunt are Weird and Hard](http://24ways.org/2013/grunt-is-not-weird-and-hard/) by [Chris Coyier](http://csstricks.com) is a great introduction to Grunt and will help you cover the basics quickly, as well as point you to some more advanced reading.

To get started with Grunt:

1. Add package.json to root directory
2. Add your gruntfile.js to the root directory
3. Run `$ npm install` from the directory that holds package.json to install grunt & its dependencies. 

```json
package.json

{
  "name": "Application Name",
  "version": "0.1.0",
  "devDependencies": {
    "grunt": "~0.4.2",
  }
}
```


```javascript
// gruntfile.js

module.exports = function(grunt) {

    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        
        concat: {
            dist: {
                src: ['assets/js/vendor/*.js'],
                dest: 'assets/js/production.js'
            }
        }

    });

    // Register your plugins here
    grunt.loadNpmTasks('grunt-contrib-concat');

    // Register your tasks here
    grunt.registerTask('default', ['concat']);

};
```

To add new [Grunt Plugins](http://gruntjs.com/plugins) to your project:

1. Install the npm module `$ npm install module-name --save-dev` - This will also declare this module as a dev dependency in your package.json file.
2. Register the new plugin in your gruntfile.js (e.g. `grunt.loadNpmTasks('grunt-contrib-concat');`)

## Load-grunt-tasks

Typically, every Grunt plugin that is used must be explicitly declared with `grunt.loadNpmTasks()`. Often times this leads to a long list of plugins, like below:

```javascript
grunt.loadNpmTasks('grunt-contrib-concat');
grunt.loadNpmTasks('grunt-contrib-coffee');
grunt.loadNpmTasks('grunt-contrib-sass');
grunt.loadNpmTasks('grunt-contrib-uglify');
grunt.loadNpmTasks('grunt-contrib-clean');
grunt.loadNpmTasks('grunt-grunticon');
grunt.loadNpmTasks('grunt-contrib-watch');
grunt.loadNpmTasks('grunt-contrib-imagemin');
grunt.loadNpmTasks('grunt-svgmin');
```

By using the plugin load-grunt-tasks, we can make this list much more concise:

```javascript
require('load-grunt-tasks')(grunt);
```

Load-grunt-tasks works by using a [glob pattern](http://en.wikipedia.org/wiki/Glob_(programming)) to load any dev dependencies listed in your package.json file.

For example, if you wanted to load only grunt-contrib tasks, you could use:

```javascript
require('load-grunt-tasks')(grunt, {pattern: 'grunt-contrib-*'});
```

To install load-grunt-tasks, simply run `$ npm install load-grunt-tasks --save-dev` from the same directory as your package.json file.

## Commonly Used Plugins
* [grunt-contrib-clean](https://npmjs.org/package/grunt-contrib-clean)
* [grunt-contrib-concat](https://npmjs.org/package/grunt-contrib-concat)
* [grunt-contrib-watch](https://npmjs.org/package/grunt-contrib-watch)
* [grunt-contrib-cssmin](https://npmjs.org/package/grunt-contrib-cssmin)
* [grunt-contrib-uglify](https://npmjs.org/package/grunt-contrib-uglify)
* [grunt-contrib-imagemin](https://npmjs.org/package/grunt-contrib-imagemin)
* [grunt-contrib-sass](https://npmjs.org/package/grunt-contrib-sass)
* [grunt-contrib-coffee](https://npmjs.org/package/grunt-contrib-coffee)
* [grunt-grunticon](https://npmjs.org/package/grunt-grunticon)
* [grunt-processhtml](https://npmjs.org/package/grunt-processhtml)
* [load-grunt-tasks](https://github.com/sindresorhus/load-grunt-tasks)

# Sample Gruntfile.js

```javascript
module.exports = function(grunt) {

    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),

        coffee: {
            compile: {
                files: {
                    'src/js/vendor/coffee-vendor-compiled.js' : 'src/js/vendor/*.coffee',
                    'src/js/coffee-application-compiled.js' : [
                        'src/js/global/*.coffee',
                        'src/js/*.coffee',
                        'src/js/vendor/!(*).coffee'
                    ]
                }
            }
        },

        concat: {
            vendor: {
                src: 'src/js/vendor/*.js',
                dest: 'lib/js/vendor.js'
            },

            applicaton: {
                src: [
                    'src/js/global/*.js',
                    'src/js/*.js',
                    'src/js/vendor/!(*).js' // Ignore /vendor
                ],
                dest: 'lib/js/application.js'
            }
        },

        uglify: {
            vendor: {
                src: 'lib/js/vendor.js',
                dest: 'lib/js/vendor.min.js'
            },

            application: {
                src: 'lib/js/application.js',
                dest: 'lib/js/application.min.js'
            }
        },

        clean: [
            'src/js/vendor/coffee-vendor-compiled.js',
            'src/js/coffee-application-compiled.js'
        ],

        sass: {
            dist: {
                options: {
                    style: 'compressed'
                },
                files: {
                    'lib/css/application.min.css' : 'src/css/application.scss'
                }
            }
        },

        svgmin: {
            dist: {
                files: [{
                    expand: true,
                    cwd: 'src/icons',
                    src: ['**/*.svg'],
                    dest: 'src/icons',
                }]
            }
        },

        grunticon: {
            icons: {
                files: [{
                    expand: true,
                    cwd: 'src/icons',
                    src: ['*.svg', '*.png'],
                    dest: 'lib/icons'
                }],
                options: {
                    template: 'src/icons/css.hbs',
                    customselectors: {
                        "*": [".icon-$1--before:before", ".icon-$1--after:after"]
                    }
                }
            }
        },

        imagemin: {
            images: {
                expand: true,
                cwd: 'src/images',
                src: '*.{png,jpg,gif}',
                dest: 'lib/images'
            }
        },

        /*==========  Watcher  ==========*/

        watch: {
            scripts: {
                files: ['src/js/*.js', 'src/js/*.coffee', 'src/js/*/*.js', 'src/js/*/*.coffee'],
                tasks: ['coffee', 'concat', 'uglify', 'clean'],
                options: {
                    spawn: false
                }
            },

            css: {
                files: ['src/css/*.scss', 'src/css/*.css', 'src/css/*/*.scss', 'src/css/*/*.css'],
                tasks: ['sass'],
                options: {
                    spawn: false
                }
            },

            icons: {
                files: ['src/icons/*.svg', 'src/icons/*.png'],
                tasks: ['svgmin','grunticon'],
                options: {
                    spawn: false
                }
            },

            images: {
                files: ['src/images/*.{png,jpg,gif}'],
                tasks: ['imagemin'],
                options: {
                    spawn: false
                }
            }
        }

    });

    // Where we tell Grunt we plan to use this plug-in.
    require('load-grunt-tasks')(grunt);

    // Where we tell Grunt what to do when we type "grunt" into the terminal.
    grunt.registerTask('default', ['coffee', 'concat', 'uglify', 'clean', 'sass', 'svgmin', 'grunticon', 'imagemin']);
    grunt.registerTask('dev', ['watch']);

};
```