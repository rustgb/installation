# rust-z80

Libraries and documentation to get Rust to compile to a Gameboy rom.

**Compilation instructions for clarity:**

Due to the size of these repos - LLVM is 2GB in size - I don't even bother to clone them for what are pretty much minor, if any changes, hence a shell script (and these instructions) to compile this for you.

*This assumes Linux. It's not even tested on WSL, let alone bare Windows. Sorry.*

- Install [sdcc](https://sdcc.sourceforge.net/); the .json file assumes you install it to a folder named `/opt/sdcc` and `/opt/sdcc/bin/sdldgb` is valid.
- Clone [rustgb/llvm-gbz80](https://github.com/Bevinsky/llvm-gbz80)
    - `cd llvm-gbz80/tools`
    - `ln -s ../../clang-gbz80 clang`
    - `cd ../`
    - `mkdir build`
    - `cd build`
    - `cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Debug -DLLVM_TARGETS_TO_BUILD="GBZ80" ..`
    - `make llc clang -j$(nproc)`
- Clone [rust-lang](https://github.com/rust-lang/rust)
    - `cd rust`
    - `./x.py setup`; you want to choose c
    - Add the following to the config.toml:
        `[target.z80-gameboy]`
        `llvm-config = "/opt/z80llvm/bin/llvm-config"`
