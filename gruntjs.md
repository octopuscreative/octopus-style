# GruntJs

1. Add pacakge.json to root directory
2. Add your gruntfile.js to the root directory
3. Run `$ npm install` from the directory that holds package.json to install grunt & its dependencies. 

```
// package.json

{
  "name": "Application Name",
  "version": "0.1.0",
  "devDependencies": {
    "grunt": "~0.4.2",
  }
}
```


```
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

To add new grunt plugins to your project

1. Install the npm module `$ npm install module-name --save-dev` - This will also declare this module as a dev dependency in your package.json file.
2. Register the new plugin in your gruntfile.js (e.g. `grunt.loadNpmTasks('grunt-contrib-concat');`)