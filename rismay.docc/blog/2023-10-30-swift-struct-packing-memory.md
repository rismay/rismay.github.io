# Swift Struct Packing

@Metadata {
  @PageImage(purpose: icon, source: "blog-2023-10-30-swift-struct-packing-memory-icon", alt: "Swift Struct Packing icon")
  @PageImage(purpose: card, source: "blog-2023-10-30-swift-struct-packing-memory-card", alt: "Swift Struct Packing card")
  @PageKind(article)
  @PageColor(blue)
}

@Image(source: "doc-2023-10-30-swift-struct-packing-memory-hero", alt: "Swift Struct Packing hero")

@Image(source: "blog-2023-10-30-swift-struct-packing-memory-hero", alt: "Swift Struct Packing hero")

A look at how Swift structs lay out memory and what it inherits from C.

Tags: Blog, C, Programming, Swift
Date: October 30, 2023

Let's dive into a fascinating topic today - Swift structs and their memory dynamics. In computer programming, particularly in languages like C and C++, "struct packing" refers to the arrangement of data within a struct or structure in memory. The term is often used in the context of memory layout and optimization, especially when dealing with low-level programming and data structures. Swift's struct packing and memory handling inherit some wisdom from the past, particularly from the world of C programming.

## The C Struct

Structs are used to group related data together, and how the elements within a struct are stored in memory can have a significant impact on program performance and memory usage. By default, many compilers will try to align struct members in memory to improve data access performance, which can lead to "padding" or unused bytes between members to meet alignment requirements. For example, consider the following struct in C:

```c
struct Example {
    char a;    // 1 byte
    int b;     // 4 bytes (assuming a typical 32-bit system)
    double c;  // 8 bytes
};
```

In this example, the **`struct Example`** contains a **`char`**, an **`int`**, and a **`double`**. The size of this struct, in total, might be larger than the sum of the sizes of its individual members due to padding introduced for alignment. On a typical 32-bit system, you might find that there is 3 bytes of padding added after the **`char`** member (**`a`**) to ensure that the **`int`** member (**`b`**) is properly aligned to a 4-byte boundary. There may also be additional padding at the end of the struct to ensure that the **`double`** member (**`c`**) is correctly aligned to an 8-byte boundary.

Now, if you were to change the order of the members like this:

```c
struct Example {
    double c;  // 8 bytes
    int b;     // 4 bytes
    char a;    // 1 byte
};
```

The memory layout may change, and the amount of padding introduced may differ. In this case, there might be no padding between the **`double`** and **`int`** members, but there could still be padding at the end to align the **`double`**. The total memory size of the struct could be different due to this change in padding.

So, changing the order of variables in a struct can impact the memory size due to differences in alignment requirements. The exact padding added by the compiler can depend on the specific architecture, compiler settings, and data types used in the struct. To minimize padding and control memory layout, you can use compiler-specific directives or attributes (such as **`__attribute__((packed))`** in GCC) or reorder the struct members strategically based on the alignment requirements of your target system. However, optimizing for memory size may come at the cost of performance, as unaligned access to data can be slower on some architectures.

## Intro to Swift Structs

Before we unravel the magic of struct packing, let's have a quick refresher on what a Swift struct is all about. Imagine a struct as a handy way to bundle related data into a neat package. Each piece of data inside a struct is called a member. Here's a basic example:

```swift
struct Point {
    var x: Double
    var y: Double
}
```

In this example, we've got a struct named `Point` with two `Double` members, `x` and `y`. It's like having a mini-coordinate system in a single entity.

## The Legacy of Memory Layout

Swift doesn't reinvent the wheel when it comes to memory layout and alignment. It takes a page from the C playbook. Every data type has an alignment requirement, specifying how it should line up in memory. For example, `double` usually needs an 8-byte alignment, while `int` might need 4 bytes.

Swift's goal is to make sure each struct member lines up properly. If it has to, it throws in some padding bytes to meet alignment requirements. Padding might sound like a bit of a buzzkill, but it's essential to ensure efficient memory access. I hear that you don't want to deal with the sluggishness of unaligned memory operations.

## Swift's Struct Packing Saga, Inspired by C

Swift aims for optimal memory usage and speedy access, and it carries over some concepts from C. In Swift, the memory layout and alignment of structs are managed by the Swift compiler, and it aims to provide a more predictable and consistent behavior compared to some other programming languages like C and C++. However, Swift structs can still be affected by memory alignment and padding, but the compiler makes efforts to minimize these issues.

Swift automatically aligns struct members according to their types and alignment requirements, just like in other languages. This alignment is designed to optimize access times and ensure memory safety. Swift also provides control over memory layout in the form of compiler attributes and annotations, such as **`@alignment`** and **`@packed`**, which can be used to control alignment and packing if necessary. However, there's room for your input to fine-tune struct packing:

### 1. It's All About Member Order

Just like in C, the order of members in a struct can shake things up in the memory layout. Swift tends to put the larger members upfront to minimize padding. It's like playing a game of Tetris with your data. Take this struct, for instance:

```swift
struct Employee {
    var salary: Double  // 8 bytes
    var employeeID: Int // 4 bytes
}
```

In this struct, `salary` takes the lead to minimize padding, just like how C would do it.

### 2. Go for Slimmer Data Types

If memory is important opt for smaller data types, such as `Int32` instead of `Int`, to keep the memory footprint lean. Smaller data types typically come with smaller alignment requirements and less padding. Here's an example:

```swift
struct SensorData {
    var value: Int32  // 4 bytes
    var timestamp: Double // 8 bytes
}
```

### 3. The `@packed` Attribute

Swift throws a wildcard into the mix with the `@packed` attribute. Apply it to a struct if you want to minimize padding, akin to C's packed attribute. But tread carefully, as it might impact performance on certain systems:

```swift
struct MyStruct {
    var a: Int32
    var b: Double
} @packed
```

### 4. Beware of Reference Types

Stay cautious with reference types like classes within a struct. They bring along some extra memory overhead, another lesson inherited from C. Remember, structs are all about values, so adding reference types can bulk up their size.

## Determining the size of Swift structs

In Swift, you can determine the size of a struct or any data type using the `MemoryLayout` struct and its `size` property. `MemoryLayout` is a generic struct that provides information about the memory layout and size of Swift types. Here's how you can use it to find the size of a struct:

```swift
struct MyStruct {
    var a: Int
    var b: Double
}

let sizeOfMyStruct = MemoryLayout<MyStruct>.size
print("Size of MyStruct: \\(sizeOfMyStruct) bytes")
```

In the code above, we define a struct `MyStruct` with two members, an `Int` and a `Double`. We then use `MemoryLayout<MyStruct>.size` to obtain the size of `MyStruct` in bytes and print it to the console.

This will give you the size of the struct in bytes as it would be laid out in memory. Keep in mind that the actual size of a struct can be affected by factors like padding and alignment, which are determined by the Swift compiler to optimize memory access and performance. The `MemoryLayout` struct provides information based on the compiler's decisions.

## The Delicate Balance

Now, here's the catch: optimizing struct packing is like walking a tightrope. You want a sleek memory footprint, but you also crave top-notch performance. Overdoing it with packing and alignment tweaks can lead to performance hiccups, especially on architectures that demand strict alignment.

Always keep an eye on memory usage and performance by profiling your application. It's the only way to ensure your optimizations hit the bullseye without introducing unexpected side effects.

In the grand scheme of things, Swift's memory layout and struct packing principles have a rich lineage from C. This inheritance ensures that Swift strikes a harmonious balance between memory efficiency and performance, benefiting from the wisdom and experience of its predecessor.

So, fellow Swift enthusiasts, go forth and craft those memory-efficient structs while keeping your code clean and snappy. Swift is the future, and it brings along a bit of the past to make it even better.
