# PureScript style guide

This is a style guide for the language PureScript based on conventions used in
its core libraries. A style guide is a set of conventions about how to write
code for a project. It is easier to read a project's source code when it all has
a consistent style. It is easier to contribute code to a project when there is
no question as to how something should be formatted.

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
  * [1.10. Each element in a list on its own line](#110-each-element-in-a-list-on-its-own-line)
  * [1.11. Format export lists like lists](#111-format-export-lists-like-lists)

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

Remove any whitespace at the end of each line of source code.

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

### 1.10. Each element in a list on its own line

Each successive element in a list should be placed on its own line, preceded by
a comma and a space.

#### Examples

```purescript
elements =
  [ div
  , h1
  , p
  ]
```

### 1.11. Format export lists like lists

Export lists should be formatted like regular lists above (except with
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
