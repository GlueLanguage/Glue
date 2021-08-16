# Glue SPECS
Specifications for the Glue language.

## Table of contents
0. [Naming conventions and other preferences](https://github.com/GlueLanguage/Glue/blob/main/SPECS.md#0-naming-conventions-and-other-preferences)
1. [Built-in types](https://github.com/GlueLanguage/Glue/blob/main/SPECS.md#1-built-in-types)
2. [Statements](https://github.com/GlueLanguage/Glue/blob/main/SPECS.md#2-statements)
3. [Expressions](https://github.com/GlueLanguage/Glue/blob/main/SPECS.md#3-expressions)
4. [Code blocks](https://github.com/GlueLanguage/Glue/blob/main/SPECS.md#4-code-blocks)
5. [Visibility modifiers](https://github.com/GlueLanguage/Glue/blob/main/SPECS.md#5-visibility-modifiers)
6. [Functions](https://github.com/GlueLanguage/Glue/blob/main/SPECS.md#6-functions)
7. [Structs and classes](https://github.com/GlueLanguage/Glue/blob/main/SPECS.md#7-structs-and-classes)
8. [Conditionals and loops](https://github.com/GlueLanguage/Glue/blob/main/SPECS.md#8-conditionals-and-loops)

## 0. Naming conventions and other preferences
Although the naming convention used throughout a program is up to the developer, we use a certain naming convention in the std and examples, so we expect this to become an "unofficial" prefered naming convention. We use `snake_case` for function names, and `CamelCase` for struct names, enum names, etc.
TODO: Add more information

## 1. Built-in types
name | description
-----|--------------
i8     | 8-bit signed integer
i16    | 16-bit signed integer
i32    | 32-bit signed integer
i64    | 64-bit signed integer
isize  | pointer-sized signed integer

name | description
-----|--------------
u8     | 8-bit unsigned integer
u16    | 16-bit unsigned integer
u32    | 32-bit unsigned integer
u64    | 64-bit unsigned integer
usize  | pointer-sized unsigned integer

name | description
-----|--------------
f16 | 16-bit floating point number (IEEE-754)
f32 | 32-bit floating point number (IEEE-754)
f64 | 64-bit floating point number (IEEE-754)

name | description
-----|--------------
bool | 8-bit boolean

**Important types part of the std:**

name | description
-----|--------------
char   | special character type that supports UTF-8? TODO
string | UTF-8 encoded string

## 2. Statements
Variable definition:
```
<var-type> <identifier> = <expr>;
```

Variable assignment:
```
<identifier> = <expr>;
```

Return statement:
```glue
return <expr>;
```

## 3. Expressions
Basic expression syntax:
```
<lhs-expr> [<binary_op> <rhs-expr>]
```

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
```glue
{
	u32 a = 8;
	u32 b = a;
	a = 5;
}
```

Code blocks can also be nested inside each other, allowing you to limit scope whenever you please.
Example:
```glue
{
	u32 a = 8;
	{
		u32 b = a;
	}
	b = 5; //Not possible, b is out of scope here
}
```

## 5. Visibility modifiers
Everything is private by default, where applicable.
To make something public, simply specify `pub` as the visibility modifier.
TODO: More visibility modifiers to aid with the import system.

## 6. Functions
Function declaration:
```
[visibility-modifier] func <identifier>([<var-type> <identifier>, ..]) {}
```
Return type:
```
[visibility-modifier] func <identifier>([<var-type> <identifier>, ..]) : <var-type> //Single return
[visibility-modifier] func <identifier>([<var-type> <identifier>, ..]) : (<var-type> <identifier>, ..) //Multiple named returns
```

Function calls:
```
<func-identifier>([<var-ref>, ..])
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
	u32 hidden;
	pub u32 visible;
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
	u32 hidden;
}

impl {
	pub func reveal_hidden(ref self) : u32 {
		return self.hidden;
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
