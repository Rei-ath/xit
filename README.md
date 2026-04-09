# xit

`xit` posts to X through the Firefox web UI using a reusable profile per account.

Auth now defaults to a localhost capture flow: `xit` starts a small local web page, you paste session data from a logged-in `x.com` browser tab, and `xit` verifies and stores that session for later reuse. This avoids the old hard dependency on a visible Firefox/X11 login window.

## Requirements

- Python 3.12+
- Firefox
- `geckodriver`
- `selenium`

Optional:

- Termux:X11 only if you still want the old visible browser auth flow or visible posting without an existing `DISPLAY`

Install Python dependency:

```bash
pip install -r requirements.txt
```

## Usage

Capture a session locally:

```bash
./xit auth your_username
```

That prints a local URL such as `http://127.0.0.1:8765/`. Open it in any browser, then paste one of these from a logged-in `https://x.com` tab:

- a Network request copied as curl
- a raw `Cookie:` header
- a cookie JSON export
- a Netscape cookie file

After that, post headlessly:

```bash
./xit your_username --post "hello" --headless
```

Or post visibly if you have a working GUI/display:

```bash
./xit your_username --post "hello"
```

Expose the auth page on another interface or device:

```bash
./xit auth your_username --bind 0.0.0.0 --port 8765
```

Use the old visible browser login flow explicitly:

```bash
./xit auth your_username --manual-browser
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

- Cached Firefox data lives under `.xprofiles/<profile>/firefox`.
- Imported session metadata is stored in `.xprofiles/<profile>/meta.json`.
- Headless posting no longer requires a previous GUI login if you captured a valid session through `xit auth`.
- If a stored session expires, run `./xit auth <profile>` again and paste fresh session data.
- UI selectors and session behavior on X can still change and break automation.
