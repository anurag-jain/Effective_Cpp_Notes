#### Item 17: Store newed objects in smart pointers in standalone statements.

1. In C++, evaluation of arguments passed as function parameters can involve interleaving of various operations. For example, consider the following situation

	`void myFunction(std::shared_ptr<someType>ptr, int arg){...}`

	is called this way

	`myFunction(std::shared_ptr<someType>(new someType), funFunctionReturningInt());`

	The above call consists of three things,
    1. Call  funFunctionReturningInt.
    2. Execute `new someType`
    3. Call `std::shared_ ptr<someType>` constructor.

   There is no particular order defined for execution of the above task in C++ unlike languages like java or C#. Thus there is a chance that `funFunctionReturningInt()` executes second after `new someType` and throws exception leading to  **memory leak**.

2. Thus it's advised to break the above call statement as
	`std::shared_ptr<someType>ptr(new someType);`
    `myFunction(ptr, funFunctionReturningInt());`

    thereby storing newed object in smart pointer in a standalone statement.
