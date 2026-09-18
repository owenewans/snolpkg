<div align="center">

# snolpkg

signed native module installer for [SNOLC](https://github.com/owenewans/snolc).

`rust` `packages` `ed25519`

</div>

## build

```sh
cargo build --locked --release
cargo test --locked
```

Rust 1.98.1 and `Cargo.lock` define the build.

## setup

```sh
install -d -m 700 "$HOME/.local/share/snolc/packages"
cp config/snolpkg.toml config/sources.toml "$HOME/.local/share/snolc/packages/"
export SNOLPKG_ROOT="$HOME/.local/share/snolc/packages"
```

## usage

```sh
snolpkg add -b https://github.com/owenewans/snolc-modules.git carrier-tcp
snolpkg add -s https://github.com/owenewans/snolc-modules.git carrier-tcp
snolpkg template owenewans/carrier-tcp@0.0.2 --role server --output modules/tcp.toml
snolpkg del owenewans/carrier-tcp@0.0.2
```

Binary mode verifies the source manifest signature, artifact byte count and
SHA-256. Source mode checks out the signed revision and builds with the pinned
toolchain. The installer never falls back between modes.

## trust

`config/sources.toml` pins each repository and Ed25519 public key. A package
cannot add its own trusted key. The extractor rejects absolute paths, parent
components, links, devices and setuid entries.

## license

[Unlicense](LICENSE)
