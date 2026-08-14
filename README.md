# VIG project

This is the integration repository for the VIG virtual machine and toolchain.
Each component remains a separate Git repository, while this repository pins a
known-compatible set of component commits and exposes them through one Bazel
workspace.

## Clone

Clone the complete project, including its component repositories:

```sh
git clone --recurse-submodules <integration-repository-url>
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
```

Every component can still be built and tested from its own directory. Bazel's
module boundaries keep imports explicit; the integration repository supplies
only composition, shared entry points, and the compatible-version pin.

## Updating components

Make and commit changes in the component repository first. Then, from this
directory, record the new component commit in the integration repository:

```sh
git add vig-bytecode vig-assembler vig-linker vig vigcc
git commit
```

Only changed submodules need to be added. A component directory marked with
`-dirty` contains uncommitted work that is not captured by the integration
repository's pin.
