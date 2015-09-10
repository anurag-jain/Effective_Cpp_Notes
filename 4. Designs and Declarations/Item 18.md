#### Make interface easy to use correctly and hard to use incorrectly.

1. Introduce new types when using built-in types leaves room for confusion and lead to incorrect usage. For example using int for defining date, month, year to represent date may lead usage errors. It can be mitigated by creating new date, month, year type classes.

2. Enums can sometime be used as int. Beware of undefined behaviour regarding reliable initialization of non-local static objects. Constrain object values and restricts operations on types. e.g. Use `const`.

3. Have your types behave consistently with built in types. When in doubts, do as ints do.

4. Instead of having function return raw pointer, return smart pointer; if required with optional deleter function(only for `std::shared_ptr`). This reduces the chances of client forgetting to clean up the memory when no more needed.

5. `std::shared_ptr` also eliminate cross DLL client problems which arises when an object is created in one DLL and deleted in another DLL. `std::shared_ptr` avoids the problem because its default deleter uses delete from the same DLL where the shared\_ptr is created. This facility can be used to unlock mutexes.
