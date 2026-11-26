# My Book — updates

<!-- Template for https://github.com/VIMALVISHALM2/my-book-releases (copy to README.md at the top of that repository).
     Kept in My Book's source repository at docs/releases-repo-README.md. -->

This repository holds **only the signed program files** of **My Book**, a shop's gold-and-silver ledger for Windows.
Every installed My Book (1.2.1 and later) looks here about once a day, and when the owner presses
Settings → Check now. If a newer version is here, it is downloaded, checked, and installed the next time My Book
opens — after a backup of the books is saved.

இந்த repository-இல் My Book-இன் கையொப்பமிட்ட program கோப்புகள் மட்டுமே உள்ளன. source code இல்லை, கணக்குகள் இல்லை,
பெயர்கள் இல்லை, எண்கள் இல்லை. My Book இங்கிருந்து புதுப்பிப்பை மட்டுமே பதிவிறக்கும்; கணக்கிலிருந்து எதுவும் ஒருபோதும்
அனுப்பப்படாது.

## What is here

| File | What it is |
|---|---|
| `latest.json` | The newest version's list: its number, its notes (Tamil and English), and the size and SHA-256 of its program file. |
| `latest.json.sig` | The signature of that list, made with My Book's own update key. |
| `<version>/app.asar` | The program's code for that version. |
| `<version>/manifest.json` and `<version>/manifest.json.sig` | The same signed list, kept with its version. |

Nothing else belongs here. The release tool refuses to publish from a folder that holds anything but these files, a
`README.md`, a `.gitattributes` and a `.gitignore`.

## What is never here

- **No source code.** The source lives in a separate, private repository.
- **No books, no backups, no names, no figures.** A shop's book never leaves its own computer. When My Book looks for
  an update it only downloads: it sends nothing from the book — no names, no weights, no amounts, no cookies, no login.
- **No keys.** The signing key stays sealed on the maker's PC. My Book carries only the public half.

## Why it is safe for this repository to be public

Every list here is signed with My Book's own update key (Ed25519). An installed My Book uses an update only when:

1. the signature of `latest.json` is right (anything else is not even read),
2. the list says it is for My Book (another program's update is refused),
3. the version is newer than the one it runs, and was not tried and failed before,
4. the program file is exactly the size and SHA-256 the signed list says (and it is checked again at every start),
5. a backup of the books was saved first (no backup, no update).

If the new version does not start, the last good one runs and that version is never tried again. Anyone can read this
repository; nobody without the key can make My Book run anything from it.

## How a version gets here

Only from the maker's PC, with My Book's release tool (it signs, checks the signature with the key inside the app,
writes the files above, commits, checks that git kept every byte as signed, and pushes):

```
node tools/release.js --repo C:\Projects\my-book-releases --notes notes.json --push
```

The same tool with `--out <folder>` (and never `--push`) writes the same files into a folder for a pen drive
(Settings → Update from a file).

## Keep the bytes exactly as signed

This repository has a `.gitattributes` with one line, so git never changes a line ending in a signed file:

```
* -text
```
