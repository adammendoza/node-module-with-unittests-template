# Node Module with Unittests Template #

This repository provides scaffolding to promptly bootstrap writing your own node module with unittests.
The unittests are run both within node environment and on the browser (which can help you determine
if your code works as expected on different browsers). The unittests get full coverage reports.

You also get a fully automated document creation from source code, automatic updating of your final
module/library name and version in README.md, and an html version of your README.md file.

## Quick Installation ##

After cloning this scaffolding from github, jut type `npm install` and this scaffolding will install
all the necessary dependencies.

## Quick Start ##

Replace ./src/dummy.js with your own module code and ./test/unittests/ with your own unittest. Type
`grunt` and you will get tests running both under node environment and browsers, your documentation,
and your full fledged README.md and README.md.html files.

## README.md vs. README.md.copy ##

README.md (this very file) is overwritten when you run "replace:dist" step of your Grunfile.js.
"replace:dist" will take your README.md.template, and replace certain varibles and produce your
final README.md file which overwrites this file. Thus, there is a copy of this file at README.md.copy.
This copy will not be deleted unless you delete it yourself.

## Scaffolding Explained ##

In this section, we describe what each file does in this template and how you can modify them to your needs.

<div style='padding: 20px'>

### ./Gruntfile.js ###

This is where all the magic lives. Gruntfile.js describes all the tasks, and how they interact
with each other. It can run your tests, create browser version of your tests, run them in
the browser, create their coverage reports, create documentation, create your dynamically
generated README.md, and README.md.html files and create your final browserified library along
with its minimized version.

### ./jsdoc.conf ###

JSDoc configuration file. You can modify this file to change the behaviour of JSDoc which is used to create
documentation from the source code.

### ./package.json ###

NPM package.json file. You describe your module in this file. The values for 'name' and 'version' fromthis file are later used in producing README.md file.

### ./README.md.template ###

This is "almost" your README.md file except you can replace text patterns dynamically during Grunt run.
In Grunt.js file, there is a step/task called "replace:dist" which will take this README.md.template,
replace text patterns you identify in the task with their produced values, and produce the README.md file.
This lets you for example dynamically add the version number to README.md file.

### ./src/dummy.js ###

This file is an example for the entry point of your library/module. You can replace it with your own module
js file(s). The Grunt.js file assumes that the entry point file to your library will be the same as the name
of your module. So, if your library is called 'dummy' in package.json, your entry point file should be named
dummy.js.

### ./test/unittests/dummy-test.js ###

You can add multiple test files to ./test/unittests/ directory. You probably want to have as many test files
under this directory as your source js file under ./src directory. In other words, you want to have one to one
mapping to your src files. I suggest for good housekeeping, every single file here should test one and only
one js file under ./src.

### ./test/index.html.template ###

This file is processed by "replace:browserified_tests_file" task to produce an index.html file.
"replace:browserified_tests_file" task writes the location of your browserified unittests into the
index.html.template to produce the final index.html file. This 'index.html' file is then used
by "mocha_phantomjs:all" task to run the browserified unittests.

</div>

## ./Gruntfile.js and Tasks ##

<div style='padding:20px'>

### browserify ###

Browserifies the library so that your library can run in a browser.

### clean ###

#### clean:dist ####

Deletes the minimized and unminimized final output files.

#### clean: docs ####

Deletes the docs.

#### clean:tests ####

Deletes the output of tests and browserified tests.

### connect ###

Starts a basic web server.

### jsdoc ###

Creates documentation from src files using jsdoc.

### jshint ###

Runs the code through jshint.

### markdown ###

Creates an html version of the README.md file called README.md.html.

### mocha_phantomjs ###

Runs the browserified tests thru PhantomJS.

### mochaTest ###

Runs the unittests.

### replace ###

Replaces text patterns in (template) files.

#### replace:browserified_test_file ####

Replaces text patterns in the index.html.template.

#### replace:dist ####

Replaces text patterns in README.md.template.

### uglify ###

Minimizes the output of browserified library/module.

</div>

## Custom Tasks ##

## browsertest ##

Runs 'clean:tests', 'jshint', 'browserify', 'replace:browserified_tests_file', 'connect:server', 'mocha_phantomjs' respectively.

## dist ##

Runs 'clean:dist', 'browserify', 'uglify' respectively.

## docs ##

Runs 'clean:docs', 'replace:dist', 'markdown', 'jsdoc' respectively.

## localtest ##

Runs 'clean:tests', 'jshint', 'mochaTest' respectively.

## test ##

Runs 'localtest', 'browsertest' respectively.

# Produced files and directories #

## ./README.md ##

Dynamically generated README.md file from README.md.template.

## ./README.md.html ##

Generated from README.md file.

## ./docs/* ##

Generated by 'jsdoc' task. All documentation in the src files should follow jsdoc format so that
this task can produce all the documentation.

## ./dist/* ##

Generated by browserify and uglify and will have your final minimized and unminimized library.

## ./test/output/coveragereport.html ##

This is an important file. It tells you how much your unittests cover your code. I recommend
to have full coverage at >98% as it will help you to catch bugs early on.

## ./test/output/browser_tests_results.txt ##

Test results from the browser run of the browserified unittests.

## ./test/output/output.txt ##

Test results from the node run of the unittests.

## projectparams section of Gruntfile.js ##

This section has all the parameters necessary to run the scaffolding correctly.

### Description of the variables in projectparams ###

* **readme_md_template:** README.md.template file name.
* **readme_md_text_file:** (Generated) README.md file name.
* **readme_md_html_file:** (Generated) README.md.html file name.
* **src_dir:** Directory where source files are located.
* **test_dir:** The root test directory. 'index.html.template' is assumed to be here.
* **unittests_dir:** Directory where the unittests are.
* **docs_dir:** (Generated) Directory for the docs.
* **dist_dir:** (Generated) Directory for the distribution files.
* **unittests_output_dir:** (Generated) Unittest output reports will be written here.
* **unittests_text_output_file:** (Generated) Node unittest run reports.
* **unittests_browsertest_results_file:** (Generated) Browser unittest run reports.
* **unittests_coverage_report_file:** (Generated) Coverage reports for unittests.
* **unittests_also_to_be_browsertested:** List of unittests also to be run in the browser.
* **unittests_browsertest_index_html_template:** 'index.html.template' file name.
* **unittests_browsertest_index_html:** 'index.html' file for browser unittests.
* **output_file:** Final browserified output file of your library.
* **minimized_output_file:** Minimized browserified output file of your library.
* **banner_for_production:** The first line for both the browserified output file and the minimized version.
