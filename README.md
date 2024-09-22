## Dashmap No Send

This is a fork of dashmap to aid in debugging deadlocks.

It's easy to accidentally misuse the dashmap crate.

The incorrect usage I'm guilty of is holding a `Ref` type over an await point.

I'm not sure if there's a technical reason this is allowed other then backwards compatibility.

This repo is meant to only be used as a debugging tool so it's not published on crates.io.

The tags in this repo will correspond to the same tag in the original project, but with
the Send and Sync trait implementations removed so that you can use cargo's patch system
to override the dependency.

For example let's say you have a rust project that looks like:

```toml
[package]
name    = "project"
version = "0.1.0"
edition = "2021"

[dependencies]
dashmap = "6.1.0"

[patch.crates-io]
dashmap  = { git = 'https://github.com/richardscollin/dashmap-no-send.git', tag = 'v6.1.0' }
```

This will remove the send bound and hopefully help you find potential problems in your crate.
