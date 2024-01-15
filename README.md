# Just a Compiler of Kaleidoscope language with LLVM prject

## Tips

### 0. Setup

I use [clang-format](https://clang.llvm.org/docs/ClangFormat.html) in this project. Follow this [tutoial](https://blog.csdn.net/chengyq116/article/details/121390536) to setup it.

To put it simply, in Ubuntu/Linux:

```bash
# install clang-format
$ sudo apt update
$ sudo apt install clang-format

# check version and path
$ clang-format --version
$ which clang-format
/usr/bin/clang-format

# create a .clang-format file in this repo
$ cd jack-llvm
$ clang-format -style=llvm -dump-config > .clang-format
```

In VS Code:

1. Install the Clang-format extension.
2. Configure Clang-Format options.
    - Settings -> User -> Clang-Format configuration
    - Settings -> Remote [*] -> Clang-Format configuration
3. Executable: `/usr/bin/clang-format` (just the path of clang-format)

## References

- [My First Language Frontend with LLVM Tutorial](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/index.html)