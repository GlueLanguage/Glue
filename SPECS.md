# Glue SPECS
Specifications for the Glue language.

## Table of contents
1. Built-in types
2. Statements
3. Expressions
4. Code blocks
5. Visibility modifiers
6. Functions
7. Structs and classes
8. Conditionals and loops

## 1. Built-in types
name | description
-----|--------------
int8  | 8-bit signed integer
int16 | 16-bit signed integer
int32 | 32-bit signed integer
int64 | 64-bit signed integer
int   | signed integer *(size defined by compiler flag, default is 32-bit)*

name | description
-----|--------------
uint8  | 8-bit unsigned integer
uint16 | 16-bit unsigned integer
uint32 | 32-bit unsigned integer
uint64 | 64-bit unsigned integer
uint   | unsigned integer *(size defined by compiler flag, default is 32-bit)*

name | description
-----|--------------
float16 | 16-bit floating point number (IEEE-754)
float32 | 32-bit floating point number (IEEE-754)
float64 | 64-bit floating point number (IEEE-754)
float   | floating point number (IEEE-754) *(size defined by compiler flag, default is 32-bit)*

name | description
-----|--------------
bool | 8-bit boolean

**Important types part of the std:**

name | description
-----|--------------
char   | special character type that supports UTF-8? TODO
string | UTF-8 encoded string

## 2. Statements
Variable definition:<br>
`<var-type> <identifier> = <expr>;`

Variable assignment:<br>
`<identifier> = <expr>;`



## 3. Expressions
Basic expression syntax:<br>
`<lhs-expr> [<binary_op> <rhs-expr>]`

Possible types of expressions:
1. Literals
2. Variable references
3. Function calls

Possible types of binary operations:
1. Addition `+`
2. Subtraction `-`
3. Multiplication `*`
4. Division `/`
5. Unary `-`

## 4. Code blocks
Code blocks are defined as a list of statements, starting with `{` and ending with `}`.
Example:
`{ int32 a = 8; }`

## 5. Visibility modifiers
Everything is private by default, where applicable.
To make something public, simply specify `public` as the visibility modifier.

## 6. Functions
Function declaration:<br>
```
[visibility-modifier] func <identifier>([<var-type> <identifier>, ..]) {}
```
Return type:<br>
```
[visibility-modifier] func <identifier>([<var-type> <identifier>, ..]) : <var-type> //Single return
[visibility-modifier] func <identifier>([<var-type> <identifier>, ..]) : (<var-type> <identifier>, ..) //Multiple named returns
```

Function calls:<br>
```
<func-identifier>([<var-ref>, ..])
```

Short-hand *(return is implied)*:<br>
```
[visibility-modifier] func <identifier>([<var-type> <identifier>, ..]) : [return-type] => <expr>;
```

## 7. Structs and classes
Struct syntax + example:
```
[visibility-modifier] struct <identifier> {
	[visibility-modifier] <var-type> <identifier>;
}
```

```glue
struct Example {
	int hidden;
	public int visible;
}
```

Classes are simply structs that have had functions implemented on them. Syntax + example:
```
[visibility-modifier] struct <identifier> {
	[visibility-modifier] <var-type> <identifier>;

	impl {
		[visibility-modifier] <func-declaration>
	}
}
```

```glue
struct Example {
	int hidden;

	impl {
		public func RevealHidden() => self.hidden; //TODO: Think of a way to define if it references or consumes itself (for builder pattern)
	}
}
```

## 8. Conditionals and loops
If-statements:
```
if (<expr>) <stmt/codeblock>
```

While-loops:
```
while (<expr>) <stmt/codeblock>
```

For-loops:
```
for (<identifier> in <enumerable>) <stmt/codeblock>
```

Enumerable: TODO