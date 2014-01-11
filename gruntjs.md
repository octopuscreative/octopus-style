# Grunt.js

[Grunt](http://gruntjs.com) is an indespensible tool for automating many of the repetitive tasks that we web developers perform every day. Although it can take some time to setup in the beginning, the time saved through using Grunt well outweighs the cost.

If you've never used Grunt before, don't worry! [Grunt is not wierd and hard](http://24ways.org/2013/grunt-is-not-weird-and-hard/) by [Chris Coyier](http://csstricks.com) is a great introduction to Grunt and will help you cover the basics quickly, as well as point you to some more advanced reading.

To get started with Grunt:

1. Add pacakge.json to root directory
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

To add new [Grunt plugins](http://gruntjs.com/plugins) to your project

1. Install the npm module `$ npm install module-name --save-dev` - This will also declare this module as a dev dependency in your package.json file.
2. Register the new plugin in your gruntfile.js (e.g. `grunt.loadNpmTasks('grunt-contrib-concat');`)