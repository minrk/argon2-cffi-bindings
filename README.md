# Low-level Python CFFI Bindings for Argon2

*argon2-cffi-bindings* provides low-level [*CFFI*](https://cffi.readthedocs.io/) bindings to the official implementation of the [Argon2] password hashing algorithm.

<!-- [[[cog
# Extract commit ID; refresh using `tox -e cog`
import subprocess
out = subprocess.check_output(["git", "submodule"], text=True)
id = out.strip().split(" ", 1)[0]
link = f'[**`{id[:7]}`**](https://github.com/P-H-C/phc-winner-argon2/commit/{id})'
print(f"The currently vendored Argon2 commit ID is {link}.")
]]] -->
The currently vendored Argon2 commit ID is [**`f57e61e`**](https://github.com/P-H-C/phc-winner-argon2/commit/f57e61e19229e23c4445b85494dbf7c07de721cb).
<!-- [[[end]]] -->

> **Note**
> If you want to hash passwords in an application, this package is **not** for you.
> Have a look at [*argon2-cffi*] with its high-level abstractions!

These bindings have been extracted from [*argon2-cffi*] and it remains its main consumer.
However, they may be used by other packages that want to use the Argon2 library without dealing with C-related complexities.


## Usage

*argon2-cffi-bindings* is available from [PyPI](https://pypi.org/project/argon2-cffi-bindings/).
The provided *CFFI* bindings are compiled in API mode.

Best effort is given to provide binary wheels for as many platforms as possible.


### Disabling Vendored Code

A copy of [Argon2] is vendored and used by default, but can be disabled if *argon2-cffi-bindings* is installed using:

```console
$ env ARGON2_CFFI_USE_SYSTEM=1 \
  python -Im pip install --no-binary=argon2-cffi-bindings argon2-cffi-bindings
```


### Overriding Automatic *SSE2* Detection

Usually the build process tries to guess whether or not it should use [*SSE2*](https://en.wikipedia.org/wiki/SSE2)-optimized code (see [`_ffi_build.py`](https://github.com/hynek/argon2-cffi-bindings/blob/main/src/_argon2_cffi_bindings/_ffi_build.py) for details).
This can go wrong and is problematic for cross-compiling.

Therefore you can use the `ARGON2_CFFI_USE_SSE2` environment variable to control the process:

- If you set it to ``1``, *argon2-cffi-bindings* will build **with** SSE2 support.
- If you set it to ``0``, *argon2-cffi-bindings* will build **without** SSE2 support.
- If you set it to anything else, it will be ignored and *argon2-cffi-bindings* will try to guess.

However, if our heuristics fail you, we would welcome a bug report.


### Python API

Since this package is intended to be an implementation detail, it uses a private module name to prevent your users from using it by accident.

Therefore you have to import the symbols from `_argon2_cffi_bindings`:

```python
from _argon2_cffi_bindings import ffi, lib
```

Please refer to [*cffi* documentation](https://cffi.readthedocs.io/en/latest/using.html) on how to use the `ffi` and `lib` objects.

The list of symbols that are provided can be found in the [`_ffi_build.py` file](https://github.com/hynek/argon2-cffi-bindings/blob/main/src/_argon2_cffi_bindings/_ffi_build.py).

[Argon2]: https://github.com/p-h-c/phc-winner-argon2
[*argon2-cffi*]: https://argon2-cffi.readthedocs.io/


## Project Information

- [**Changelog**](https://github.com/hynek/argon2-cffi-bindings/blob/main/CHANGELOG.md)
- [**Documentation**](https://github.com/hynek/argon2-cffi-bindings#readme)
- [**PyPI**](https://pypi.org/project/argon2-cffi-bindings/)
- [**Source Code**](https://github.com/hynek/argon2-cffi-bindings)
- **License**: [MIT](https://github.com/hynek/argon2-cffi-bindings/blob/main/LICENSE)
- **Supported Python Versions**: 3.7 and later, including PyPy


### Credits & License

*argon2-cffi-bindings* is written and maintained by [Hynek Schlawack](https://hynek.me/about/).
It is released under the [MIT license](https://github.com/hynek/argon2-cffi/blob/main/LICENSE>).

The development is kindly supported by [Variomedia AG](https://www.variomedia.de/).

The authors of Argon2 were very helpful to get the library to compile on ancient versions of Visual Studio for ancient versions of Python.

The documentation quotes frequently in verbatim from the Argon2 [paper](https://www.password-hashing.net/argon2-specs.pdf) to avoid mistakes by rephrasing.


#### Vendored Code

The original Argon2 repo can be found at <https://github.com/P-H-C/phc-winner-argon2/>.

Except for the components listed below, the Argon2 code in this repository is copyright (c) 2015 Daniel Dinu, Dmitry Khovratovich (main authors), Jean-Philippe Aumasson and Samuel Neves, and under [CC0] license.

The string encoding routines in src/encoding.c are copyright (c) 2015 Thomas Pornin, and under [CC0] license.

The [*BLAKE2*](https://www.blake2.net) code in ``src/blake2/`` is copyright (c) Samuel Neves, 2013-2015, and under [CC0] license.

[CC0]: https://creativecommons.org/publicdomain/zero/1.0/


### *argon2-cffi-bindings* for Enterprise

Available as part of the Tidelift Subscription.

The maintainers of *argon2-cffi-bindings* and thousands of other packages are working with Tidelift to deliver commercial support and maintenance for the open-source packages you use to build your applications.
Save time, reduce risk, and improve code health, while paying the maintainers of the exact packages you use.
[Learn more.](https://tidelift.com/subscription/pkg/pypi-argon2-cffi-bindings?utm_source=undefined&utm_medium=referral&utm_campaign=enterprise&utm_term=repo)
