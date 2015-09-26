###Item 21: Don't try to return a reference when you must return an object.

1. On the theme of pass by reference, you might be tempted to return by reference.

2. Never return a reference or pointer to a local stack object from a function. As soon as the scope expires(just when you return from function) your reference/pointer will be pointing to an invalid non-existent object/location in memory leading your program to an undefined behaviour.

3. Never return a reference to an object created on heap from a function. This may cause memory leak because the caller will not have a way to call delete/free to release that memory. Although it is fine to return pointer to objects created on heap.

4. Returning reference to local static object will obviously make your function thread unsafe; additionally it will cause every returned reference to point to the same object.

5. Modern compiler carry out optimisations to eliminate the constructor/copy function calls while returning an object by value from a function. Thus it's advised to rely on those facilities. Thus,

		1. Never return a pointer/reference to a local stack object.
		2. Never return a reference to a heap allocated object.
		3. Never return a pointer/reference to a static object if there is a chance
		there more than one such object might be required.
