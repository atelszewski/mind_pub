# Notes on C++

## Classes

### Constructors
### Destructors

`constexpr` implies `inline`.

## Type information

### Getting type of a member of a structure

```cpp
class the_class
{
    struct the_struct
    {
        some_type_t the_member;
    };
};

using the_member_type =
    decltype(the_class::the_struct:the_member);
```

## Arguments passing

### Fixed size array passed by reference

Declare function that accepts fixed-size array,
that is passed by reference.

```cpp
size_t getTimestamp(uint64_t (& timestamp)[ARRAY_SIZE]);
```
