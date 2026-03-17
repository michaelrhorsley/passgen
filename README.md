# passgen

A command-line password generator that builds secure, memorable passwords from the [BIP39 wordlist](https://github.com/bitcoin/bips/blob/master/bip-0039/english.txt).

## Password Format

```
{special}{UPPER}.{word}.{word}.{word}.{word}.{word}.{word}.{4 digits}
```

Example output:

```
%V.drink.response.ladder.cannon.sun.board.6259
```

| Component | Description |
|-----------|-------------|
| `special` | One random character from `! @ # $ % ^ & *` |
| `UPPER`   | One random uppercase letter (I and O excluded) |
| `words`   | Six random words from the 2048-word BIP39 list |
| `digits`  | Random number between 1000 and 9999 |

## Usage

```bash
passgen [count]
```

```bash
./passgen          # generate 1 password
./passgen 5        # generate 5 passwords
./passgen --help   # show help
```

## Installation

Clone the repo and make the script executable (or run it directly with Python 3):

```bash
git clone <repo-url> && cd passgen
chmod +x passgen
./passgen
```

No dependencies beyond the Python 3 standard library.

## Security

- All randomness is generated using Python's `secrets` module, which provides cryptographically secure random numbers.
- The 2048-word BIP39 list is embedded directly in the script — no external files are read at runtime.
