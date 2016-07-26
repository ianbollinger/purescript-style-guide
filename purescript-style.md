# PureScript style guide

This is a style guide for the language [PureScript](http://www.purescript.org/) based on conventions used in
its core libraries. A style guide is a set of conventions about how to write
code for a project. It is easier to read a project's source code when it all has
a consistent style. It is easier to contribute code to a project when there is
no question as to how something should be written.

This style guide is licensed under the [Creative Commons Zero license](https://creativecommons.org/publicdomain/zero/1.0/legalcode).

## Table of contents

- [1. General formatting](#1-general-formatting)
  * [1.1. Lines should be no longer than 80 characters](#11-lines-should-be-no-longer-than-80-characters)
  * [1.2. Do not use tabs](#12-do-not-use-tabs)
  * [1.3. Indent with 2 spaces](#13-indent-with-2-spaces)
  * [1.4. Separate top-level definitions with a blank line](#14-separate-top-level-definitions-with-a-blank-line)
  * [1.5. Surround operators with spaces](#15-surround-operators-with-spaces)
  * [1.6. No space after a lambda](#16-no-space-after-a-lambda)
  * [1.7. Lines must not have trailing spaces](#17-lines-must-not-have-trailing-spaces)
  * [1.8. Place each data type constructor on its own line](#18-place-each-data-type-constructor-on-its-own-line)
  * [1.9. Don't align code](#19-dont-align-code)
  * [1.10. Place each element in a long array on its own line](#110-place-each-element-in-a-long-array-on-its-own-line)
  * [1.11. Precede items in arrays, records, and import lists with commas](#111-precede-items-in-arrays-records-and-import-lists-with-commas)
  * [1.12. Format export lists like arrays](#112-format-export-lists-like-arrays)
  * [1.13. Doubly indent nested record or array literals](#113-doubly-indent-nested-record-or-array-literals)
  * [1.14. Prefer case expressions over equational pattern matching](#114-prefer-case-expressions-over-equational-pattern-matching)
- [2. Naming](#2-naming)
  * [2.1. Use camel case for function names](#21-use-camel-case-for-function-names)
  * [2.2. Use upper camel case for type names](#22-use-upper-camel-case-for-type-names)
  * [2.3. Use all capitals for effect names](#23-use-all-capitals-for-effect-names)
  * [2.4. Do not use all capitals for acronyms](#24-do-not-use-all-capitals-for-acronyms)
  * [2.5. Use the singular for module names](#25-use-the-singular-for-module-names)
- [3. Imports](#3-imports)
  * [3.1. Group imported modules by origin](#31-group-imported-modules-by-origin)
  * [3.2. Sort imports alphabetically](#32-sort-imports-alphabetically)
  * [3.3. Qualify imports or explicitly list imported symbols](#33-qualify-imports-or-explicitly-list-imported-symbols)
- [4. Comments](#4-comments)
  * [4.1. Use Markdown syntax in documentation comments](#41-use-markdown-syntax-in-documentation-comments)
  * [4.2. Comment every exported definition](#42-comment-every-exported-definition)
- [5. Miscellaneous](#3-miscellaneous)
  * [5.1. Avoid over-using point-free style](#51-avoid-over-using-point-free-style)
  * [5.2. Code must be warning-free](#52-code-must-be-warning-free)

## 1. General formatting

### 1.1. Lines should be no longer than 80 characters

Lines should not be longer than **80 characters**.

#### Rationale

Long lines hinder readability by making the eye scan too far across the screen
or page. The column at which a line should be broken, however, is somewhat
arbitrary and chosen for historical reasons.

#### Exceptions

URLs must not be split over multiple lines.

### 1.2. Do not use tabs

Source files must not contain tab characters; use spaces for indentation.

#### Rationale

Indentation has syntactic meaning in PureScript, meaning that tabs must be
interpreted as having a fixed width. However, editors can display tabs as any
width. Thus, code that looks visually correct can be syntactically incorrect,
especially if tabs have been mixed with spaces.

### 1.3. Indent with 2 spaces

Code blocks should be indented with **2 spaces**.

#### Exceptions

* [Nested record and array literals should be indented **4 spaces**.](#113-doubly-indent-nested-record-or-array-literals)
* `let` bindings should be indented **4 spaces** as well.

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

### 1.9. Don't align code

Do not align code. Types within field declarations must not be aligned with one
another; instead, they should be flush against the field name. Additionally,
patterns and arrows in pattern match cases should not be aligned with one
another.

#### Rationale

Alignment makes it harder when updating code. For instance, if a new record field
is added that is longer than the rest, the rest of the fields must be retabulated
if the formatting is to be maintained. Doing so is even worse, however, because
the resulting "diff" of the edit will indicate that several lines have changed,
even though they were only reformatted.

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

Each successive element in a long array should be placed on its own line.
If an array literal doesn't fit on a single line then it should be
considered "long".

#### Rationale

This makes for more readable diffs when having to alter a long array.

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

### 1.11. Precede items in arrays, records, and import lists with commas

Each successive element in a long array, record, or import list should be preceded by
a comma and a space.

#### Rationale

PureScript does not support trailing commas, thus preceding an element with a comma
makes it easier to add and remove items to the end of a list.

#### Examples

```purescript
data Rgba = Rgba
  { red :: Int
  , green :: Int
  , blue :: Int
  , alpha :: Int
  }
```

### 1.12. Format export lists like arrays

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

### 1.13. Doubly indent nested record or array literals

When nesting record or array literals, the nested literal should be doubly indented (that is, indented 4 spaces.)

#### Examples

```purescript
{ bounds:
    { x: 0
    , y: 0
    , width: 400
    , height: 300
    }
, color: Red
, children:
    [ component1
    , component2
    , component3
    ]
}
```

### 1.14. Prefer case expressions over equational pattern matching

Case expressions should be used instead of equational pattern matching.

#### Rationale

If a function needs to be renamed when using a case expression in lieu of equational
pattern maching, only a single edit needs to be made.

#### Exceptions

When matching multiple patterns, using equational pattern matching may be preferable.

#### Examples

```purescript
catMaybes :: forall a. List (Maybe a) -> List a
catMaybes = case _ of
  Nil -> Nil
  Nothing : xs -> catMaybes xs
  Just x : xs -> x : catMaybes xs
```

## 2. Naming

### 2.1. Use camel case for function names

Functions must be written in camel case.

#### Examples

* `add`
* `fromMaybe`
* `isJust`

#### Rationale

Syntactically, functions in PureScript *must* begin with a lower case letter.

### 2.2. Use upper camel case for type names

Data types and constructors must be written in upper camel case.

#### Examples

* `Maybe`
* `CommutativeRing`
* `STRef`

#### Rationale

Syntactically, data types and constructors in PureScript *must* begin with a capital letter.

### 2.3. Use all capitals for effect names

Effects should be written in all capital letters.

#### Examples

* `CONSOLE`
* `EXCEPTION`
* `RANDOM`

### 2.4. Do not use all capitals for acronyms

Acronyms should be capitalized like any other word.

#### Rationale

Names containing adjacent capitals that belong to separate words may hinder
readability. Additionally, since function names must begin with a lower case
letter, fully capitalizing all acronyms can be impossible.

#### Exceptions

Two letter acronyms should have both letters capitalized.

#### Examples

* `HtmlParser`
* `rgbToHsl`
* `ST`

### 2.5. Use the singular for module names

Module names should be in the singular.

#### Examples

* Use `Data.String` instead of `Data.Strings`.
* Use `Data.Function` instead of `Data.Functions`.

## 3. Imports

### 3.1. Group imported modules by origin

Imports should be grouped in the following order:

1. the `Prelude`
2. other third-party imports
3. local application or library imports

### 3.2. Sort imports alphabetically

The imports in each import group should be sorted alphabetically by module name.

### 3.3. Qualify imports or explicitly list imported symbols

Imported modules should either always be qualified or have explicit import lists.

#### Rationale

This makes your code more robust against changes in imported modules. It also makes
your code compile without warnings.

#### Exceptions

The `Prelude` does not need to be qualified or have an implicit import list.

## 4. Comments

### 4.1. Use Markdown syntax in documentation comments

Markdown syntax should be used in documentation comments.

### 4.2. Comment every exported definition

Every exported function and data type should have a documentation comment.

## 5. Miscellaneous

### 5.1. Avoid over-using point-free style

Point-free style should be avoided when it inhibits readability.

### 5.2. Code must be warning-free

Code must not produce warnings when compiled.

#### Rationale

Ignoring warnings that are false positives or benign can eventually make
it difficult to identify warnings that are serious.
