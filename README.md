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

## __Example__ 1

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

## `rebind` Struct

The `rebind` struct within the allocator class is a template metaprogramming feature that allows users to transform the allocator of one type into the allocator of another related type. This is particularly useful when working with allocators in generic programming scenarios.

### Usage

When you need to allocate memory for a different type using the same allocator, you can use the `rebind` struct. It is a nested template within the allocator that takes a template parameter representing the new type you want to allocate.

For example, assuming you have an allocator for `T`, you can use `rebind` to create an allocator for `U`:

## __Example__ 2
```CPP
#include "./../lib/allocator/allocator.hh"

using cc_tokenizer::allocator;

template <typename T = float>
class foo {

    T num;

    public:
        foo(T n) : num(n)
        {
            // Using rebind to create an allocator for type char
            typename allocator<T>::template rebind<char>::other charAllocator;
            char* ptr = charAllocator.allocate(10);

            // Perform operations with ptr
            charAllocator.deallocate(ptr, 10);

            std::cout << "Hello World!" << std::endl;
        }
};

int main(int argc, char* argv[])
{
    foo<float> obj(10);

    return 0;
}
```

### License
This project is governed by a license, the details of which can be located in the accompanying file named 'LICENSE.' Please refer to this file for comprehensive information.