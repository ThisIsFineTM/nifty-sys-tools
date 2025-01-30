# This is just a list of nifty tools that I've been liking for the moment. No rhyme or reason. Just neat stuff.

## Misc tools

### [ranger](https://github.com/ranger/ranger)

> ranger is a console file manager with VI key bindings. It provides a minimalistic and nice curses interface with a view on the directory hierarchy. It ships with rifle, a file launcher that is good at automatically finding out which program to use for what file type.

https://ranger.github.io/

### [pixz](https://github.com/vasi/pixz)

> The existing XZ Utils provide great compression in the .xz file format, but they produce just one big block of compressed data. Pixz instead produces a collection of smaller blocks which makes random access to the original data possible. This is especially useful for large tarballs.

More command-line friendly than 7z and allows for quick individual file extraction.

https://github.com/vasi/pixz/releases

### [zstd](https://github.com/facebook/zstd)

> Zstandard, or zstd as short version, is a fast lossless compression algorithm, targeting real-time compression scenarios at zlib-level and better compression ratios. 

General purpose compression and my go-to for general use. Good balance between ratio and speed. Currently doesn't have indexing for tar files like what pixz provides.

https://github.com/facebook/zstd/releases

Ships with most package managers. Peazip also supports it.

### [zpaq](https://mattmahoney.net/dc/zpaq.html)

> zpaq is a free and open source incremental, journaling command-line archiver for Windows, Linux and Mac OS/X.

If you don't mind waiting a while, `zpaq -m5` can give some bonkers compression ratios that can blow zstd and xz out of the water, but it is *slow*. Good for stuff you want to keep but don't plan on needing quickly.

Ships in fedora's package manager at least.

### [grub-btrfs](https://github.com/Antynea/grub-btrfs)

> grub-btrfs improves the grub bootloader by adding a btrfs snapshots sub-menu, allowing the user to boot into snapshots. grub-btrfs supports manual snapshots as well as snapper, timeshift, and yabsnap created snapshots.

Note: Read the instructions and check the script. Some paths need to be updated to match your system.

https://github.com/Antynea/grub-btrfs/releases

### [jomt](https://github.com/gaujay/jomt)

> Visualization tool for Google benchmark results.

https://github.com/gaujay/jomt/releases

### [lynis](https://github.com/CISOfy/Lynis)

> Lynis is a battle-tested security tool for systems running Linux, macOS, or Unix-based operating system. It performs an extensive health scan of your systems to support system hardening and compliance testing. The project is open source software with the GPL license and available since 2007.

https://cisofy.com/lynis

### [mold](https://github.com/rui314/mold)

> mold is a faster drop-in replacement for existing Unix linkers.

https://github.com/rui314/mold/releases

### [ncdu](https://dev.yorhel.nl/ncdu)

> Ncdu is a disk usage analyzer with a text-mode user interface. It is designed to find space hogs on a remote server where you don’t have an entire graphical setup available, but it is a useful tool even on regular desktop systems. Ncdu aims to be fast, simple, easy to use, and should be able to run on any POSIX-like system.

### [compsize](https://github.com/kilobyte/compsize)

> compsize takes a list of files (given as arguments) on a btrfs filesystem and measures used compression types and effective compression ratio.

### [dnscrypt-proxy](https://github.com/DNSCrypt/dnscrypt-proxy)

> A flexible DNS proxy, with support for modern encrypted DNS protocols such as DNSCrypt v2, DNS-over-HTTPS, Anonymized DNSCrypt and ODoH (Oblivious DoH).

I'll get around to posting my configs for this eventually.

https://github.com/DNSCrypt/dnscrypt-proxy/releases

## Rust-based tools (in vaguely alphabetical order)

### [cargo-install-update](https://github.com/nabijaczleweli/cargo-update)

> A cargo subcommand for checking and applying updates to installed executables.

```sh
cargo install cargo-update
```

### [cargo-cache](https://github.com/matthiaskrgr/cargo-cache)

> Display information on the cargo cache (~/.cargo/ or $CARGO_HOME). Optional cache pruning.

```sh
cargo install cargo-cache
```

### [afltriage](https://github.com/quic/AFLTriage)

> AFLTriage is a tool to triage crashing input files using a debugger. It is designed to be portable and not require any run-time dependencies, besides libc and an external debugger. It supports triaging crashes generated by any program, not just AFL, but recognizes AFL directories specially, hence the name.

```sh
git clone https://github.com/quic/AFLTriage
cargo install
```

### [arx](https://github.com/jubako/arx)

> Arx is a high-performance file archive format built upon the Jubako container format. It offers a compelling alternative to traditional archive formats like zip and tar, providing significant speed advantages, especially for large archives and random access operations. Arx archives can even be mounted as read-only filesystems.

I've been shopping around for something indexed like pixz/7z but with more flexibility. This fits that bill rather nicely. It's a nice middle-ground between tar and squashfs. Seems to do better than squashfs compressing clang. arx/sqfs/tar compressed at zstd:22.
```
5.9G clang-19.1.0
1.9G clang-19.1.0 [compsize btrfs force-compress=zstd:4]
1.3G clang-19.1.0.arx
1.6G clang-19.1.0.sqfs
969M clang-19.1.0.tar.zst
```

```sh
cargo install arx
```

### [ast-grep](https://github.com/ast-grep/ast-grep)

> ast-grep(sg) is a CLI tool for code structural search, lint, and rewriting.

```sh
cargo install ast-grep --locked
```

### [bandwhich](https://github.com/imsnif/bandwhich)

> This is a CLI utility for displaying current network utilization by process, connection and remote IP/hostname.

```sh
cargo install bandwhich
```

### [bat](https://github.com/sharkdp/bat)

> A cat(1) clone with wings.

```sh
cargo install bat
```

### [binsider](https://github.com/orhun/binsider)

> Binsider can perform static and dynamic analysis, inspect strings, examine linked libraries, and perform hexdumps, all within a user-friendly terminal user interface!

https://binsider.dev/

```sh
cargo install binsider
```

### [blake3/b3sum](https://github.com/BLAKE3-team/BLAKE3)

Really really fast cryptographic hashing. SIMD and parallel. Made it to the final round of the NIST hash function competition. 

Large file hashing from a ramdisk normalized to b3sum:
| hash | normalized time |
| -- | -- |
| b3     | 1.00  | 
| md5    | 26.10 |
| xxh    | 2.59  |
| xxh64  | 2.59  |
| xxh128 | 1.66  |
| sha1   | 11.90 |
| sha256 | 12.60 |
| sha512 | 23.11 |
| sha3   | 62.13 |
| crc32  | 3.08  |


```sh
cargo install b3sum
```

### [bottom/btm](https://github.com/ClementTsang/bottom)

> A customizable cross-platform graphical process/system monitor for the terminal.
Supports Linux, macOS, and Windows. Inspired by gtop, gotop, and htop. 

```sh
cargo install bottom --locked
```

### [git-delta/delta](https://github.com/dandavison/delta)

Fancy git diff viewer with line numbers and highlighting. 

```sh
cargo install git-delta
```

`.gitconfig`:
```gitconfig
[core]
    pager = delta

[interactive]
    diffFilter = delta --color-only

[merge]
    conflictstyle = zdiff3

[delta]
    navigate = true    # use n and N to move between diff sections
    line-numbers = true
    hyperlinks = true
    side-by-side = true
    true-color = always
    dark = true
```

### [dust](https://github.com/bootandy/dust)

> du + rust = dust. Like du but more intuitive.

```sh
cargo install du-dust
```

### [fclones](https://github.com/pkolaczk/fclones)

> fclones is a command line utility that identifies groups of identical files and gets rid of the file copies you no longer need. It comes with plenty of configuration options for controlling the search scope and offers many ways of removing duplicates. For maximum flexibility, it integrates well with other Unix utilities like find and it speaks JSON, so you have a lot of control over the search and cleanup process.

```sh
cargo install fclones
```

### [fd-find/fd](https://github.com/sharkdp/fd)

> fd is a program to find entries in your filesystem. It is a simple, fast and user-friendly alternative to find. While it does not aim to support all of find's powerful functionality, it provides sensible (opinionated) defaults for a majority of use cases.

```sh
cargo install fd-find
```

### [fend](https://github.com/printfn/fend)

> fend is an arbitrary-precision unit-aware calculator.

```sh
cargo install fend
```

### [fselect](https://github.com/jhspetersson/fselect)

> Find files with SQL-like queries.

```sh
cargo install fselect
```

### [gitui](https://github.com/extrawurst/gitui)

> GitUI provides you with the comfort of a git GUI but right in your terminal.

```sh
cargo install gitui --locked
```

### [gping](https://github.com/orf/gping)

> Ping, but with a graph.

```sh
cargo install gping
```

### [grex](https://github.com/pemistahl/grex)

> grex is a library as well as a command-line utility that is meant to simplify the often complicated and tedious task of creating regular expressions. It does so by automatically generating a single regular expression from user-provided test cases. The resulting expression is guaranteed to match the test cases which it was generated from.

```sh
cargo install grex
```

### [hexyl](https://github.com/sharkdp/hexyl)

> hexyl is a hex viewer for the terminal. It uses a colored output to distinguish different categories of bytes (NULL bytes, printable ASCII characters, ASCII whitespace characters, other ASCII characters and non-ASCII).

```sh
cargo install hexyl
```

### [httm](https://github.com/kimono-koans/httm)

> httm prints the size, date and corresponding locations of available unique versions (deduplicated by modify time and size) of files residing on snapshots, but can also be used interactively to select and restore files, even snapshot mounts by file! httm might change the way you use snapshots (because ZFS/BTRFS/NILFS2 aren't designed to find unique file versions) or the Time Machine concept (because httm is very fast!).

```sh
cargo install httm
```

### [hyperfine](https://github.com/sharkdp/hyperfine)

> A command-line benchmarking tool.

```sh
cargo install hyperfine
```

### [jql](https://github.com/yamafaktory/jql)

> jql - JSON Query Language - is a fast and simple command-line tool to manipulate JSON data.

Benchmarks vs `jq`: https://github.com/yamafaktory/jql/blob/main/PERFORMANCE.md

```sh
cargo install jql
```

### [lowcharts](https://github.com/juan-leon/lowcharts)

> Tool to draw low-resolution graphs in terminal. lowcharts is meant to be used in those scenarios where we have numerical data in text files that we want to display in the terminal to do a basic analysis.
 
```sh
cargo install lowcharts
```

### [mdbook](https://github.com/rust-lang/mdBook)

> Creates a book from markdown files

```sh
cargo install mdbook
```

### [mdcat](https://github.com/swsnr/mdcat)

> Fancy cat for Markdown

```sh
cargo install mdcat
```

### [nushell/nu](https://github.com/nushell/nushell)

> Nu draws inspiration from projects like PowerShell, functional programming languages, and modern CLI tools. Rather than thinking of files and data as raw streams of text, Nu looks at each input as something with structure. For example, when you list the contents of a directory what you get back is a table of rows, where each row represents an item in that directory. These values can be piped through a series of steps, in a series of commands called a 'pipeline'.

Everything is a structured query. Has built-in support for lots of data formats. Its like fish, sql, and ipython had a baby.

```sh
cargo install nu
```

### [oxipng](https://github.com/shssoichiro/oxipng)

> Oxipng is a multithreaded lossless PNG/APNG compression optimizer. It can be used via a command-line interface or as a library in other Rust programs.

```sh
cargo install oxipng
```

### [oxker](https://github.com/mrjackwills/oxker)

> A simple tui to view & control docker containers

```sh
cargo install oxker
```

### [pastel](https://github.com/sharkdp/pastel)

> pastel is a command-line tool to generate, analyze, convert and manipulate colors. It supports many different color formats and color spaces like RGB (sRGB), HSL, CIELAB, CIELCh as well as ANSI 8-bit and 24-bit representations.

```sh
cargo install pastel
```

### [pipr](https://github.com/Elkowar/pipr)

> Pipr uses bubblewrap to execute your command in an isolated, read-only environment.

Construct chained shell commands in an interactive bubblewrapped sandbox so you can dry run your `rm` commands.

```sh
cargo install pipr
```

### [ripgrep/rg](https://github.com/BurntSushi/ripgrep)

> ripgrep is a line-oriented search tool that recursively searches the current directory for a regex pattern. By default, ripgrep will respect gitignore rules and automatically skip hidden files/directories and binary files.

```sh
cargo install ripgrep
```

### [rnr](https://github.com/ismaelgv/rnr)

> RnR is a command-line tool to securely rename multiple files and directories that supports regular expressions. 

```sh
cargo install rnr
```

### [systemd-hardening-helper/shh](https://github.com/desbma/shh)

> Automatic systemd service hardening guided by strace profiling.

```sh
git clone https://github.com/desbma/shh
cargo install
```

### [skim/sk](https://github.com/skim-rs/skim)

> It's a general fuzzy finder that saves you time.

fzf alternative.

```
# works with grep
sk --ansi -i -c 'grep -rI --color=always --line-number "{}" .'
# works with ack
sk --ansi -i -c 'ack --color "{}"'
# works with ag
sk --ansi -i -c 'ag --color "{}"'
# works with rg
sk --ansi -i -c 'rg --color=always --line-number "{}"'
# works with bat
rg --files | sk --preview="bat {} --color=always"
```

```sh
cargo install skim
```

### [sniffnet](https://github.com/GyulyVGC/sniffnet)

> Application to comfortably monitor your Internet traffic.

```sh
cargo install sniffnet
```

### [streampager/sp](https://github.com/markbt/streampager)

> streampager is a library that implements a general-purpose pager for browsing streams of data one page at a time.

```sh
cargo install streampager
```

### [sqlx-cli/sqlx](https://github.com/launchbadge/sqlx/tree/main/sqlx-cli)

> SQLx's associated command-line utility for managing databases, migrations, and enabling "offline" mode with sqlx::query!() and friends.

```sh
cargo install sqlx-cli
```

### [tokei](https://github.com/XAMPPRocky/tokei)

> Tokei is a program that displays statistics about your code. Tokei will show the number of files, total lines within those files and code, comments, and blanks grouped by language.

```sh
cargo install --git https://github.com/XAMPPRocky/tokei.git tokei
```

### [xh](https://github.com/ducaale/xh)

> xh is a friendly and fast tool for sending HTTP requests. It reimplements as much as possible of HTTPie's excellent design, with a focus on improved performance.

```sh
cargo install xh --locked
```

### [zellij](https://github.com/zellij-org/zellij)

> Zellij is a workspace aimed at developers, ops-oriented people and anyone who loves the terminal. Similar programs are sometimes called "Terminal Multiplexers".

Tmux alternative.

```sh
cargo install --locked zellij
```

### [zoxide/z](https://github.com/ajeetdsouza/zoxide)

> zoxide is a smarter cd command, inspired by z and autojump. It remembers which directories you use most frequently, so you can "jump" to them in just a few keystrokes.

```sh
cargo install zoxide --locked
```

In `.bashrc`: `eval "$(zoxide init bash)"`


