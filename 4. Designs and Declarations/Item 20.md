#### Item 20: Prefer *pass-by-reference-to-const* to *pass-by-value*.

1. By default in C and C++ objects are passed by value to and from function unless specified otherwise. Function arguments are initialised with new copies of parameters passed and the function caller gets a new copy of the value returned by the function. This happes throguh respective copy constructors which is an expensive operations.

2. If a class has other user-defined type objects as its member, pass by value will cause calls to the copy constructors of those types as well.

3. Pass by reference doesn't involve any copy creation, i.e. any call to constructor, destructor, copy functions(copy constructor or assignment operator) because there is no new copy being created. To ensure that the object doesn't gets changed unintentonally by the function, use `const` reference.

4. Passing objects by reference also avoids the slicing problem which occur when a derived class object is assigned to its base class object.

5. When we have objects of built in types, its more efficient to pass them by value. The same advice goes for STL iterators and function objects.

6. A small object might have a heavy copy constructor may become large as part of code changes over a perriod of time, so always use pass by reference, except for built in types, STL iterators and function objects.