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

1. What does code confidence mean to me
2. What are coding conventions?
3. How do we install/run/configure PHPCS
4. How to increase code confidence using PHPCS

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

#  1# New projects

<!--
- Start from scratch, no code (yet)
- No architectural decisions have been made (yet)
- No frameworks or library’s chosen (yet)
- No bugs (yet)
- No end users (yet)
- Shopping list of new requirements
-->

---

# 2# Legacy projects

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

# 3# Migrations/rebuilds

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
- Gain visual feedback on what parts of code needs adjusting before merging.
- Spot potential future gotchas in coding conventions.
- Create a CI that reports code violations quickly and blocks the pipeline.
- Ensure the team follows the same set of rules.
- Move quickly whilst ensuring the team comply with a given set of agreed coding conventions.
-->
---

# Legacy projects

Quickly identify existing style violations whilst building up confidence with the code

<!--
- Be aware of known issues before deployment
- Clean up existing code smells
- Enforcing coding style requirements and checks during continual integration.
- Standardize the codebase
- Make the devs happy
-->

---

# Migrated projects

Ensure the migration from one code base to another is as smooth as possible.

<!--
- Ensure old code standards can be easily adapted.
- Remove old code styles (Either defined or implied)
- Minimise the amount of pollution that the old code base presents. 
-->

---

# How do we get there

---

# Add PHPCS to your toolbox

<!--
- PHPCS is just one of many tools
- Mess detection
- Static analysis
- Unit tests
-->

---

# #2
## What are Code Conventions

---

# From Wikipedia

"Coding conventions are a set of guidelines for a specific programming language that recommend programming style, practices, and methods for each aspect of a program written in that language. These conventions usually cover file organization, indentation, comments, declarations, statements, white space, naming conventions, programming practices, programming principles,"

---

# What does that mean?

- It forces new code to adhere to a given set of rules (sniffs).
- It makes the code easy to read.
- It removes ambiguity of which convention is allowed.
- It reduces noise and debate in pull requests.

---
# What's the point?

## We read code more than we write code

<!--
When we write code we read the surrounding code, the calling code and the architecture.
-->

---
# What's the point?

## Switching between conventions is a brain drain

<!--
It's like jumping between different languages or dialects. If you're having a conversation with someone and you don't understand them you may ask them to repeat themselves.  In code you will need to re-read the code.
-->

---
# What's the point?

## Code is complicated enough. Don't confuse the reader any more than needed.

<!--
Help the coders that come after you by following the conversions defined by the coders before you.
-->
---

# #3
## PHP_CodeSniffer has entered the chat

- [https://github.com/squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- Is free and open source

---

# Thank you

[@pfwd](https://twitter.com/pfwd])

