# C++ allocator class

## Overview

The `allocator` class provided in this repository is part of the `cc_tokenizer` namespace in C++. It is a template class that specializes in allocating memory for different data types. The allocator supports several predefined types, including `char`, `float`, `double`, `unsigned char`, `int`, `wchar_t`, and `size_t`. 

## Usage:-

### Template Specializations

The allocator is specialized for different data types, and each specialization provides the following public typedefs:

- `value_type`: The type of elements to allocate.
- `pointer`: A pointer to `value_type`.
- `const_pointer`: A const pointer to `value_type`.
- `reference`: A reference to `value_type`.
- `const_reference`: A const reference to `value_type`.
- `size_type`: An unsigned integer type representing the size of allocated memory.
- `difference_type`: A signed integer type representing the difference between two pointers.

### Member Functions

1. **max_size():**
   - Returns the maximum number of elements that the allocator can allocate.

2. **allocate(size_type n):**
   - Allocates memory for `n` elements of type `value_type`.
   - Throws `std::bad_alloc` if the allocation fails.
   - Throws `std::length_error` if the requested allocation size exceeds the maximum size.

3. **deallocate(pointer ptr, size_type n = static_cast<size_type>(0)):**
   - Deallocates the memory pointed to by `ptr`.
   - The optional parameter `n` is ignored and included for compatibility with the standard allocator interface.

## Example

```cpp
#include <iostream>
#include "./../lib/allocator/allocator.hh"

using cc_tokenizer::allocator;

int main(int argc, char* argv[]) {

    allocator<size_t>::pointer ptr;
    
    try {
        ptr = allocator<size_t>().allocate(19);
        allocator<size_t>().deallocate(ptr);
    }
    catch (std::bad_alloc& e) {
        std::cout<< e.what() << std::endl;
    }
    
    return 0;
}
```
### License
This project is governed by a license, the details of which can be located in the accompanying file named 'LICENSE.' Please refer to this file for comprehensive information.