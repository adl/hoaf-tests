# hoaf-tests
A repository of correct and incorrect automata in [HOA format](http://adl.github.io/hoaf/).

You can find the latest version of this repository at https://github.com/adl/hoaf-tests/

## Overview

This collection of automata in the HOA format is intended to provide
 * examples of the various features of the HOA format
 * examples of corner-cases in the format
 * automata that are invalid in specific ways to enabled testing of parsers
 
One aim is to serve as a test suite for HOAF parsers.

## Structure

The automata/ sub-directory contains a variety of automata:

| Directory      | Description / Test Goal                            |
|----------------|----------------------------------------------------|
| format-spec-v1 | Example automata from the format specification     |
| syntax         | Various aspects of the HOA syntax                  |
| acceptance     | Acceptance specifications                          |

The scripts/ sub-directory contains scripts that can be used for
testing parsers and automata translators.

Run
```
  scripts/run-hoa-tests --man
```
to read the manual.

## Automata annotations

To allow for the automated testing of HOAF parsers and manipulation tools,
the automata can be annotated using comments at the start of the file:

```
/** HOA-TEST: VALID */
/** HOA-TEST: INVALID */
/** HOA-TEST: TRICKY */
```

`VALID` signifies that the following automaton should be accepted by a
fully-features HOA parser.

`INVALID` signifies that the following automaton has syntax errors or violates
the HOA format in some other way (e.g. by specifying not applicable properties).
It should be rejected by a fully-featured HOA parser.

`TRICKY` signifies that the following automaton has issues that would justify 
a parser to reject the automaton as invalid. In contrast to `INVALID`, these issues
might be difficult to detect. For example, the automaton might have 
'properties: stutter-invariant' without actually being stutter-invariant, which
requires heavy automata-based algorithms to detect. A fully-featured HOA parser
that does not rely on more advanced analysis algorithms would not be expected
to reject `INVALID` automata.

For `VALID` automata, the language of the automaton can be specified as follows:

```
/** HOA-LANGUAGE(syntax): formula */
```

syntax identifies the syntax of the form, examples would be

| Syntax      | Description                      |
|-------------|----------------------------------|
| `LTL-LBT`   |  formula in LBT(T) prefix format |
| `LTL-SPOT`  |  formula in Spot format          |
| `LTL-SPIN`  |  formula in Spin format          |

By providing the language, tools may attempt to verify that the parsed automaton
actually matches the language.

