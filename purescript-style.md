# PureScript style guide

This is a style guide for the language PureScript based on conventions used in
its core libraries. A style guide is a set of conventions about how to write
code for a project. It is easier to read a project's source code when it all has
a consistent style. It is easier to contribute code to a project when there is
no question as to how something should be written.

This style guide is licensed under the Creative Commons Zero license.

## Table of contents

- [1. Formatting](#1-formatting)
  * [1.1. Lines should be no longer than 80 characters](#11-lines-should-be-no-longer-than-80-characters)
  * [1.2. Do not use tabs](#12-do-not-use-tabs)
  * [1.3. Indent with 2 spaces](#13-indent-with-2-spaces)
  * [1.4. Separate top-level definitions with a blank line](#14-separate-top-level-definitions-with-a-blank-line)
  * [1.5. Surround operators with spaces](#15-surround-operators-with-spaces)
  * [1.6. No space after a lambda](#16-no-space-after-a-lambda)
  * [1.7. Lines must not have trailing spaces](#17-lines-must-not-have-trailing-spaces)
  * [1.8. Place each data type constructor on its own line](#18-place-each-data-type-constructor-on-its-own-line)
  * [1.9. Don't align types within record field declarations](#19-dont-align-types-within-record-field-declarations)
  * [1.10. Place each element in a long array on its own line](#110-place-each-element-in-a-long-array-on-its-own-line)
  * [1.11. Format export lists like arrays](#111-format-export-lists-like-arrays)
  * [1.12. Doubly indent nested record or array literals](#112-doubly-indent-nested-record-or-array-literals)
- [2. Naming](#2-naming)
  * [2.1. Use camel case for function names](#21-use-camel-case-for-function-names)
  * [2.2. Use upper camel case for type names](#22-use-upper-camel-case-for-type-names)
  * [2.3. Use all capitals for effect names](#23-use-all-capitals-for-effect-names)
  * [2.4. Do not use all capitals for acronyms](#24-do-not-use-all-capitals-for-acronyms)
  * [2.5. Use the singular for module names](#25-use-the-singular-for-module-names)

## 1. Formatting

### 1.1. Lines should be no longer than 80 characters

Lines should not be longer than **80 characters**.

#### Rationale

Long lines hinder readability by making the eye scan too far across the screen
or page. The column at which a line should be broken, however, is somewhat
arbitrary and chosen for historical reasons.

#### Exceptions

* URLs must not be split over multiple lines.

### 1.2. Do not use tabs

Source files must not contain tab characters; use spaces for indentation.

#### Rationale

Indentation has syntactic meaning in PureScript, meaning that tabs must be
interpreted as having a fixed width. However, editors can display tabs as any
width. Thus, code that looks visually correct can be syntactically incorrect,
especially if tabs have been mixed with spaces.

### 1.3. Indent with 2 spaces

Code blocks should be indented with **2 spaces**.

#### Examples

```purescript
catMaybes :: forall a. List (Maybe a) -> List a
catMaybes = case _ of
  Nil -> Nil
  Nothing : xs -> catMaybes xs
  Just x : xs -> x : catMaybes xs
```

### 1.4. Separate top-level definitions with a blank line

* There should be one blank line between top-level definitions.
* Do not place blank lines between type signatures and function definitions.
* One blank line may be placed between functions in type class instance
  declarations if the functions bodies are large.

### 1.5. Surround operators with spaces

Binary operators should be surrounded with a single space on either side.

### 1.6. No space after a lambda

Do not insert a space after the lambda symbol (backslash or `\`).

### 1.7. Lines must not have trailing spaces

Spaces must not appear at the end of any line of source code.

### 1.8. Place each data type constructor on its own line

Data types with multiple constructors should have each constructor placed on
its own line.

#### Examples

```purescript
data Color
  = Red
  | Blue
  | Green
```

### 1.9. Don't align types within record field declarations

Types within field declarations must not be aligned with one another; instead,
they should be flush against the field name.

#### Rationale

Alignment makes it harder when updating code. If a new record field is added
that is longer than the rest, the rest of the fields must be retabulated if the
formatting is to be maintained. Doing so is even worse, however, because the
resulting "diff" of the edit will indicate that several lines have changed, even
though they were only reformatted.

#### Examples

```purescript
data Rectangle = Rectangle
  { x :: Int
  , y :: Int
  , width :: Int
  , height :: Int
  }
```

### 1.10. Place each element in a long array on its own line

Each successive element in a long array should be placed on its own line, preceded by
a comma and a space. If an array literal doesn't fit on a single line then it should
be considered "long".

#### Rationale

This makes for more readable diffs when having to alter a long list.

#### Examples

```purescript
elements =
  [ div
  , h1
  , p
  , em
  , span
  , body
  ]
```

### 1.11. Format export lists like arrays

Export lists should be formatted like regular arrays above (except with
parentheses instead of square brackets.)

#### Examples

```purescript
module Data.Array
  ( Array
  , empty
  , singleton
  , sort
  ) where
```

### 1.12. Doubly indent nested record or array literals

When nesting record or array literals, the nested literal should be doubly indented (that is, indented 4 spaces.)

#### Examples

```purescript
{ bounds: 
    { x: 0
    , y: 0
    , width: 400
    , height: 300
    }
, color: RGB 128 0 0
, children:
    [ component1
    , component2
    , component3
    ]
}
```

## 2. Naming

### 2.1. Use camel case for function names

Functions must be written in camel case.

#### Examples

* `functionName`

#### Rationale

Syntactically, functions in PureScript *must* begin with a lower case letter.

### 2.2. Use upper camel case for type names

Data types and constructors must be written in upper camel case.

#### Examples

* `DataType`

#### Rationale

Syntactically, data types and constructors in PureScript *must* begin with a capital letter.

### 2.3. Use all capitals for effect names

Effects should be written in all capital letters.

#### Examples

* `CONSOLE`
* `EXCEPTION`
* `RANDOM`

### 2.4. Do not use all capitals for acronyms

Only the first letter of an acronym should be capitalized.

#### Examples

Write `HtmlParser` instead of `HTMLParser`.

#### Rationale

Names containing adjacent capitals that belong to separate words may hinder
readability.

#### Exceptions

Two letter acronyms should have both letters capitalized--for example, `ST`.

### 2.5. Use the singular for module names

Module names should be in the singular.

#### Examples

* Use `Data.String` instead of `Data.Strings`.
* Use `Data.Function` instead of `Data.Functions`.
