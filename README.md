This is an example calculator written in [ANTLR](https://www.antlr.org) and [ASDL](https://github.com/empirical-soft/asdl4cpp) using C++.

Build with CMake:

```
$ mkdir build && cd build
$ cmake ..
$ make -j8
```

Run the resulting binary:

```
$ ./calculantlr
>>> 1+3*5
16
>>> (1+3)*5
20
```

The ANTLR and ASDL components are pre-included in `thirdparty/`, so there is nothing to download. Also, the resulting binary is statically linked, so it can be copied anywhere without further dependencies.

All of the work is in `src/`. The calculator simply parses the user's input into an abstract syntax tree (AST) and then evaluates to compute the result. See the source files for a more thorough explanation.
