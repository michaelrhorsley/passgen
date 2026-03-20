# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Single-file Python 3 CLI tool (`passgen`) that generates passwords using the BIP39 wordlist. No dependencies beyond the standard library. The word list is embedded directly in the script (not read from `BIP39.txt` at runtime).

## Running

```bash
./passgen              # generate 1 password
./passgen 5            # generate 5 passwords
./passgen --help       # show help
```

## Password Format

`{special}{UPPER}.{word}.{word}.{word}.{word}.{word}.{word}.{4digits}`

Example: `%V.drink.response.ladder.cannon.sun.board.6259`

- `special`: one of `!@#$%^&*`
- `UPPER`: one uppercase letter (I and O excluded)
- `words`: 6 random words from the 2048-word BIP39 list
- `digits`: random number 1000–9999

## Notes

- Uses `secrets` module for cryptographically secure randomness
- The word list is the `WORDS` constant embedded in the script (no external files read at runtime)
- No tests, linter, or build system — it's a single executable script
- The script has no function definitions; all logic is at the top level
