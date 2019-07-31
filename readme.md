# Picklewagon Coding Standard

Include this package in your project to enforce the coding standard used for Picklewagon projects.

## Install

Add to composer.json. Since it is a private package, you have to add some dependencies as well.

```
"require-dev": {
    ...
    "picklewagon/picklewagon-coding-standards": "1.0.0"
},
"repositories": [
    {
        "type": "vcs",
        "url": "git@bitbucket.org:picklewagon/picklewgon-coding-standards.git"
    }
],
```

Run from the command line:

``` bash
$ composer require squizlabs/php_codesniffer
$ composer require wimg/php-compatibility
$ composer update picklewagon/picklewagon-coding-standards
$ ./vendor/bin/phpcs --config-set installed_paths vendor/picklewagon/php-coding-standards-pkg/,vendor/wimg/php-compatibility/
```

Verify package installation by running the following command:
``` bash
$ ./vendor/bin/phpcs -i
```

You should see the Picklewagon coding standard has now been installed.

## Usage

Create a file that your specific repository will use for it's coding standard.

Details can be found at the [PHP_CodeSniffer wiki](https://github.com/squizlabs/PHP_CodeSniffer/wiki).

Basically, you want to create a phpcs.xml file in the project root.

Here is an example of what will be in this file:

``` xml
<?xml version="1.0"?>
<ruleset name="PrinterInstaller">
    <description>The coding standard for the user microservice.</description>

    <!-- Include these folders -->
    <file>app</file>
    <file>bootstrap</file>
    <file>config</file>
    <file>database</file>
    <file>resources</file>
    <file>routes</file>
    <file>tests</file>

    <!-- Don't validate these files -->
    <exclude-pattern>*.blade.php</exclude-pattern>
    <exclude-pattern>bootstrap/autoload.php</exclude-pattern>
    <exclude-pattern>bootstrap/cache/services.php</exclude-pattern>

    <!-- Configuration -->
    <!-- Check for cross-version support for PHP 7.1 and higher. -->
    <config name="testVersion" value="7.1-" />

    <!-- Arguments -->
    <arg value="sp" />
    <arg name="extensions" value="php" />
    <arg name="report-json" value="build/reports/php/phpcs-code.json" />

    <!-- Include the Picklewagon coding standard. -->
    <rule ref="Picklewagon" />
</ruleset>
```

You'll need to customize it to the repo where you are installing it.

Run the command:

``` bash
$ ./vendor/bin/phpcs
```