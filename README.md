
Description how to run Grails IDE (set of plugins to work with obsolete Grails 2 framework) with Eclipse Oxygen.

## Introduction

If you still need to work with projects written in Grails 2 framework, here is description how to
run Grails IDE in Oxygen.2 Eclipse release.

Main problem was Grails IDE itself as it is not maintained for some time. Last available version has conflicts with newest lib versions and uses removed/deprecated API's. I've made fork of [this](https://github.com/spring-projects/grails-ide) project (you can check [here](https://github.com/TomSzymko/grails-ide)) and adjusted it to build properly and work with Oxygen Eclipse and newest GrEclipse plugins.

This updated plugin is essential in described process.

## Prerequisites
 * ensure you have JDK 8 installed (it is Eclipse Oxygen prerequisite).
 * download updated `Grails IDE` plugins from this project:
    * file `org.grails.ide.eclipse.site-3.6.4-SNAPSHOT.zip` from `bin` folder

### Warning!
* below description was tested only on Windows environment
* this process was made on clean and fresh Oxygen instance, probably there are some problems if other plugins are installed (especially Spring IDE)

# Eclipse installation

* go to Eclipse [download](http://www.eclipse.org/downloads/eclipse-packages/) page
* download newest _Eclipse IDE for Java EE Developers_
    * I've used Windows version: `eclipse-jee-oxygen-2-win32-x86_64.zip`
* unpack archive

## Eclipse initial setup

* (optional) you can increase initial memory pool in `eclipse.ini` file
    * e.g. you can set
        ```
        -Xms1g
        -Xmx4g
        ```


# Grails IDE installation

* create file `bookmarks.xml` with following content (used update sites):
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <bookmarks>
       <site url="http://dist.springsource.org/snapshot/GRECLIPSE/e4.7/" selected="true" name="GrEclipse"/>
       <site url="http://download.eclipse.org/tools/ajdt/47/dev/update" selected="true" name="AJDT"/>
       <site url="jar:file:/C:/download/org.grails.ide.eclipse.site-3.6.4-SNAPSHOT.zip!/" selected="true" name="Grails IDE (Oxygen)"/>
    </bookmarks>
    ```
    * replace `/C:/download/` by path to location where you saved `org.grails.ide.eclipse.site-3.6.4-SNAPSHOT.zip` downloaded from this project
* start your Eclipse Oxygen
* from `Help` menu select `Install New Software..`
    * click `Manage..`
    * click `Import` and import `bookmarks.xml`. Close dialog.
    * use `GrEclipse` update site and install:
        * `Groovy Compiler 2.4`
        * `Groovy-Eclipse Feature`
        * `JDT Core patch for Groovy-Eclipse plugin on Eclipse 4.7`
    * use `AJDT` update site and install:
        * `AspectJ Development Tools`
        * all items from `Other AJDT Tools` group
    * use `Grails IDE (Oxygen)` update site and install all available items
        * ignore warning about not signed content
    * in preferences set at least one Grails Installation

Now you're ready to import Your Grails 2 project! Enjoy!

# Known issues

* support for Grails 1.3 was removed from this version of plugin
* I did not changed plugin versioning, it is same as original one (to be fixed some day)

# Building Grails IDE

To build updated `Grails IDE` use:
```
mvn -Pe47 -Dmaven.test.skip=true clean install
```
