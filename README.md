# VIG project

Integration repo for the VIG virtual machine and associated toolchain.
Each component is just a submoule, this repository pins component commits and exposes them through one Bazel
workspace.

## Clone

Clone the complete project, including its component repositories:

```sh
git clone --recurse-submodules https://github.com/TheBozzz34/vig-meta.git
```

For an existing clone:

```sh
git submodule update --init --recursive
```

## Build and test

Run these commands from this directory:

```sh
bazelisk build //:toolchain
bazelisk test //:tests
```

The public commands are also available directly:

```sh
bazelisk run //:vig -- --help
bazelisk run //:vigasm -- --help
bazelisk run //:vigld -- --help
bazelisk run //:vigcc -- --help
bazelisk run //:bench -- loop
bazelisk run //:vigide
```

Every component can also still be built and tested from its own directory.

The workspace is pinned to Bazel 8.4.2, which is compatible with the current
`rules_zig` dependency graph on Windows.
