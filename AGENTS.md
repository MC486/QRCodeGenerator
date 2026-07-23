# AGENTS.md

## Cursor Cloud specific instructions

### What this is
Single-file Python CLI: `QRCodeGenerator.py`. It shortens a URL via the TinyURL
API, generates a high-error-correction QR code (`segno`), overlays a logo and a
Mickey-Mouse template (`Pillow`), and logs results to `tinyurl_links.xlsx`
(`openpyxl`). No web server, database, or other long-running services. Python
3.12 is available; deps (`requests`, `segno`, `Pillow`, `openpyxl`) are installed
by the startup update script.

### Running
- Run from the repo root; the script uses relative paths for `mickey_template.png`,
  `sweeping-mickey.png`, and `tinyurl_links.xlsx`.
- It is interactive (`input()` for URL then output filename). Pipe stdin to run
  non-interactively, e.g. `printf 'https://example.com\nmyqr\n' | python3 QRCodeGenerator.py`.

### Gotchas
- `read_auth_token()` reads `tinyurl_auth_token.txt` (git-ignored) and raises
  `FileNotFoundError` if missing. Create a placeholder file to get past this.
- `api.tinyurl.com` is blocked by cloud egress, and `shorten_url_with_tinyurl()`
  only handles non-200 responses (not `ConnectionError`), so the script crashes
  on the network call before doing any local work. To exercise the core image
  pipeline locally, import the module's functions and skip the network call
  (set `shortened_url = data`). To run the real shortening flow, request egress
  allowlisting for `api.tinyurl.com` plus a valid token in `tinyurl_auth_token.txt`
  (with the domain reachable, a bad token returns non-200 and falls back to the
  original URL, so the full `main()` still completes).

### Tests / lint / build
None configured. No test suite, linter, or build step. Smoke check:
`python3 -c "import requests, segno, PIL, openpyxl; print('deps OK')"`.
