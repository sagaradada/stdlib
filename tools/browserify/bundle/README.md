# Bundle

> Bundle files into a single file using [browserify][browserify].


<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- Package usage documentation. -->

<section class="usage">

## Usage

``` javascript
var bundle = require( '@stdlib/tools/browserify/bundle' );
```

#### bundle( files, \[dest,\] clbk )

Bundle files into a single file using [browserify][browserify].

``` javascript
var files = [
    '/foo/bar.js',
    '/beep/boop.js'
];

bundle( files, clbk );

function clbk( error, bundle ) {
    if ( error ) {
        throw error;
    }
    console.log( bundle.toString() );
}
```

To specify an output file path, provide a `dest` argument.

``` javascript
var files = [
    '/foo/bar.js',
    '/beep/boop.js'
];

bundle( files, './bundle.js', clbk );

function clbk( error ) {
    if ( error ) {
        throw error;
    }
}
```

</section>

<!-- /.usage -->

<!-- Package usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- Package usage examples. -->

<section class="examples">

## Examples

``` javascript
var join = require( 'path' ).join;
var bundle = require( '@stdlib/tools/browserify/bundle' );

var fpath = join( __dirname, 'fixtures', 'index.js' );
var files = [ fpath ];

bundle( files, onBundle );

function onBundle( error, output ) {
    if ( error ) {
        throw error;
    }
    console.log( output.toString() );
}
```

</section>

<!-- /.examples -->

<!-- Section for describing a command-line interface. -->

---

<section class="cli">

## CLI

<!-- CLI usage documentation. -->

<section class="usage">

### Usage

``` bash
Usage: browserify-bundle [options] file1 file2 ...

Options:

  -h,    --help                Print this message.
  -V,    --version             Print the package version.
```

</section>

<!-- /.usage -->

<!-- CLI usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- CLI usage examples. -->

<section class="examples">

### Examples

``` bash
$ browserify-bundle ./examples/fixtures/index.js
```

</section>

<!-- /.examples -->

</section>

<!-- /.cli -->

<!-- Section to include cited references. If references are included, add a horizontal rule *before* the section. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="references">

</section>

<!-- /.references -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[browserify]: https://github.com/substack/node-browserify

</section>

<!-- /.links -->
