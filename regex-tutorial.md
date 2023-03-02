# Regex Tutorial - Matching an Email

Email's are used on any application that you use. You should always verify that the user's email input actually follows a valid email template. This tutorial will go through how you can easily check that a given email is actually a correct email address.

## Summary

We will be going through the following regex for matching an email.
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

A regex is considered a literal, so the pattern must be wrapped in slash characters (`/`).

### Anchors

There are two anchor tags, `^` and `$`. The `^` anchor signifies a string that begins with the characters that follow. The `$` anchor signifies that end of the string.

### Quantifiers

Quantifiers set the limits of the string that your regex matches. Frequently, they are the minimum or maximum number of characters that your regex is looking for.

* `*` Zero or more
* `+` One or more
* `?` Zero or one
* `{}` Curly brackets can provide more options for limits
    * `{ n }` Exactly `n` number of times
    * `{ n, }` `n` or more
    * `{ n, x }` Minimum of `n` times and maximum of `x` times

Back to our email matching regular expression
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```
You can see that we use the `+`, and the `{ x, n }` quantifiers to designate the maximum and minimum of the groupings.

### OR Operator

In order to ensure that we can have options within a grouping, we will use the OR operator, (`|`).

For example, if you had the regular expression
```
(abc)
```
Then it would look for an exact match of `abc`. Whereas if we introduce the OR operator as follows
```
(a|b|c)
```
Then `a`, `b`, `c`, `ab`, `bc`, `ac`, or `abc` are all valid matches.

### Character Classes

A character class in a regex defines a set of characters. Here are some of the common character classes.
* `.` Matches any character except a newline character (`\n`)
* `\d` Matches any numeral digit. This is equivalent to `[0-9]`
* `\w` Matches any alphanumeric character. This is equivalent to `[A-Za-z0-9_]`
* `\s` Matches any whitespace character, including tabs and line breaks

Any of these character classes can be changed to perform the inverse match by capitalizing the letter character. For example, `\D` matches any non-digit character.

### Flags

Flags are the one exception that can be placed outside of the slash characters which determine the beginning and end of a regular expresion. Flags create additional functionality or limits for the regex. Below are the three most common flags that you will use.
* `g` Global search: the regex should be tested against all possible matches in a string
* `i` Case-insensituve search: case should be ignored while attempting to match a string
* `m` Multi-line search: a multi-line input string should be treated as multiple lines

### Grouping and Capturing

There are three main parts of an email that we can break out. The first part is the user created part. This part is typically someones name while including a period, hyphen, or underscore to separate the user's first name and last name. The second part is the second-level domain name and lastly the top-level domain, i.e. `com`, `edu`, `etc`.

In order to check these independently, we will create groupings for each part. To create a grouping we use `()`.

If you take a look at our email matching regular expression
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```
You will notice that we have three distinct groupings which we talked about above.

### Bracket Expressions

Anything inside a set of square brackets `[]` show the options of the characters that we want to match against. You will notice that we do not need the OR operator within a bracket expression. This pattern is know as a bracket expression. For example, `[0-9]` will look for a string that contains any single number, i.e. the numbers 0 through 9. Alternatively, the pattern `[a-zA-Z]` will look for a string that contains any letter, either upper case or lower case.

As you can see in our regex for matching an email there are a few bracket expressions.
* `[a-z0-9_\.-]` This bracket expression says that any lowercase letter, any number between 0 and 9, any underscore, any period, or any hyphen is a valid character
* `[\da-z\.-]` This bracket expression says that any digit, lowercase letter, period, or hyphen is a valid character.
* `[a-z\.]` This bracket expression says that any lowercase letter or period is a valid character.

### Greedy and Lazy Match

Greedy match means that you can match as many characters as possible. For example, `/a.*a/` would match any character that comes between two letter `a`'s. 

Lazy match makes it so that it matches as few characters as possible. By adding a question mark to the greedy match, you can make the previous regex a lazy match instead, `/a.*?a/`.

Take the following string as an example input string, `greedy match can be dangerous`. Greedy match would match between, `atch can be da` because that is between the first and last `a`. Whereas lazy match would match between, `atch ca` because it matches between the first set of `a`'s.

### Boundaries

Boundry matchers are useful in order to find a particular word if it appears at the beginning or end of a word.
* `\b` Word boundary, matches the end of a word
```
/[a-z]\b/g
```
The above regex would match the last letter of each word in a given string.
* `\B` Non-word Boundary, matches any characters at the beginning of a word
```
/[a-z]*\B/g
```
The above regex would match the whole beginning of a word until the last letter.

### Back-references

Back references identify a previously matched group and looks for the same text again. 

### Look-ahead and Look-behind

* `foo(?=bar)` Lookahead, asserts that the given subpattern can be matched without consuming the characters
`foobar foobaz` would match just the `foo` before `foobar`.

* `(?<=foo)bar` Lookbehind, ensures that the given pattern will match, ending at the curent position in the expression
`foobar fuubar` would match just the `bar` after `foobar`.

## Author

Amanda Cappleman

Software Engineer

[GitHub Profile](https://www.github.com/acappleman)
