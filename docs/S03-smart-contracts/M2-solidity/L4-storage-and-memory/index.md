**Notes on the usage of memory:**There are defaults for the storage location depending on which type of variable it concerns:

- State variables are always in storage
- Function arguments are always in memory
- Local variables of struct, array or mapping type reference storage by default
- Local variables of value type (i.e. neither array, nor struct nor mapping) are stored in the stack

For more information on storage vs memory, please see [this article.](https://www.geeksforgeeks.org/storage-vs-memory-in-solidity/)
