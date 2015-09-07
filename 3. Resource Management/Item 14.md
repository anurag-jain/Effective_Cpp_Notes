#### Item 14: Think Carefully about copying behavior in resource-managing classes.

1. There are times when we have to deal with resource which are not heap based. For example, file descriptors, data base connection, locks, network sockets etc. `std::auto_ptr` and `std::shared_ptr` are generally inappropriate.

2. To create custom destructor behaviour like closing locks when critical section is exited, closing db connection, socket or file after IO completion we need to create our own resource managing class.

3. The Copying behaviour can be controlled in following ways.

    - **Prohibit Copying:** At times, in case of synchronisation primitives we don't want copies of lock. Thus RAII objects can be make uncopyable. See Item 6.
    - **Reference Count the underlying object:** Sometime we want the resource to be held until last object pointing it. In such case, copying the RAII object increments the count of objects pointing to the resource.

        RAII can implement reference-counting copying behaviour by containing `std::shared_ptr` which also takes optional second argument as "deleter" - a function or function object to be called when the reference count becomes zero. `std::auto_ptr` doesn't have this facility.

    - **Copy underlying resource:** Perform deep copy when multiple independent copies of resource are required. For e.g. `std::string` contains the pointer to heap memory where the characters are located in memory. On copying a `std::string` object, a copy is made of both the pointer as well as the memory pointed by it.

    - **Transfer Ownership of underlying object:** When we want only one RAII object pointing to raw resource, it's desired to transfer the ownership of the resource similar what `std::auto_ptr` does.

4. You should write your own versions of copy constructor and assignment function unless the compiler generated ones do the required thing. In some cases we should support generalised versions of these functions(Item 45).
