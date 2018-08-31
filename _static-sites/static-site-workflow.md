---
layout: post
title:  "Static site workflow"
description: "Step by step instructions for creating a simple responsive static site."
---

## Workflow

This workflow uses Bootstrap, specifically the grid system to achieve a simple responsive single column site.

The workflow also implements effective development tools. Browsersync offers a lot of testing functionality; especially useful is the ability to view the website over multiple devices over a shared local network. Contrib sass compiles Sass to CSS, and when combined with Contrib watch, the compilation happens automatically on save. Additionally, the site is automatically reloaded whenever any changes are saved.

This allows the smooth and effective development of a static site.

## 1 Create the structure

```
- index.html
- gruntfile.js
- package.json
- README.md
- js/
	- main.js
- styles/
	- css/
	- sass/
		- styles.sass
- assets/
	- fonts/
	- images/
```

## 2 Write the markup

**Bootstrap** - [Documentation](https://getbootstrap.com/docs/4.0/getting-started/introduction/)

Include links to CDN in the head of the document:

```html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css" integrity="sha384-PsH8R72JQ3SOdhVi3uxftmaW6Vc51MKb0q5P2rRUpPvrszuE4W1povHYgTpBfshb" crossorigin="anonymous">
<script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.3/umd/popper.min.js" integrity="sha384-vFJXuSJphROIrBnz7yo7oB41mKfc8JzQZiCq4NCceLEaO4IHwicKwpJf9c9IpFgh" crossorigin="anonymous"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/js/bootstrap.min.js" integrity="sha384-alpBpkh1PFOepccYVYDB4do5UnbKysX5WZXm3XxPqe5iKTfUKjNkCk9SaVuEZflJ" crossorigin="anonymous"></script>
```

## 3 Set up [build tools](https://wearejh.com/frontend-automation-with-grunt-sass-browsersync/)

### Fill out the [gruntfile.js](https://github.com/Dinkers/Static-Site-Builder/blob/master/build_files/gruntfile.js) in the top level of the project:

```javascript
module.exports = function(grunt) {

    grunt.initConfig({

        // Watch task config
        watch: {
            sass: {
                files: ['styles/sass/styles.sass'],
                tasks: ['sass']
            }
        },

        // SASS compile task config
        sass: {
            dev: {
                files: {
                    "styles/css/styles.css" : "styles/sass/styles.sass",
                }
            }
        },

        // Browser sync config
        browserSync: {
            default_options: {
                bsFiles: {
                    src: [
                    'styles/css/styles.css',
                    'js/main.js',
                    '*.html'
                    ]
                },
                options: {
                    watchTask: true,
                    server: {
                        baseDir: "./"
                    }
                }
            }
        }
    });

    grunt.loadNpmTasks('grunt-contrib-watch');
    grunt.loadNpmTasks('grunt-contrib-sass');
    grunt.loadNpmTasks('grunt-browser-sync');

    grunt.registerTask('default', ['browserSync', 'watch']);

};
```

### Fill out [package.json](./package.json) in the top level of the project (replacing PROJECT_NAME, AUTHOR, and GITHUB_URL appropriately):

```javascript
{
  "name": "PROJECT_NAME",
  "author": "AUTHOR",
  "version": "1.0.0",
  "description": "",
  "main": "index.html",
  "devDependencies": {
    "grunt": "^1.0.0",
    "grunt-browser-sync": "^2.2.0",
    "grunt-contrib-sass": "^1.0.0",
    "grunt-contrib-watch": "^1.1.0"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+GITHUB_URL"
  },
  "license": "ISC",
  "bugs": {
    "url": "GITHUB_URL/issues"
  },
  "homepage": "GITHUB_URL#readme",
  "dependencies": {
    "npm": "^6.3.0"
  }
}
```

### Install the npm packages:
	npm install

### Run the site and start the sass watcher:
	grunt

## 4 Write SASS styles

* [SASS Documentation](http://sass-lang.com/guide)
* [Bootstrap Documentation](https://getbootstrap.com/docs/4.0/getting-started/introduction/)
* [Mobile first design guide](https://www.uxpin.com/studio/blog/a-hands-on-guide-to-mobile-first-design/)


## 5 Write JavaScipt

## 6 Deploy

---

The build process of this workflow has been automated, and can be sped up with the use of the [Static Site Builder](https://github.com/Dinkers/Static-Site-Builder).