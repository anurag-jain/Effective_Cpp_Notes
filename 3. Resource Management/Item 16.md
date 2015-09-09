#### Item 16: Use same form in corresponding use of new and delete.

1. If you allocated a single object using `new` deallocate that using `delete`.

2. If you allocated an array of objects using `new Type[]` deallocate it using `delete[]`.

3. Any deviation from above statement will leade to undefined behaviour. Error memory leak or heap corruption.