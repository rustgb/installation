# installation

Documentation on how to compile.
*This assumes Linux. It's not even tested on WSL, let alone bare Windows. Sorry.*

- `git submodule update`
- Install [sdcc](https://sdcc.sourceforge.net/); the source code assumes you install it to a folder named `/opt/sdcc`, and that `/opt/sdcc/bin/sdldgb` is valid.
- **llvm-gbz80**
    - `cd llvm-gbz80/tools`
    - `ln -s ../../clang-gbz80 clang`
    - `cd ../`
    - `mkdir build`
    - `cd build`
    - `cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Debug -DLLVM_TARGETS_TO_BUILD="GBZ80" ..`
    - `make llc clang -j$(nproc)`
    - `mkdir /opt/z80llvm`
    - `cp bin docs include lib /opt/z80llvm -r`
- **rust-lang**
    - `cd rust`
    - `./x.py setup`; you want to choose c
    - Add the following to the config.toml:
    
        `[target.z80-gameboy]`

        `llvm-config = "/opt/z80llvm/bin/llvm-config"`
