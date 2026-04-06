# xit

`xit` posts to X through the Firefox web UI using a persistent browser profile per account.

This repo targets Termux and Firefox/geckodriver. Login is done in a normal visible Firefox window, then later posts can reuse that saved session in visible or headless mode.

## Requirements

- Python 3.12+
- Firefox
- `geckodriver`
- `selenium`
- Termux:X11 for visible login on Android/Termux

Install Python dependency:

```bash
pip install -r requirements.txt
```

## Usage

First login:

```bash
./xit auth your_username
```

After that, post visibly:

```bash
./xit your_username --post "hello"
```

Or reuse the cached session headlessly:

```bash
./xit your_username --post "hello" --headless
```

Inspect cached profile status:

```bash
./xit your_username
./xit list
```

Remove a cached profile:

```bash
./xit logout your_username
```

Rename a cached profile:

```bash
./xit nickname old_name new_name
```

## Notes

- Cached Firefox session data is stored under `.xprofiles/<profile>/firefox`.
- Headless mode only works after a visible login has already been cached.
- If `DISPLAY` is missing, `xit` tries to start Termux:X11 automatically.
- Sites can still invalidate sessions or change UI selectors; this tool depends on the current X web app structure.
