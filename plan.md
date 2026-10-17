retro-uninstaller/
├── Cargo.toml                  # deps + [profile.release]
├── Cargo.lock
├── Makefile                    # build/install/test/lint wrappers
├── rust-toolchain.toml         # pin the stable toolchain
├── rustfmt.toml
├── clippy.toml
├── LICENSE
├── README.md
├── install.sh
├── .gitignore
│
├── src/
│   ├── main.rs                 # thin: parse args, call lib::run(), map Err -> exit code
│   ├── lib.rs                  # `pub mod` list + run()  (makes it testable)
│   ├── cli.rs                  # clap derive structs + subcommand enum
│   ├── error.rs                # thiserror enum: RetroError
│   ├── config.rs               # serde structs + toml load
│   │
│   ├── commands.rs             # module root
│   ├── commands/
│   │   ├── purge.rs
│   │   ├── tree.rs
│   │   ├── scan.rs
│   │   ├── clean.rs
│   │   ├── restore.rs
│   │   └── version.rs
│   │
│   ├── pkgmanager.rs           # trait PackageManager + detect()
│   ├── pkgmanager/
│   │   ├── pacman.rs
│   │   ├── apt.rs
│   │   ├── dnf.rs
│   │   ├── zypper.rs
│   │   ├── flatpak.rs
│   │   ├── snap.rs
│   │   └── standalone.rs
│   │
│   ├── scanner.rs              # orchestrator + heuristics
│   ├── scanner/
│   │   ├── xdg.rs              # ~/.config, ~/.local/share, ~/.cache
│   │   ├── sandbox.rs          # ~/.var/app, ~/snap
│   │   ├── system.rs           # /etc, /var, /opt
│   │   ├── desktop.rs          # .desktop launchers + icons
│   │   └── systemd.rs          # user units
│   │
│   ├── safety.rs               # whitelist + per-path validation
│   │
│   ├── backup.rs               # tar.gz rollback create + restore
│   │
│   ├── disktree.rs             # tree model + ASCII render
│   ├── disktree/
│   │   └── size.rs             # walkdir + human KB/MB/GB
│   │
│   └── ui.rs                   # theme + output + prompt
│   └── ui/
│       ├── theme.rs            # retro-green, amber, cyber, plain
│       ├── output.rs           # [*] [+] [★] banners
│       ├── prompt.rs           # dialoguer/inquire Y/n/select
│       └── tui.rs              # ratatui — roadmap item
│
├── tests/                      # integration tests (assert_cmd + predicates)
│   ├── cli.rs
│   └── purge.rs
├── testdata/                   # fake ~/.config / ~/.cache trees
│
├── .github/workflows/
│   ├── ci.yml
│   └── release.yml
│
└── packaging/
    ├── aur/PKGBUILD
    ├── deb/
    ├── rpm/retro-uninstaller.spec
    └── goreleaser? no -> cargo-dist.toml   # Rust cross-compile release tool
