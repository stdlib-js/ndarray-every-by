<!--

@license Apache-2.0

Copyright (c) 2026 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# everyBy

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Test whether all elements along one or more [`ndarray`][@stdlib/ndarray/ctor] dimensions pass a test implemented by a predicate function.

<section class="intro">

</section>

<!-- /.intro -->



<section class="usage">

## Usage

```javascript
import everyBy from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-every-by@deno/mod.js';
```

You can also import the following named exports from the package:

```javascript
import { assign } from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-every-by@deno/mod.js';
```

#### everyBy( x\[, options], predicate\[, thisArg] )

Tests whether all elements along one or more [`ndarray`][@stdlib/ndarray/ctor] dimensions pass a test implemented by a predicate function.

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

function isPositive( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ] );

// Test whether all elements are positive:
var out = everyBy( x, isPositive );
// returns <ndarray>[ true ]
```

The function accepts the following arguments:

-   **x**: input [`ndarray`][@stdlib/ndarray/ctor].
-   **options**: function options _(optional)_.
-   **predicate**: predicate function.
-   **thisArg**: predicate function execution context _(optional)_.

The function accepts the following options:

-   **dims**: list of dimensions over which to perform a reduction.
-   **keepdims**: boolean indicating whether the reduced dimensions should be included in the returned [`ndarray`][@stdlib/ndarray/ctor] as singleton dimensions. Default: `false`.

By default, the function performs a reduction over all elements in a provided [`ndarray`][@stdlib/ndarray/ctor]. To reduce specific dimensions, set the `dims` option.

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

function isPositive( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ 1.0, 2.0 ], [ -3.0, -4.0 ] ] );
// returns <ndarray>

var opts = {
    'dims': [ 1 ]
};

// Perform reduction:
var out = everyBy( x, opts, isPositive );
// returns <ndarray>[ true, false ]
```

By default, the function returns an [`ndarray`][@stdlib/ndarray/ctor] having a shape matching only the non-reduced dimensions of the input [`ndarray`][@stdlib/ndarray/ctor] (i.e., the reduced dimensions are dropped). To include the reduced dimensions as singleton dimensions in the output [`ndarray`][@stdlib/ndarray/ctor], set the `keepdims` option to `true`.

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

function isPositive( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ 1.0, 2.0 ], [ -3.0, -4.0 ] ] );

var opts = {
    'keepdims': true
};

// Perform reduction:
var out = everyBy( x, opts, isPositive );
// returns <ndarray>[ [ false ] ]
```

To set the function execution context, provide a `thisArg`.

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

function isPositive( value ) {
    this.count += 1;
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ] );
// returns <ndarray>

// Create a context object:
var ctx = {
    'count': 0
};

// Perform reduction:
var out = everyBy( x, isPositive, ctx );
// returns <ndarray>[ true ]

var count = ctx.count;
// returns 4
```

#### everyBy.assign( x, y\[, options], predicate\[, thisArg] )

Tests whether all elements along one or more [`ndarray`][@stdlib/ndarray/ctor] dimensions pass a test implemented by a predicate function and assigns the result to a provided output [`ndarray`][@stdlib/ndarray/ctor].

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';
import empty from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-empty@deno/mod.js';

function isPositive( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ] );

// Create an output ndarray:
var y = empty( [], {
    'dtype': 'bool'
});

// Perform reduction:
var out = everyBy.assign( x, y, isPositive );
// returns <ndarray>[ true ]

var bool = ( out === y );
// returns true
```

The function accepts the following arguments:

-   **x**: input [`ndarray`][@stdlib/ndarray/ctor].
-   **y**: output [`ndarray`][@stdlib/ndarray/ctor]. The output [`ndarray`][@stdlib/ndarray/ctor] must have a shape matching the non-reduced dimensions of the input [`ndarray`][@stdlib/ndarray/ctor].
-   **options**: function options _(optional)_.
-   **predicate**: predicate function.
-   **thisArg**: predicate function execution context _(optional)_.

The function accepts the following options:

-   **dims**: list of dimensions over which to perform a reduction.

By default, the function performs a reduction over all elements in a provided [`ndarray`][@stdlib/ndarray/ctor]. To reduce specific dimensions, set the `dims` option.

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';
import empty from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-empty@deno/mod.js';

function predicate( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ 1.0, 2.0 ], [ -3.0, -4.0 ] ] );
// returns <ndarray>

// Create an output ndarray:
var y = empty( [ 2 ], {
    'dtype': 'bool'
});

var opts = {
    'dims': [ 1 ]
};

// Perform reduction:
var out = everyBy.assign( x, y, opts, predicate );
// returns <ndarray>[ true, false ]

var bool = ( out === y );
// returns true
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   The predicate function is provided the following arguments:

    -   **value**: current array element.
    -   **indices**: current array element indices.
    -   **arr**: the input ndarray.

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
import discreteUniform from 'https://cdn.jsdelivr.net/gh/stdlib-js/random-array-discrete-uniform@deno/mod.js';
var isPositive = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/assert-is-positive-number' ).isPrimitive;
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import ndarray from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-ctor@deno/mod.js';
import everyBy from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-every-by@deno/mod.js';

var xbuf = discreteUniform( 40, 0, 10 );
var x = new ndarray( 'generic', xbuf, [ 2, 4, 5 ], [ 20, 5, 1 ], 0, 'row-major' );
console.log( ndarray2array( x ) );

var y = everyBy( x, isPositive );
console.log( y.get() );
```

</section>

<!-- /.examples -->

<!-- Section for related links. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/ndarray-every-by.svg
[npm-url]: https://npmjs.org/package/@stdlib/ndarray-every-by

[test-image]: https://github.com/stdlib-js/ndarray-every-by/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/ndarray-every-by/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/ndarray-every-by/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/ndarray-every-by?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/ndarray-every-by.svg
[dependencies-url]: https://david-dm.org/stdlib-js/ndarray-every-by/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/ndarray-every-by/tree/deno
[deno-readme]: https://github.com/stdlib-js/ndarray-every-by/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/ndarray-every-by/tree/umd
[umd-readme]: https://github.com/stdlib-js/ndarray-every-by/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/ndarray-every-by/tree/esm
[esm-readme]: https://github.com/stdlib-js/ndarray-every-by/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/ndarray-every-by/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/ndarray-every-by/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor/tree/deno

<!-- <related-links> -->

<!-- </related-links> -->

</section>

<!-- /.links -->
