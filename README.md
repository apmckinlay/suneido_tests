suneido_tests
=============

Portable tests for Suneido implementations.

Currently, there are implementations in cSuneido, jSuneido, gSuneido, suneido.js,
and in Suneido (stdlib) itself.

Tests are defined in text files.
They are read with the Suneido lexer.

A test file consists of multiple test cases for multiple fixtures.

```text
@fixture1
case1
case2
@fixture2 // comment
case1
case2
```

A test case is ended by a newline,
unless the line ends with a comma.
Otherwise commas are optional and ignored.

Comments are allowed.

Fixtures must be defined in each implementation for each type of test,
usually along with the other unit test code.

Fixtures
--------

`@compile`

- string, expected_type, expected_value
- string, throws "exception substring"

Classes should have their content shown sorted by member.

Functions should have their parameters shown

`@method` // call a method

- value, method, arg ..., expected

@method tests could be done with @execute, but @method doesn't require compiling and executing code.

`@execute` // compile and run

- string, expected
- string, `"**notfalse**"`
- string, throws "exception substring"

There should be a function Def(name, value) which can be used to define globals - this is necessary to test classes. If the value is a string, it is compiled with the specified name - this is necessary to test privatization.

`@tr`

- string, from, to, expected

`@regex_match`

- string, pattern // should match
- string, pattern, false // shouldn't match
- string, pattern, \0, \1 ...

`@regex_replace`

- string, pattern, replacement, expected

Only the first match is replaced.

`@dnum_add` // check both ways  
`@dnum_sub` // checks x - y = z and if z != 0 also y - x = -z  
`@dnum_mul` // check both ways  
`@dnum_div`

- number, number, expected

Round off the least significant decimal digit of the result
before comparing.

`@dnum_cmp`

- value, value, value ...

Compares each value to all of the following values, both ways.

`@lang_sub`

- string, pos [, len], expected

Test [i ::], [i :: n], and [i ..] on strings and objects

`@lang_range`

- string, start [, limit], expected

Test [start ..] and [start :: limit] on strings and objects

`@compare`

- value, value, value ...

Compares each value to all of the following values, both ways.

Values must be strings that can be compiled to constants.

`@compare_packed`

Same as @compare except it compares the values packed.

It should also check that Unpack reverses Pack.
