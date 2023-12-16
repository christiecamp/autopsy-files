![header](./blood-stained/header.png)

[![Markdown Badge](https://img.shields.io/badge/markdown-teal.svg?&logo=Markdown&logoColor=white)](https://canva.com/)
[![Canva Badge](https://img.shields.io/badge/canva-tan.svg?&logo=Canva&logoColor=white)](https://canva.com/)

[![View Badge](https://img.shields.io/badge/view-darkmode-maroon.svg?&logo=Github&logoColor=white)](https://canva.com/)

### ![table-of-contents](./blood-stained/toc.png)

  - [OVERVIEW](#overview)
  - [REGEX COMPONENTS](#regex)
    - [*anchors*](#anchors)
    - [*quantifiers*](#quantifiers)
    - [*grouping constructs*](#grouping)
    - [*bracket expressions*](#bracket)
    - [*character classes*](#classes)
    - [*the or operator*](#operator)
    - [*flags*](#flags)
    - [*character escapes*](#escapes)
  - [SOURCES](#sources)
  - [CONNECT](#connect)

![overview](./blood-stained/1.png)

**AUTOPSY FILES** is here to dissect a variety of *REGEX expressions* to help you understand, and breakdown, each component.
*REGEX expressions* - or [Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions) - is an exceptionally useful sequence of characters that specifies a match pattern in text. 

#
> the expression will accept a certain set a strings that match the pattern, and reject the rest.
#

### ![regex](./blood-stained/2.png)

There are a variety of parts to every *REGEX expression*. We will be covering each portion in detail for the expressions below:

##### *REGEX expression* that checks for hex values (not case-sensitive)
```javascript
const regex = /^#?([a-f0-9]{6}|[a-f0-9]{3})$/i;
```
##### *REGEX expression* that checks for all character values, including defined special characters
```javascript
const regex = /^[\w!@#$%\^&*)(+=./-]*$/;
```
##### *REGEX expression* that checks the validity of a phone number
```javascript
const regex = /^(?:\d{3}|\(\d{3}\))([-.])\d{3}\1\d{4}$/;
```

#### ![anchors](./blood-stained/5.png)

Anchors are used at the start and end of a *REGEX expression* string, and describe the position of the expression in a line of text. Anchors are comprised of the **caret `^`** and **dollar `$`** symbol.

>The `^` symbol designates match start & the `$` symbol designates match end.

Each *REGEX expression* below is defined by both the **caret** `^` and **dollar** `$` symbol, stating the beginning and end of each match string.

##### hex value
```javascript
/  ^  #?([a-f0-9]{6}|[a-f0-9]{3})  $  /i
```
##### character value
```javascript
/  ^  [\w!@#$%\^&*)(+=./-]*  $  /
```
##### phone number
```javascript
/  ^  (?:\d{3}|\(\d{3}\))([-.])\d{3}\1\d{4}  $  /
```

###### We inspect the innards of each *REGEX expression* in the coming sections!

#### ![quantifiers](./blood-stained/6.png)

**Quantifiers** are used within the *REGEX expression* to dictate how many characters are expected within the string of text, and details how many instances the character(s) must be present for match.

* The optional symbol `?` informs that the proceeding character may, or may not, be present in the string for match.
* The curly braces `{..}` orders a match of the proceeding character(s) for as many times defined inside the bracket.
* The asterick symbol `*` orders a match of the preceding character(s) for 0 or more times (until infinity & beyond). This symbol is considered a *repeater*.

##### hex value *quantifiers* include: `?`, `{6}`, `{3}`

 * `?` :: the component proceeding can match 0 to 1 times - ` ([a-f0-9]{6}|[a-f0-9]{3})`.
 * `{6}` & `{3}` :: the component preceeding these quantifiers should match - either 6 characters (**Hex Triplet Format**) or 3 (**Shorthand Hex Format**).
```javascript
/^#  ?  ([a-f0-9]  {6}  |[a-f0-9]  {3}  )$/i
```

##### character value *quantifier*: `*`
```javascript
/^[\w!@#$%\^&*)(+=./-]  *  $/
```
##### phone number *quantifiers* include: `?`, `{3}`, `{4}`
```javascript
/^(  ?  :\d {3} |\(\d {3} \))([-.])\d {3} \1\d  {4}  $/
```

#### ![grouping](./blood-stained/7.png)

**Grouping Constructs**, or *subexpressions*, are used to break up the string into sections to fulfill different requirements. *Subexpressions* are segements inside parenthesis `()`, and have two primary categories: **capturing** and **non-capturing**.

* **capturing** *subexpressions* capture the match character sequence for possible re-use.
* **non-capturing** *subexpressions* do not capture the match character sequence. This can be done by adding `?:` at the beginning of the expression string inside the `()`.


##### hex value *subexpression*: `([a-f0-9]{6}|[a-f0-9]{3})`
```javascript
/^#?  ([a-f0-9]{6}|[a-f0-9]{3})  $/i
```
##### character value does not contain a *subexpression*
```markdown
> > > > >           > > > > >          > > > > > 
```
##### phone number *subexpressions* include: `(?:\d{3}|\(\d{3}\))` & `([-.])`
```javascript
/^  (?:\d{3}|\(\d{3}\))  ([-.])  \d{3}\1\d{4}$/
```

#### ![bracket](./blood-stained/8.png)

**Bracket Expressions**, or *positive character groups*, are used to signify a range of characters needed to match. These expressions reside within square brackets `[]`.

* bracket expressions can be turned into *negative character groups* by adding the `^` symbol to the beginning of the expression string inside the `[]`.

##### hex value *bracket expressions*: `[a-f0-9]` & `[a-f0-9]`
```javascript
/^#?(  [a-f0-9]  {6}|  [a-f0-9]  {3})$/i
```
##### character value *bracket expressions*: `[\w!@#$%\^&*)(+=./-]`
```javascript
/^  [\w!@#$%\^&*) (+=./-]  *$/
```
##### phone number *bracket expression*: `[-.]`
```javascript
/^   (?:\d{3}|\(\d{3}\))(  [-.]  )\d{3}\1\d{4}   $/
```

#### ![classes](./blood-stained/9.png)

**Character Classes** define a set of characters, within a string, that fulfils a match to the *REGEX expression*.

* characters within `[...]` are accepted as a match.
* characters within *range expression* `[.-.]` are accepted as a match.
* the `\d` symbol matches any arabic numeral digit - is the equivalent to the **range expression** `[0-9]`.
* if the `^` is included within the expression string, then the characters are not a match - ie `[^0-9]` means .

##### hex value *character classes*: `[a-f0-9]` & `[a-f0-9]`
```javascript
/^#?(  [a-f0-9]  {6}|  [a-f0-9]  {3})$/i
```
##### character value *character classes*: `[\w!@#$%\^&*)(+=./-] `
```javascript
/^  [\w!@#$%\^&*)(+=./-]  *$/
```
##### phone number *character classes*: `[-.]` & `\d`
```javascript
/^(?: \d {3}|\( \d {3}\))( [-.] ) \d {3}\1 \d {4}$/
```

#### ![operator](./blood-stained/10.png)

The **OR operator** matches any one element in the string proceding or succeeding the vertical bar `|`.

##### hex value *or operator* `|` seperates two *bracket expressions*
```javascript
/^#?([a-f0-9]{6}  |  [a-f0-9]{3})$/i
```
##### character value does not contain an *OR operator*
```markdown
> > > > > > > > > > > > > > > > > > > > > > > >
```
##### phone number does not contain an *OR operator*
```markdown
> > > > > > > > > > > > > > > > > > > > > > > >
```

#### ![flags](./blood-stained/11.png)

**Flags** are used at the end of the *REGEX expression* to define additional functionality or limits for match. A typical expression is wrapped in slash `/` symbols, which inform the start and end of the `/regex string/`. There are 6 optional flags, but the three listed below are most frequently used:

* `g` :: **global search** - expression tested against all possible matches in a string.
* `i` :: **case-insensitive search** - case should be ignored while attempting a match.
* `m` :: **multi-line search** - multi-line input treated as multiple lines

##### hex value *flag*: `i`
```javascript
/^#?([a-f0-9]{6}|[a-f0-9]{3})$/  i
```
##### character value does not contain a *flag*
```markdown
> > > > >           > > > > >          > > > > > 
```
##### phone number does not contain a *flag*
```markdown
> > > > >           > > > > >          > > > > > 
```

#### ![escapes](./blood-stained/12.png)

**Character Escapes** are used to *escape* special characters using the backslash symbol (or escape symbol) `\`, making it literal and considered for match. 

> all special characters, including the backslash `\`, lose their significance inside *bracket expressions* `[]`.


##### hex value does not contain an *escape character*
```markdown
> > > > >           > > > > >          > > > > > 
```
##### character value does not contain an *escape character*
```markdown
> > > > >           > > > > >          > > > > > 
```
##### phone number *escape character* `\` 
```javascript
/^(?:\d{3}| \ (\d{3} \ ))([-.])\d{3} \ 1 \d{4}$/
```

#
### ![sources](./blood-stained/3.png)

1. [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions)
2. [Regular-Expressions](https://www.regular-expressions.info/)
3. [Geeks for Geeks](https://www.geeksforgeeks.org/write-regular-expressions/)
4. [Full-Stack Blog](https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial)
5. [Wikipedia](https://en.wikipedia.org/wiki/Regular_expression)

### ![connect](./blood-stained/4.png)

##### `leave a comment!`

[![gist](https://img.shields.io/badge/gist-christiecamp-salmon.svg?&logo=Github&logoColor=white)](https://gist.github.com/christiecamp)