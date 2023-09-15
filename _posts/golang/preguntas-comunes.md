
## Init function

- It is automatically called by the Go runtime when a package is initialized before the `main()` function.
- It is called before the main function and can be used to perform initialization tasks for the package.
- It does not take any arguments and does not return a value.
- It is typically used to set initial values for package-level variables, establish connections.
- It can be defined anywhere in the package, and multiple "init" functions can be defined in the same package. All "init" functions within a package will be called by the Go runtime in the order they appear in the code.
