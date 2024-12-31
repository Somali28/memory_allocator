# memory_allocator

Overview

This project implements a simple memory allocator that mimics the behavior of standard memory allocation functions like malloc(), free(), and realloc(). The allocator manages a fixed-size memory pool and efficiently allocates, deallocates, and resizes memory blocks upon request.

Features

Dynamic Memory Allocation: Provides functions to allocate and free memory at runtime.

Efficient Block Management: Uses strategies to minimize fragmentation and reuse freed blocks.

Resize Capability: Allows for reallocation of memory to adjust block sizes.

Memory Pool: Operates on a fixed-size memory buffer to control allocation limits.

Thread Safety: Optional locking mechanism to ensure safe usage in multi-threaded environments.

Requirements

C/C++ compiler

Standard C library

Compatible with Unix/Linux and Windows environments

Installation

Clone the repository and compile the source files:

$ git clone <repository-url>
$ cd memory-allocator
$ make

Usage

Include the allocator header and initialize the memory pool:

#include "allocator.h"

int main() {
    allocator_init();

    void* ptr = allocator_malloc(128); // Allocate 128 bytes
    ptr = allocator_realloc(ptr, 256); // Resize to 256 bytes
    allocator_free(ptr);               // Free allocated memory

    allocator_destroy();
    return 0;
}

API

allocator_init(size_t size)

Initializes the memory pool with a specified size.

Parameters: size - Size of the memory pool in bytes.

Returns: 0 on success, -1 on failure.

allocator_malloc(size_t size)

Allocates a block of memory of the specified size.

Parameters: size - Size of memory block to allocate.

Returns: Pointer to allocated memory or NULL if allocation fails.

allocator_free(void* ptr)

Frees the allocated memory block pointed to by ptr.

Parameters: ptr - Pointer to memory block to free.

allocator_realloc(void* ptr, size_t size)

Resizes an existing memory block to the new size.

Parameters:

ptr - Pointer to existing memory block.

size - New size of the memory block.

Returns: Pointer to resized memory or NULL if resizing fails.

allocator_destroy()

Frees the entire memory pool and cleans up resources.

Example

#include "allocator.h"

int main() {
    allocator_init(1024); // Initialize with 1KB pool

    int* numbers = (int*) allocator_malloc(10 * sizeof(int));
    for (int i = 0; i < 10; i++) {
        numbers[i] = i * i;
    }

    numbers = (int*) allocator_realloc(numbers, 20 * sizeof(int));
    for (int i = 10; i < 20; i++) {
        numbers[i] = i * i;
    }

    allocator_free(numbers);
    allocator_destroy();

    return 0;
}

Testing

Run unit tests to verify the allocator:

$ make test

