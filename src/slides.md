---
theme: uncover
marp: true
paginate: true
class:
  size: 16:9
  footer: "Peter Fisher BSc MBCS [howtocodewell.net](https://howtocodewell.net) [@howToCodeWell](https://twitter.com/howtocodewell) [@pfwd](https://twitter.com/pfwd)"
---

# Code with confidence using PHPCS

---

1. What does code confidence mean to me?
2. What are coding conventions?
3. How do we install/run/configure PHPCS?
4. How to increase code confidence using PHPCS?

---

# $ whoami = Peter Fisher

- PHP Contractor from the UK
- Playing with PHP > 20 years
- Host of the How To Code Well
  -- Podcast [howtocodewell.fm](https://howtocodewell.fm)
  -- YouTube channel [youtube.com/howtocodewell](https://youtube.com/howtocdewell)
  -- Twitch live coders team [howtocodewell.net/live](https://howtocodewell.net/live)
  -- Tutorials and courses [howtocodewell.net](https://howtocodewell.net)

---

# Get the slides

[http://peterfisher.me.uk/slides/code-with-confidence-using-phpcs.html](http://peterfisher.me.uk/slides/code-with-confidence-using-phpcs.html)

---

# #1
## What does code confidence mean to me?

---

## There are three types of projects that every programmer deals with during their career

---

#  1# New / green field projects

<!--
- Start from scratch, no code (yet)
- No architectural decisions have been made (yet)
- No frameworks or library’s chosen (yet)
- No Code styles have been chosen
- List of requirements and timescales

-->

---

# 2# Legacy / brown field projects

<!--
- It could have a mixture of code styles
- It could have mixture of frameworks and library's
- The code could be out of date
- It could be using an older version of PHP
- Team members who advocated a coding style may no longer be on the team
- Low documentation
-->

---

# 3# Migrations / rebuilds

<!--
- Migrating from one code style to another
- Migrating from one framework to another
- Migrating from versions which us different code conventions
-->

---

# The dream

---

# New projects

Start clean, continue clean whilst building up confidence with the codebase

<!--
- Be aware of known style violations before the first deployment
- Gain visual feedback on what parts of code need adjusting before the first deployment.
- Spot potential future gotchas in coding conventions.
- Create a CI that reports code violations quickly and blocks the pipeline from going forward.
- Ensure the team follows the same set of rules.
- Move quickly whilst ensuring the team comply with a given set of agreed coding conventions.
- Create a space for discussions about code conventions
-->
---

# Legacy projects

Quickly identify existing style violations whilst building up confidence with the code

<!--
- Be aware of known issues and violations in the project.
- Prioritise existing code smells
- Reduce team arguments on coding conventions. 
- Make it easier for future developers to know which conventions are required.
-->

---

# Migrated projects

Ensure the migration from one code base to another is as smooth as possible.

<!--
- Ensure old code standards can be easily adapted.
- Remove old code styles (Either defined or implied)
- Minimise the amount of cross pollination of styles.
-->

---

# How do we get there

---

# Add PHPCS to your toolbox

<!--
- PHPCS is just one of many tools
- Mess detection
- Compatibility checks
- Static analysis
- Tests (Unit/Integration/Acceptance)
-->
---

# What about PHP Coding Style Fixer (PHP CS)

- Fixer first approach (Great for automation)
- Supported by Symfony
- Different output style
- Cannot ignore individual lines of code
- Configured by PHP
- Has hundreds of rules
- Only checks PHP

---

# #2
## What are Code Conventions?

---

# From Wikipedia

"Coding conventions are a set of guidelines for a specific programming language that recommend programming style, practices, and methods for each aspect of a program written in that language. These conventions usually cover file organization, indentation, comments, declarations, statements, white space, naming conventions, programming practices, programming principles,"

---

# What does that mean?
<!--
- It forces code to adhere to a given set of rules (sniffs).
- It makes the code easier to read.
- It removes ambiguity of which convention is allowed.
- It reduces noise and debate in pull requests.
-->
---

# What's the point?

<!--
We read code more than we write code.

When we write code we read the surrounding code, the calling code and the architecture.

Switching between conventions is a brain drain.

-->

---

# #3
## PHP_CodeSniffer has entered the chat

- [https://github.com/squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- PHP >=5.4.0
- Uses XML for config
- Multiple reporting outputs
---

# Install via Composer

# Composer

```bash
$ composer global require "squizlabs/php_codesniffer=*"
```

---

# Other ways to install

- Pear
- Curl
- Wget
- Git clone

See [github.com/squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)

---

# Two tools

- phpcs
- phpcbf

---

# What is phpcs?

- Tokenizer for PHP, JavaScript and CSS

---

# What is phpcbf?

- Automatic fixer

---

# Your first run

```bash
$ phpcs ~/path/to/file.php
```

```bash
$ phpcs ~/path/to/directory
```

---

# When things go well

```bash
root@3aff108bdba0:/var/www/html# bin/phpcs src/MyController.php
root@3aff108bdba0:/var/www/html#
```

---

# Catching errors
```
root@3aff108bdba0:/var/www/html# bin/phpcs src/Controller/ConnectController.php

FILE: src/Controller/ConnectController.php
-----------------------------------------------------------------------
FOUND 1 ERROR AFFECTING 1 LINE
-----------------------------------------------------------------------
 24 | ERROR | [x] Expected 0 spaces after opening parenthesis; 1 found
-----------------------------------------------------------------------
PHPCBF CAN FIX THE 1 MARKED SNIFF VIOLATIONS AUTOMATICALLY
-----------------------------------------------------------------------

Time: 596ms; Memory: 10MB
```

---

# Fixing the Sniff Violation

```bash
root@3aff108bdba0:/var/www/html# bin/phpcbf src/Controller/ConnectController.php

PHPCBF RESULT SUMMARY
----------------------------------------------------------------------
FILE                                                  FIXED  REMAINING
----------------------------------------------------------------------
src/Controller/ConnectController.php                  1      0
----------------------------------------------------------------------
A TOTAL OF 1 ERROR WERE FIXED IN 1 FILE
----------------------------------------------------------------------

Time: 611ms; Memory: 10MB
```

--- 

# What's a sniff?

- A sniff is a file checks one part of the coding standard.
- A coding standard is a collection of sniffs.
- A coding standard is a directory and a ruleset.xml
- The default standard is PEAR
---

# What's a ruleset
- XML file of that configures the coding standard
- Can define include and exclude rules
- Can include output rules
- Can include sniffs from other rulesets

[More info](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Annotated-Ruleset)

---
# Creating a ruleset

`./custom_ruleset.xml`

`phpcs --standard=/path/to/custom_ruleset.xml /path/to/file.php`

---

# Add a rule

```xml
<?xml version="1.0" ?>
<ruleset name="MyProject">
  <rule ref="PSR1" />
</ruleset>
```
---
# Adding other rules

```xml
<?xml version="1.0" ?>
<ruleset name="MyProject">
  <rule ref="PSR1" />
  <rule ref="PSR2" />
</ruleset>
```
---
# Rule parts

```
Standard.Subset.Sniff.ErrorCode
```

```
PSR2.Classes.ClassDeclaration.OpenBraceNewLine
```
---
# Excluding parts of a rule

```xml
<rule ref="PSR2">
    <exclude name="PSR2.Classes.ClassDeclaration.OpenBraceNewLine" />
</rule>
```
---

# Overriding parts of a rule
```xml

<rule ref="Generic.Files.LineLength">
  <properties>
    <property name="lineLimit" value="90"/>
    <property name="absoluteLineLimit" value="100"/>
  </properties>
</rule>
```
<!--
Includes LineLength sniff but changes settings so the sniff will show warnings for any line longer
than 90 chars and errors for any line longer than 100 chars.
-->

---
# Messaging
```xml
<exclude-pattern>*/vendor/*</exclude-pattern>
<rule ref="Generic.Files.LineLength">
    <message>The line is too long</message>
  <properties>
    <!-- default line limit is 120 -->
    <property name="lineLimit" value="170"/>
  </properties>
</rule>
```
<!--
Excludes the vendor directory
-->
---

# Excluding patterns from all rules
```xml
<exclude-pattern>*/vendor/*</exclude-pattern>
<rule ref="PSR2">
    <exclude name="PSR2.Classes.ClassDeclaration.OpenBraceNewLine" />
</rule>
<rule ref="Generic.Files.LineLength">
  <properties>
    <!-- default line limit is 120 -->
    <property name="lineLimit" value="170"/>
  </properties>
</rule>
```
<!--
Excludes the vendor directory
-->
---
# What standards are installed
```
root@3aff108bdba0:/var/www/html# bin/phpcs -i
The installed coding standards are MySource, PEAR, PSR1, PSR2, PSR12, Squiz, Zend, html and Security
```

---
# What Rules are installed
```
root@3aff108bdba0:/var/www/html# bin/phpcs --standard=MySource --generator=text
```

```
---------------------------------------------------
| MYSOURCE CODING STANDARD: PROPERTY DECLARATIONS |
---------------------------------------------------

Property names should not be prefixed with an underscore to indicate visibility.  Visibility should
be used to declare properties rather than the var keyword.  Only one property should be declared
within a statement.  The static declaration must come after the visibility declaration.

----------------------------------------- CODE COMPARISON ------------------------------------------
| Valid: Correct property naming.                | Invalid: An underscore prefix used to indicate  |
|                                                | visibility.                                     |
----------------------------------------------------------------------------------------------------
| class Foo                                      | class Foo                                       |
| {                                              | {                                               |
|     private $bar;                              |     private $_bar;                              |
| }                                              | }                                               |
----------------------------------------------------------------------------------------------------

```
<!--
Generator could be markdown
-->
---
# Configuration options

```
bin/phpcs -p -v --extensions=php,inc -d memory_limit=1024 --parallel=8 src/Controller
```

```
Registering sniffs in the  standard... DONE (43 sniffs registered)
Creating file list... DONE (30 files in queue)
Loading cache... DONE (30 files in cache)
Changing into directory src/Controller/CMS
Processing CourseController.php [loaded from cache]... DONE in 2ms (0 errors, 0 warnings)
```

<!--
-p = Show progress of the run
-v = Print processed files
-d = Set the [key] php.ini value to [value] or [true] if value is omitted
--extensions = A comma separated list of file extensions to check
--parallel = Amount of processes to run

-->
---
```
bin/phpcs -p -v --extensions=php,inc -d memory_limit=1024M --parallel=8 src/Controller
```

```xml
<arg value="pv"/>
<arg name="extensions" value="php,inc" />
<ini name="memory_limit" value="1024M" />
<arg name="parallel" value="8" />
<file>src/Controller</file>
```

---
# Ignoring files
```php
<?php
// phpcs:ignoreFile
$xmlPackage = new XMLPackage;
$xmlPackage['error_code'] = get_default_error_code_value();
$xmlPackage->send();
```
---
# Ignoring parts of a file

```php
$xmlPackage = new XMLPackage;
// phpcs:disable
$xmlPackage['error_code'] = get_default_error_code_value();
$xmlPackage->send();
// phpcs:enable
```
---

# Ignoring sniffs
```php
// phpcs:disable Generic.Commenting.Todo.Found
$xmlPackage = new XMLPackage;
$xmlPackage['error_code'] = get_default_error_code_value();
// TODO: Add an error message here.
$xmlPackage->send();
// phpcs:enable
```

---
# Ignoring lines 1/3
```php
// phpcs:ignore
$foo = [1,2,3];
bar($foo, false);
```
<!-- Example shows PHPCS ignoring line below. -->
---
# Ignoring lines 1/2
```php
$foo = [1,2,3]; // phpcs:ignore
bar($foo, false);
```
<!-- Example shows PHPCS ignoring the current line. -->
---
# Ignoring lines 1/3
```php
// phpcs:ignore Squiz.Arrays.ArrayDeclaration.SingleLineNotAllowed
$foo = [1,2,3];
bar($foo, false);
```
<!-- Example shows PHPCS ignoring sniff -->
---

# #4
## How to increase code confidence using PHPCS

--- 

# Recommendations for any project

---
# Test order is important

PHPCS -> PHPStan -> PHPUnit

<!-- Run PHPCS first as this will require automatic alterations to the code -->
---

# One command to rule them all
```bash
$ make tests
```
```bash
$ composer test
```
---
# Use Continual Integration (CI)
<!--
- Enforce that no code can be merged into the main branches unless the CI fully passes
-->
---
# Only test your code
<!--
- Don't check code that you haven't written.  
- Don't include the vendor
- Ignore any code that is automatically generated like migrations
-->
---

# Recommendations for new projects

<!--
- Do not ignore lines, files or disable sniffs unless you really have to.
- Document why you are ignoring things.
-->

---

# Recommendations for legacy projects

<!--
- Choose to use PHPCS or PHP CS 
- Investigate which conventions are currently in use
- Get an agreement with the team as to which conventions to use/drop
- If anything needs to be ignored then write a ticket and add the ticket reference into the comment.
-->
---

# Example

```php
// phpcs:ignore Squiz.Arrays.ArrayDeclaration.SingleLineNotAllowed [PORT-123]
$foo = [1,2,3];
bar($foo, false);
```

---

# 3 Confidence levels for legacy projects

---

# 1) PHPCS is already in use. 

Any ignored files or lines have been documented with a related ticket in the backlog

- High confidence level

---
# 2) PHPCS is installed
However lots of files/lines/sniffs have been ignored with no explanation

- Low confidence level

---
# How do you improve a legacy project?
<!--
- Collate all the ignored files, lines and have a meeting with the team to discuss a way forward.
- Can the ignored items be fixed and the rule be included
- Start very slowly with goal to get better linter over time

-->
---

# 3) PHPCS is not installed

- Very low confidence level

How do you install PHPCS on a legacy project?

---
1. Get the buy in of the team
2. Choose the standards and run PHPCBF over the code base to fix quick wins
3. Start to introduce new sniffs and re run PHPCBF over the codebase each time
5. Put the code formatting changes in a separate branch/pr
6. Rinse and repeat

---

# PHPCS and Security

```xml
<rule ref="Security.BadFunctions.Asserts"/>
<rule ref="Security.BadFunctions.Backticks"/>
<rule ref="Security.BadFunctions.CallbackFunctions"/>
<rule ref="Security.BadFunctions.CryptoFunctions"/>
<rule ref="Security.BadFunctions.EasyRFI"/>
<rule ref="Security.BadFunctions.EasyXSS"/>
<rule ref="Security.CVE.20132110"/>
<rule ref="Security.CVE.20134113"/>
```

[https://github.com/FloeDesignTechnologies/phpcs-security-audit](https://github.com/FloeDesignTechnologies/phpcs-security-audit)

---

# PHPCS and PHP Compatibility

```xml
<rule ref="PHPCompatibility"/>
```

```bash
phpcs -p ./src --standard=vendor/phpcompatibility/php-compatibility/PHPCompatibility --runtime-set testVersion 8.0
```

[https://github.com/PHPCompatibility/PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility)

---

# Thank you

[@pfwd](https://twitter.com/pfwd])

