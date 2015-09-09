#### Item 15: Provide access to raw resource in resource-managing classes.

1. At times we need to deal with raw pointer to the resource. For such situations `std::auto_ptr` and `std::shared_ptr` provide a `get()` member function to return the raw pointer inside the RAII object.

2. Smart pointer class like `std::auto_ptr` and `std::shared_ptr` have overloaded pointer dereferencing operators(operator -> and operator *).

3. While creating your own RAII class be sure to provide access to the raw pointer to the resource. That is converting the RAII object into raw resource it contains.

4. The implicit way of doing is over loading dereferencing operators(operator -> and operator \*) in your custom RAII class or by providing an implicit conversion function. Despite being convenient implicit conversion increases chances of error.

5. Explicit way of doing is to provide a get function in the RAII class. Safer than implicit conversion.
