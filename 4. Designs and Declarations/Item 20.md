#### Item 20: Prefer *pass-by-reference-to-const* to *pass-by-value*.

1. By default in C and C++ objects are passed by value to and from function unless specified otherwise. A new copy of passed by value object is created for the function to work and the original copy at the caller remains unchanged.

2. 