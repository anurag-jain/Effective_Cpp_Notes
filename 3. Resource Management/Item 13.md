#### Item 13: Use objects to manage resources.

1. So that you don’t forget to release dynamically allocated memory and release resources like locks, file descriptors, sockets, db connection etc.

2. Idea is to put the heap allocated object inside a class and use the stack allocated object of this class to manage the encapsulated resource. Thus when the scope of managing object expires, its destructor will release the resource.

3. `std::auto_ptr`  and `std::shared_ptr` are general purpose smart pointers in standard library.

4. RAII - Resource Acquisition Is Initialization i.e. resources are acquired and immediatedly turned over to resource managing objects. Resource acquisition and initialization of resource managing object happens in same statement as below.

    `std::auto_ptr<SomeClass> pSmartPtr(new SomeClass());`

5. Resource managing object use its destructor to ensure resource are released. Make sure the destructor don't throw exceptions.

6. Because auto\_ptr deletes what it points to when it's destroyed; thus there can't be more than one auto\_ptr pointing to an object. You know what'd happen when one of them does delete. Thus auto\_ptr does ownership transfer upon copy or assignment; setting the old object to null.

7. Containers of auto\_ptr are not possible because the unusual copying behaviour of auto\_ptr will invalidate the copying behaviour of the container class.

8. Reference Counting smart pointer keep track of number of objects pointing to a particular resource and deletes the resource when nobody is pointing to it any longer.`std::shared_ptr` provides this facility. Doesn't support cyclic refenrece.

9. Containers of shared\_ptr are possible because of it copying nature. Thus better choice over auto\_ptr

10. `std::auto_ptr` and `std::shared_ptr` use `delete` in their destructor not `delete[]`. Thus they can't  be used to manage dynamically allocated arrays. See `boost::scoped_array` and `boost::shared_array`.
