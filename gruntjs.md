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

To add new [Grunt Plugins](http://gruntjs.com/plugins) to your project

1. Install the npm module `$ npm install module-name --save-dev` - This will also declare this module as a dev dependency in your package.json file.
2. Register the new plugin in your gruntfile.js (e.g. `grunt.loadNpmTasks('grunt-contrib-concat');`)

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