
<!-- README.md is generated from README.Rmd. Please edit that file -->

# tok

<!-- badges: start -->

[![R build
status](https://github.com/dfalbel/tok/workflows/R-CMD-check/badge.svg)](https://github.com/dfalbel/tok/actions)
<!-- badges: end -->

tok provides bindings to the
[🤗tokenizers](https://huggingface.co/docs/tokenizers/v0.13.3/en/index)
library. It uses the same Rust libraries that powers the Python
implementation.

We still don’t provide the full API of tokenizers. Please open a issue
if there’s a feature you are missing.

## Installation

Before you can install this package, you need to install a working Rust
toolchain. We recommend using [rustup.](https://rustup.rs/)

On Windows, you’ll also have to add the `i686-pc-windows-gnu` and
`x86_64-pc-windows-gnu` targets:

    rustup target add x86_64-pc-windows-gnu
    rustup target add i686-pc-windows-gnu

Once Rust is working, you can install this package via:

``` r
remotes::install_github("dfalbel/tok")
```

## Features

We still don’t have complete support for the 🤗tokenizers API. Please
open an issue if you need a feature that is currently not implemented.

## Loading tokenizers

`tok` can be used to load and use tokenizers that have been previously
serialized. For example, HuggingFace model weights are usually
accompanied by a ‘tokenizer.json’ file that can be loaded with this
library.

To load a pre-trained tokenizer from a json file, use:

``` r
path <- testthat::test_path("assets/tokenizer.json")
tok <- tok::tokenizer$from_file(path)
```

Use the `encode` method to tokenize sentendes and `decode` to transform
them back.

``` r
enc <- tok$encode("hello world")
tok$decode(enc$ids)
#> [1] "hello world"
```

## Using pre-trained tokenizers

You can also load any tokenizer available in HuggingFace hub by using
the `from_pretrained` static method. For example, let’s load the GPT2
tokenizer with:

``` r
tok <- tok::tokenizer$from_pretrained("gpt2")
enc <- tok$encode("hello world")
tok$decode(enc$ids)
#> [1] "hello world"
```
