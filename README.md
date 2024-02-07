# MKLC

Just a Compiler of Kaleidoscope language with LLVM prject.

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

> This tutorial series requires you are familiar with Modern C++, you can watch [Cherno's C++ playlist](https://www.youtube.com/playlist?list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb) if you are not familiar with Modern C++.

### 1. Kaleidoscope language and Lexer

Extend the error checking of scanning number:

```c++
// Number: [0-9.]+
if (isdigit(LastChar) || LastChar == '.') {
  std::string NumStr;
  bool isdot = false;
  do {
    // error checking: incorrect number
    if (LastChar == '.') {
      if (isdot == true)
        fprintf(stderr, "Error: %s\n", "Invalid number");
      isdot = true;
    }
    NumStr += LastChar;
    LastChar = getchar();
  } while (isdigit(LastChar) || LastChar == '.');

  NumVal = strtod(NumStr.c_str(), 0);
  return tok_number;
}
```

Using a bool flag `isdot` to check if period (.) has benn scanned.

### 2. Implementing a Parser and AST

This chapter uses to many `std::unique_ptr` and `std::move`, if you don't known this, you can watch videos [SMART POINTERS in C++ (std::unique_ptr, std::shared_ptr, std::weak_ptr)][smart-pointers] (for `std::unique_ptr`) and [std::move and the Move Assignment Operator in C++][move] (for `std::move`).

Syntax in this chapter:

```
primary
  ::= identifierexpr
  ::= numberexpr
  ::= parenexpr
identifierexpr
  ::= identifier
  ::= identifier '(' expression* ')'
numberexpr ::= number
parenexpr  ::= '(' expression ')'
```

## References

- [My First Language Frontend with LLVM Tutorial](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/index.html)

[smart-pointers]: https://www.youtube.com/watch?v=UOB7-B2MfwA&list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb&index=43&pp=iAQB
[move]: https://www.youtube.com/watch?v=OWNeCTd7yQE&list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb&index=90&pp=iAQB
