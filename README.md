# tinyhttp-c

A small HTTP server written in C. It listens on `127.0.0.1:8080` and serves a few
static HTML pages from the local `pages/` directory.

## Features

- Handles one request per connection and forks a child process for each client.
- Serves `GET` requests for a fixed set of routes.
- Returns simple HTTP response headers and serves the page contents as HTML.
- Reaps finished child processes so they do not remain as zombies.

## Routes

| Path | Page |
| --- | --- |
| `/` | `pages/index.html` |
| `/index.html` | `pages/index.html` |
| `/about.html` | `pages/about.html` |
| `/contact.html` | `pages/contact.html` |

Only these paths and the `GET` method are accepted. Other requests receive a
`400 Bad Request` response. The server binds to `127.0.0.1` on port `8080`.

## Build

Requirements: a C compiler, [Meson](https://mesonbuild.com/), and
[Ninja](https://ninja-build.org/).

From the project root:

```sh
meson setup build
meson compile -C build
```

This produces the `build/http_server_c` executable.

### Nix development shell

If you use Nix with flakes enabled, enter the provided development environment:

```sh
nix develop
```

Then run the Meson build commands above.

## Run

Start the server from the project root so it can find the `pages/` directory:

```sh
./build/http_server_c
```

The server prints a message when it is ready. Open <http://127.0.0.1:8080/> in
a browser, or make requests with `curl`:

```sh
curl -i http://127.0.0.1:8080/
curl -i http://127.0.0.1:8080/about.html
```

Stop the server with `Ctrl+C`.

## Project layout

```text
include/  Header files
pages/    Static HTML pages served by the server
src/      Server setup, request handling, and main program
```

## License

No license file is currently included in this repository.
