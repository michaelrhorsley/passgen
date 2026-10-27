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

## PowerShell

`passgen.ps1` is the same generator for Windows PowerShell 5.1 and PowerShell 7+ on Windows, macOS, and Linux. The positional count defaults to 1, and the password format matches `passgen`.

```powershell
./passgen.ps1            # 1 password
./passgen.ps1 5          # 5 passwords
./passgen.ps1 -Count 5   # named parameter
./passgen.ps1 -h         # help (-Help and --help do the same)
Get-Help ./passgen.ps1 -Full
```

Windows often blocks local scripts with its execution policy. Either of these runs the file once and leaves the machine policy unchanged:

```powershell
powershell -ExecutionPolicy Bypass -File .\passgen.ps1
pwsh -ExecutionPolicy Bypass -File ./passgen.ps1
```

For the rest of the current session only:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Passwords are written to the success output stream only. The script does not save them to a file.

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
- `passgen.ps1` uses `System.Security.Cryptography.RandomNumberGenerator` and rejection sampling (not `Get-Random` or `System.Random`).
- The 2048-word BIP39 list is embedded directly in the script — no external files are read at runtime.
