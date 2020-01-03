# Grawkit - The Awksome Git Graph Generator [![MIT License][license-svg]][license-url]

Grawkit is a tool that helps build SVG graphs from git command-line descriptions, and is built in Awk.

This tool was created in support of the ["Orthogonal Git Workflow"][orthogonal-git] post. Yes, this took way longer to write than the post itself.

## Testing & Documentation

A `Makefile` is provided for running tests and producing documentation for Grawkit. Run `make help` in the project root for more information.

A full test-suite is provided (depending only on `make` and `awk`), which should serve as a good example of the existing feature-set. Run it with `make test`.

## Installation

Copy the included `grawkit` AWK script into your local search path (most commonly
`$HOME/.local/bin`), or just use it directly in this folder. Grawkit should work with most
POSIX-compatible AWK implementations, and has been tested against `gawk`, `nawk`, `busybox awk`, and `goawk`.

## Status & Usage

Grawkit has basic support for common `git` commands such as `git branch`, `git tag` and `git merge`, allowing for fairly complex graphs. The integrated test-suite serves as an example, check the `tests` folder for more.

In order to use this tool, either run the `grawkit` executable against a file containing supported
`git` commands (any command not recognized will be silently ignored), or pass these in standard
input. For instance, given the following file `test.txt`:

```sh
git checkout Industrialization
git commit -m "Expected activity1 result"
git tag Assignee
git commit -m "Expected activity2 result"
git branch Parrallel_Activity_To_Scope
git checkout Parrallel_Activity_To_Scope
git commit -m "Expected parallel activity result"
git checkout Industrialization
git merge Parrallel_Activity_To_Scope
git commit -m "Release: An expected X.Y release"
git tag X.Y
```

You can execute either:

```sh
grawkit explanation.rmp > test.svg
```

Which will produce SVG markup to standard output, rendered as:

<p align="center"> <img
src="https://github.com/fthomasfr/grawkit/blob/roadmap/tests/explanation.svg"
alt="" width="300"></p>

If the commit use the convention "Release:", grawkit generates a specific display for this commit.

## License

All code in this repository is covered by the terms of the MIT License, the full text of which can be found in the LICENSE file.

[orthogonal-git]: https://deuill.org/post/orthogonal-git-workflow/
[license-url]: https://github.com/deuill/grawkit/blob/master/LICENSE
[license-svg]: https://img.shields.io/badge/license-MIT-blue.svg
