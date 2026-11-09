# Awesome Hypereffect [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of projects built with, on top of, or around hypereffect.

[hypereffect](https://hypereffect.dev) is a small protocol for server-guided, reactive interfaces that can be rendered anywhere. A server sends elements and signals, the client draws them with its own native widgets, and actions are the only way back. The same application can be a web page, a terminal UI, a phone screen, or a sandboxed WebAssembly module without shipping HTML, CSS, or a client framework.

This list collects the protocol itself, its renderers, the tools and servers that use it, and the larger applications built on it.

## Contents

- [The protocol](#the-protocol)
- [Renderers](#renderers)
- [Tool collections](#tool-collections)
- [Applications](#applications)
- [Cassis](#cassis)
- [Resources](#resources)

## The protocol

- [hypereffect](https://github.com/hypereffect/hypereffect) - A small protocol for server-guided, reactive interfaces: elements, signals, [CEL](https://cel.dev) expressions, and actions, with implementations in Rust, TypeScript, Go, and Python.

## Renderers

- [hyperb](https://github.com/hypereffect/hyperb) - A standalone browser for hypereffect applications on desktop, Android, terminal, and web. It opens `hyperb://` addresses over HTTP or [iroh](https://iroh.computer), or runs sandboxed WebAssembly modules locally, and ships demo apps such as a focus timer, a grammar checker, a SQL client, and a smart-home console.
  - [desktop](https://github.com/hypereffect/hyperb/tree/master/crates/desktop) - A native browser for Linux, macOS, and Windows, with an address bar, tabs, history, and favorites.
  - [android](https://github.com/hypereffect/hyperb/tree/master/android) - A Kotlin Compose app for Android, backed by the `hyperb-mobile` JNI bridge, with history and favorites.
  - [tui](https://github.com/hypereffect/hyperb/tree/master/crates/tui) - A terminal renderer that shows the single app it was started with, `hyperb-tui <address>`, without an address bar, tabs, history, or favorites.
  - [web](https://github.com/hypereffect/hyperb/tree/master/crates/web) - A browser renderer built with Leptos and compiled to WebAssembly.

## Tool collections

- [hyperwasmtools](https://github.com/hypereffect/hyperwasmtools) - Small, serverless tools packaged as sandboxed WebAssembly modules for hyperb. Each module runs entirely inside the renderer. Published at [hypereffect.github.io/hyperwasmtools](https://hypereffect.github.io/hyperwasmtools/).
  - [qr](https://github.com/hypereffect/hyperwasmtools/blob/master/src/qr.rs) - Generate QR codes. (`hyperb://hypereffect.github.io/hyperwasmtools/wasm-apps/qr.wasm`)
  - [textutils](https://github.com/hypereffect/hyperwasmtools/blob/master/src/textutils.rs) - A pocket knife of small tools for text, data, numbers, encoding, hashing, compression, and more. (`hyperb://hypereffect.github.io/hyperwasmtools/wasm-apps/textutils.wasm`)
  - [worldclock](https://github.com/hypereffect/hyperwasmtools/blob/master/src/worldclock.rs) - Live clocks across time zones, plus a time converter. (`hyperb://hypereffect.github.io/hyperwasmtools/wasm-apps/worldclock.wasm`)
  - [finance](https://github.com/hypereffect/hyperwasmtools/blob/master/src/finance.rs) - An RPN financial calculator in the spirit of the HP-12C, with time-value-of-money keys, cash flows, NPV, and IRR. (`hyperb://hypereffect.github.io/hyperwasmtools/wasm-apps/finance.wasm`)
  - [billsplit](https://github.com/hypereffect/hyperwasmtools/blob/master/src/billsplit.rs) - Split a bill: each person has a share and what they paid, and the remaining amount updates as you edit. (`hyperb://hypereffect.github.io/hyperwasmtools/wasm-apps/billsplit.wasm`)
  - [wordle](https://github.com/hypereffect/hyperwasmtools/blob/master/src/wordle.rs) - Guess the five-letter word in six tries, with proper repeated-letter scoring. (`hyperb://hypereffect.github.io/hyperwasmtools/wasm-apps/wordle.wasm`)

  In a plain browser, any of these opens through the [hyperb web renderer](https://hypereffect.github.io/hyperb/) by passing its address as `link`, such as [qr](https://hypereffect.github.io/hyperb/?link=hyperb%3A%2F%2Fhypereffect.github.io%2Fhyperwasmtools%2Fwasm-apps%2Fqr.wasm).

- [hyperutils](https://github.com/hypereffect/hyperutils) - Self-hosted, single-purpose servers for everyday coordination problems. Every server is one hypereffect app, served over HTTPS with Server-Sent Events or over iroh, and sees callers as sessions whose public key proves their identity.
  - [bbs](https://github.com/hypereffect/hyperutils/tree/master/crates/bbs) - An old-school bulletin board with message boards, mail, and teleconference. (`hyperb://ff17a00e374e8f7e0bded3b91a0a0c7c43e8695cf61c8cda223b80e822aa57b2`)
  - [meet](https://github.com/hypereffect/hyperutils/tree/master/crates/meet) - A Doodle-style scheduler: share a code, mark the times that suit you, and watch everyone's answers update live. (`hyperb://meet.hypereffect.dev`)
  - [forms](https://github.com/hypereffect/hyperutils/tree/master/crates/forms) - Build a form, share it, and read the answers as they come in; forms can expire after a day to a month. (`hyperb://forms.hypereffect.dev`)
  - [tournament](https://github.com/hypereffect/hyperutils/tree/master/crates/tournament) - Round-robin fixtures and standings for a league or group, with one link for entering results and one for following along. (`hyperb://tournament.hypereffect.dev`)
  - [signup](https://github.com/hypereffect/hyperutils/tree/master/crates/signup) - Sign-up sheets for roles or things to bring, with every entry attributed to the person who wrote it. (`hyperb://signup.hypereffect.dev`)

  In a plain browser, any of these opens as `https://hypereffect.github.io/hyperb/?link=hyperb%3A%2F%2F<host>`, such as [meet](https://hypereffect.github.io/hyperb/?link=hyperb%3A%2F%2Fmeet.hypereffect.dev).

## Applications

- [flipflop](https://github.com/andunieee/flipflop) - A peer-to-peer app for desktop and Android where groups share files, texts, a scratchpad, and WebAssembly app tabs as Automerge documents over iroh. Includes LAN, QR, and Bluetooth LE discovery, a Bluetooth transport, and browser-based guest links.
- [ribolita](https://github.com/andunieee/ribolita) - A local-first host for small WebAssembly programs. Each program keeps its own state, describes its interface with hypereffect, and syncs entries with peers through range-based set reconciliation. Ships as a Kotlin Multiplatform app with a CLI and a server.
- [garden](https://github.com/andunieee/garden) - A Blossom file server where files stay alive as long as someone keeps paying for them: nostr-keyed accounts, Arkade payments, per-file rent, B2/S3/R2 storage backends, and a hyperb operator dashboard.
- [Grassline](https://github.com/andunieee/grassline) - Run Claude Code, opencode, Codex, and other coding agents on your own computer and talk to them from your phone over iroh. Includes a lightweight Rust daemon, an Android app, and a hyperb admin dashboard.
- [Cathode](https://github.com/andunieee/cathode) - A YouTube client for the desktop with search, a queue, automatic downloads for offline playback, chapters and subtitles, plus a phone remote control built with iroh and hyperb.

## Cassis

- [Cassis Order Protocol](https://github.com/cassiscash/cassis_order_protocol) - A specification for streaming an order page from a merchant to a customer's wallet over iroh and getting paid at the end. It extends hypereffect with `invoice` and `invoicerequest` messages, connection URIs, and resumable orders.
- [cassis-routerd](https://github.com/cassiscash/cassis/tree/master/cassis-routerd) - A Cassis router daemon that opens the configured networks, routes and announces hops, and keeps wallets refreshed. Supports Arkade, Lightning, Cashu, Fedimint, Liquid, Rootstock, Bitcoin, and Bark through cargo features, and serves a hyperb admin interface.

## Resources

- [`hypereffect` on crates.io](https://crates.io/crates/hypereffect) - The Rust crate for building servers and renderers.
- [`hypereffect` on npm](https://www.npmjs.com/package/hypereffect) - The TypeScript package for servers and renderers.
- [`hypereffect-ui` on PyPI](https://pypi.org/project/hypereffect-ui/) - The Python package for servers and a renderer client.
- [Go package](https://pkg.go.dev/github.com/hypereffect/hypereffect/go) - Go servers and a renderer client.

## Contributing

Contributions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

In short: add one item per pull request, keep descriptions short and factual, link to a maintained project that uses or extends hypereffect, and make sure every link works.

Released under [CC0 1.0](LICENSE).
