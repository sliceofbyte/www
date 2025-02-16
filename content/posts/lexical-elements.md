---
title: Lexical elements
date: February 16, 2025, 5:02 PM
version: "go1.24 (Dec 30, 2024)"
---

Lexical elements define the structure of Go source code, similar to how words form sentences. These elements include identifiers, keywords, operators, literals, and punctuation. The lexer (or lexical analyzer) scans the source code and breaks it down into tokens, which represent these elements. These tokens are then passed to the parser, which constructs an abstract syntax tree (AST) to represent the program’s structure. The AST is used by the compiler to generate executable code.

## Comments

Comments are for humans, The compiler ignores them, but you shouldn’t. Just don’t put them inside [string](#string-literals) or [rune literals](#rune-literals)—the parser won’t be amused.

Go has two types of comments:  

- **Line comments** start with `//` and go to the end of the line.  
- **Block comments** are enclosed in `/* ... */`, span multiple lines, and can appear anywhere whitespace is allowed.  

```go
// This is a line comment.

/*
   This is a block comment.
   Useful for larger explanations.
*/
```

Block comments act like spaces if they contain no newlines; otherwise, they behave like newlines. You can’t nest them.

## Tokens

Tokens are the smallest units of meaningful elements in source code, identified during [lexical analysis](https://en.wikipedia.org/wiki/Lexical_analysis). Think of tokens as the words in a sentence. In Go, they include:

- **Identifiers** (e.g., `x`, `MyFunc`)
- **Keywords** (`func`, `if`, `return`, etc.)
- **Operators & punctuation** (`+`, `:=`, `{}`, etc.)
- **Literals** (`42`, `"hello"`, `0xFF`)

Whitespace separates tokens but is otherwise ignored.

## Semicolons (or lack thereof)

Go has semicolons, but you don’t need to type them. The lexer inserts them automatically at the end of a line if the last token is:

- an identifier  
- a literal (`42`, `"hello"`, etc.)  
- `break`, `continue`, `fallthrough`, or `return`  
- an operator like `++`, `--`, `)`, `]`, or `}`  

If you insist on manually adding semicolons, you can, but it’s not recommended.

## Identifiers

Identifiers name things—variables, functions, types. They start with a letter and can include digits.

```go
foo
X9
thisIsCamelCase
αβ // Unicode allowed
```

They’re case-sensitive, so foo and Foo are different. Choose wisely.

## Keywords

Go has 25 reserved words, or keywords. You can’t use them as identifiers.  

`break`, `case`, `chan`, `const`, `continue`, `default`, `defer`, `else`, `fallthrough`, `for`, `func`, `go`, `goto`, `if`, `import`, `interface`, `map`, `package`, `range`, `return`, `select`, `struct`, `switch`, `type`, `var`.

## Operators and punctuation

Go has a variety of operators and punctuation marks. The following character sequences represent operators and punctuation in Go:

```go
+    &     +=    &=     &&    ==    !=    (    )
-    |     -=    |=     ||    <     <=    [    ]
*    ^     *=    ^=     <-    >     >=    {    }
/    <<    /=    <<=    ++    =     :=    ,    ;
%    >>    %=    >>=    --    !     ...   .    :
     &^          &^=          ~
```

## Integer literals

Go supports decimal, binary, octal, and hexadecimal literals.  

```go
42   // Decimal
0b10 // Binary
0o60 // Octal
0xFF // Hexadecimal
```

## Floating-point literals

Floating-point literals can be written in decimal or scientific notation.  

```go
3.14    // Decimal
6.022e23 // Scientific
```

They’re precise but not perfect—just like... well, you know.

## Imaginary literals

Imaginary literals are commonly used in scientific computing and graphics applications. They’re written with a numeric literal followed by the `i` suffix.

```go
3.14i
```

## Using `_` in numeric literals

You can use underscores `_` to make numeric literals more readable. They’re ignored by the compiler.

```go
1_000_000 // Same as 1000000
0b_0010_0000 // Same as 0b00100000
```

If an underscore is the first or last character in a numeric literal, or if two underscores appear next to each other, the compiler will complain.

```go
fmt.Println(0b0_010_0000_)
// Output: '_' must separate successive digits
```

## Rune literals

Go source text is Unicode characters encoded in UTF-8. A rune literal represents a single Unicode code point. A rune literal is expressed as one or more characters enclosed in a pair of quotes.

There are several ways to express a rune literal, the most common being a single character enclosed in single quotes.

```go
'a'   // 97
'本'  // 26412
```

Similarly, you can represent a rune literal as a Unicode code point in hexadecimal or octal notation. If we want to represent the character `a` (which is `U+0061` in Unicode or `97` in decimal), we can write it as:

```go
'\x61' // 97 in hexadecimal
'\141' // 97 in octal
```

Which are all equivalent to `'a'`.

There are a several ways to represent a Unicode code point, we recommend that you read the [Go specification](https://golang.org/ref/spec#Rune_literals) for more details.

## String literals

There are two types of string literals in Go: raw string literals and interpreted string literals.

### Raw string literals

Raw string literals are character sequences between quotes, like so:

```go
`Hello, 世界`
```

The value of a raw string literal is the string composed of the uninterpreted characters between the quotes. Within the quotes, any character may appear except back quote. Backslashes have no special meaning inside a raw string literal, and the string may span multiple lines.

### Interpreted string literals

Interpreted string literals are character sequences between double quotes, like so:

```go
"Hello, 世界"
```

The text between the double quotes forms the value of the literal, with backslash escapes interpreted as they are in [rune literals](#rune-literals). Backslashes have a special meaning inside interpreted string literals. An escape sequence is a backslash (`\`) followed by one or more characters that replace the sequence. For example, the escape sequence `\n` represents a newline character.
