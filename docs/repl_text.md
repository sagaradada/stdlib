# REPL Text

> A guide for writing REPL texts.


Read-eval-print-loop (REPL) texts are plain text documents which provide help information in a REPL context. A typical use case is when a user is performing various actions within a REPL and would like to know how to use a particular function interface. For example,

``` bash
> help( lowercase )

lowercase( str )
    Converts a `string` to lowercase.

    Parameters
    ----------
    str: string
        Input string.

    Returns
    -------
    out: string
        Lowercase string.

    Examples
    --------
    > var out = lowercase( 'bEEp' )
    'beep'

    See Also
    --------
    uppercase


```

The above REPL text displays the function interface `lowercase( str )`, as well as provides more detailed information, including input parameter types, return value types, and examples.


## Guide

### Format

The general format of a REPL text is as follows:

``` text

{{alias}}( param1, param2, ... )
    A short description.

    A longer description, including notes explaining special cases and use
    cases.

    Parameters
    ----------
    param1: <type>
        Parameter description.

    param2: <type>
        Parameter description.

    Returns
    -------
    out: <type>
        Return value description.

    Examples
    --------
    > var out = {{alias}}()
    <output>

    References
    ----------
    - Nadler, Boaz. 2006. "Design Flaws in the Implementation of the Ziggurat
      and Monty Python methods (and some remarks on MATLAB randn)." *ArXiv*
      abs/math/0603058 (March).

    See Also
    --------


```

### Spacing

REPL texts should use `4` space indentation. Do __not__ use tab indentation, as tabs are rendered inconsistently across terminals.


### Wrapping

REPL texts should __never__ exceed `80` characters in width. Be sure to wrap all text longer than `80` characters.


### Interface

An interface may be a primitive constant (e.g., `number`, `string`, `boolean`), an `Object` (e.g., a regular expression), or a `Function`. If an interface is a function, the interface should display all required and optional parameters. If an interface has associated properties and/or methods, document each method and property separately.

``` text
foo( bar )
    A short description.

    ...

    Examples
    --------
    ...

foo.beep( boop )
    A short description.

    ...

    Examples
    --------
    ...

foo.boop( beep )
    A short description.

    ...

    Examples
    ________
    ...

    References
    ----------
    ...

    See Also
    --------


```

A few notes:

* In a function interface, each parameter should be surrounded by `1` space to the left and `1` space to the right.

  ``` text
  foo( beep, boop, bop )
      A short description.

      ...
  ```

* If a function parameter is __optional__, enclose the parameter in square brackets.

  ``` text
  foo( beep[, boop[, bop]] )
      A short description.

      ...
  ```


### Description

#### Short Description

The short description should be a single sentence written in the simple present tense. For example,

``` text
lowercase( str )
    Converts a `string` to lowercase.

    ...
```

Do __not__ write the description in the declarative mood. For example, avoid

``` text
lowercase( str )
    Convert a `string` to lowercase.

    ...
```

An empty line should __always__ follow the short description.


#### Extended Description

An extended description should include auxiliary information which helps a user understand expected behavior. For example,

``` text
dcopy( N, x, strideX, y, strideY )
    Copies values from `x` into `y`.

    The `N` and `stride` parameters determine how values from `x` are copied
    into `y`.

    Indexing is relative to the first index. To introduce an offset, use typed
    array views.

    If `N` is less than or equal to `0`, the function returns `y` unchanged.

    Parameters
    ----------
    ...
```

Each separate *note* within an extended description should be followed by an empty line.


##### Lists

To include a list in an extended description, use the following style

``` text
    ...

    This is a list:

    - item 1
    - item 2

    ...
```


### Parameters

The `Parameters` section states the parameter name, the parameter type, and a short description. An empty line should follow each parameter declaration.

``` text
pad( str, len[, options] )
    Short description.

    Parameters
    ----------
    str: string
        Input string.

    len: integer
        Output string length.

    options: Object (optional)
        Options.

    options.lpad: string (optional)
        String used to left pad.

    options.rpad: string (optional)
        String used to right pad.

    options.centerRight: boolean (optional)
        Boolean indicating whether to center right in the event of a tie.
        Default: `false` (i.e., center left).

    ...
```

To document a variadic interface,

``` text
foo( ...args )
    A short description.

    Parameters
    ----------
    args: ...string
        String arguments.

    ...
```

The following parameter types are supported:

* `any`: if a parameter can be any type.
* `null`: if a parameter must be `null`.
* `undefined`: if a parameter must be `undefined`.
* `string`: if a parameter must be a `string` primitive.
* `number`: if a parameter must be a `number` primitive.
* `integer`: if a parameter must be a `number` primitive having an integer value.
* `boolean`: if a parameter must be a `boolean` primitive.
* `Function`: if a parameter must be a `function`.
* `Object`: if a parameter must be an `object`.
* `Array`: if a parameter must be an `array`.
* `Array<type>`: if a parameter must be an `array` containing only values of a particular type.
* `RegExp`: if a parameter must be a regular expression.
* `Date`: if a parameter must be a `Date` object.
* `Buffer`: if a parameter must be a Node.js `Buffer` object.
* `Error`: if a parameter must be an `Error` object.
* `TypedArray`: if a parameter must be a typed array.
* `Float64Array`: if a parameter must be a `Float64Array`.
* `Float32Array`: if a parameter must be a `Float32Array`.
* `Int32Array`: if a parameter must be an `Int32Array`.
* `Uint32Array`: if a parameter must be a `Uint32Array`.
* `Int16Array`: if a parameter must be an `Int16Array`.
* `Uint16Array`: if a parameter must be a `Uint16Array`.
* `Int8Array`: if a parameter must be an `Int8Array`.
* `Uint8Array`: if a parameter must be a `Uint8Array`.
* `Uint8ClampedArray`: if a parameter must be a `Uint8ClampedArray`.
* `ArrayBuffer`: if a parameter must be an `ArrayBuffer`.

For parameters which may be more than one type, use a `|` separator.

``` text
foo( value )
    A short description.

    Parameters
    ----------
    value: string|number|boolean
        A parameter description.

    ...
```

In general, avoid specialized and/or uncommon value types; e.g., `NonNegativeInteger`, `Probability`, etc. Users are unable to discern the meaning of specialized types without access to external (possibly out-of-band) documentation.

A few notes:

* Parameter names should __match__ the parameter names in function and method signatures.
* If a parameter is __optional__, explicitly state that the parameter is optional __after__ the type declaration.
* For `Object` parameters, list each required and/or optional `Object` property as a separate parameter.
* All parameter descriptions should end with a period.
* If a `function` does not have parameter values, __omit__ this section.


### Returns

The `Returns` section states the return value name, the return value type, and a short description. An empty line should follow each return value declaration.

``` text
    ...

    Returns
    -------
    out: <type>
        A short description.

    ...
```

Conventional names for output values include

* `bool`: for `boolean` return values.
* `fcn`: for `Function` return values.
* `out`: for generic return values.
* `y`: for `number` return values mathematical functions satisfying the form `y = f(x)`.

For return values which can be more than one type, use a `|` separator.

``` text
    ...

    Returns
    -------
    out: Buffer|Error
        A short description.

    ...
```

A few notes:

* For `Object` return values having a defined structure (e.g., mathematical models), list each `Object` property as a separate return value and separate each property with an empty line.
* Possible return value types are the same as for parameters.
* All return value descriptions should end with a period.
* If a `function` does not have return values, __omit__ this section.


### Examples

Examples should demonstrate essential behavior.

``` text
foo( str )
    A short description.

    Parameters
    ----------
    str: string
        An input value.

    Returns
    -------
    out: string
        An output value.

    Examples
    --------
    > var out = foo( 'beep' )
    'boop'

    ...
```

To delineate examples demonstrating conceptually distinct behavior, use comment headings and separate each example with an empty line.

``` text
foo( str )
    A short description.

    Parameters
    ----------
    str: string|number
        An input value.

    Returns
    -------
    out: string
        An output value.

    Examples
    --------
    // String inputs:
    > var out = foo( 'beep' )
    'boop'

    // Number inputs:
    > var x = 3.14;
    > out = foo( x )
    10.0

    ...
```

A few notes:

* Begin each line of user input with a `>` symbol.
* Place expected output on the line immediately following a line of user input.
* To indicate silenced output (i.e., a line of user input whose output is suppressed), end a user input line with a semicolon.
* Only declare variables the first time a variable is used.
* A REPL text should __always__ include an `Examples` section.


### References

Only include references __if__ usage requires citations. If not required, remove the `References` section entirely. Otherwise, include citations, placing each on a separate line without line separation. For example,

``` text
    ...

    References
    ----------
    - Nadler, Boaz. 2006. "Design Flaws in the Implementation of the Ziggurat
      and Monty Python methods (and some remarks on MATLAB randn)." *ArXiv*
      abs/math/0603058 (March).
    - McFarland, Christopher D. 2016. "A modified ziggurat algorithm for
      generating exponentially and normally distributed pseudorandom numbers."
      *Journal of Statistical Computation and Simulation* 86 (7): 1281–94.
      doi:10.1080/00949655.2015.1060234.

    ...
```

A few notes:

* Each citation should be a properly formatted citation.
* Citations are not required to include URLs.
* Include only __one__ `References` section per REPL text.


### See Also

The `See Also` section should include related functionality available in a REPL context. Each entry in the section should have a corresponding REPL text and thus be available to a user in a manner similar to the source REPL text.

``` text
    ...

    See Also
    --------
    beep, boop, bar

```

A few notes:

* Separate each entry with a comma followed by a space.
* Insert an empty line following the last line containing entries.
* If a `See Also` section does __not__ contain entries, insert two empty lines following the section header.
* Include only __one__ `See Also` section per REPL text.