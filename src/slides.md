---
theme: uncover
class:
- lead
- invert
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
## What does code confidence mean to me

---

## There are three types of projects that every programmer deals with during their career

---

#  1# New / green field projects

<!--
- Start from scratch, no code (yet)
- No architectural decisions have been made (yet)
- No frameworks or library’s chosen (yet)
- No bugs (yet)
- No end users (yet)
- Shopping list of new requirements
-->

---

# 2# Legacy / brown field projects

<!--
- It could be a spaghetti code base
- It could have mixture of frameworks and library's
- The code could be out of date
- It could be using an older version of PHP
- It could have incoming change requests
- It could have poor technical documentation
- There might be 0 tests
- There could be lots of known bugs
- There could be lots of unknown bugs
- There could be many end users. Some might be complaining
- There could be performance, security, and data integrity issues
- You could have a low confidence that an upgrading or improving something will work
-->

---

# 3# Migrations / rebuilds

<!--
- Data integrity could be poor
- Existing user base
- Downtime issues
- There could be many reasons why a migration is needed
- Workarounds
-->

---

# The dream

---

# New projects

Start clean, continue clean whilst building up confidence with the code

<!--
- Be aware of known style violations before the first deployment
- Gain visual feedback on what parts of code need adjusting before the first deployment.
- Spot potential future gotchas in coding conventions.
- Create a CI that reports code violations quickly and blocks the pipeline.
- Ensure the team follows the same set of rules.
- Move quickly whilst ensuring the team comply with a given set of agreed coding conventions.
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
- Unifi the coding conventions.
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
- Has hundreds rules
- Only checks PHP

---

# #2
## What are Code Conventions

---

# From Wikipedia

"Coding conventions are a set of guidelines for a specific programming language that recommend programming style, practices, and methods for each aspect of a program written in that language. These conventions usually cover file organization, indentation, comments, declarations, statements, white space, naming conventions, programming practices, programming principles,"

---

# What does that mean?

- It forces code to adhere to a given set of rules (sniffs).
- It makes the code easier to read.
- It removes ambiguity of which convention is allowed.
- It reduces noise and debate in pull requests.

---
# What's the point?

## We read code more than we write code

## Switching between conventions is a brain drain

<!--
When we write code we read the surrounding code, the calling code and the architecture.
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

# The fix

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


<!--
- Updating the return type to allow for nullable values (:?string)
-->

--- 

# What's a sniff?


---

# Thank you

[@pfwd](https://twitter.com/pfwd])

