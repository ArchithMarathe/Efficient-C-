# Unique_ptr

1. std::unique_ptr can be used when we dont want to share the pointer among different parts of code.

2. To use unique_ptr we have to #include<memory>.

3. std::unique_ptr is a class template , it takes class name and custom deleter within angular braces.

4. When the unique_ptr object goes out of scope it is automatically deleted.
  
  Eg : `std::unique_ptr<MyClass,myDeleter> ptr ;`
  
5. The unique_ptr has explicit ctor so we cannot use = for initialization.

  Eg :<code> std::unique_ptr<MyClass,myDeleter> ptr  = GetPointer(); //is not allowed <br>
       &nbsp;&nbsp;&nbsp;&nbsp;std::unique_ptr<MyClass,myDeleter> ptr{GetPointer()}; //is allowed </code>

6. We can check unique_ptr == nullptr as == is overloaded for unique_ptr.

7. Once unique_ptr is created we cannot assign a new pointer to it, we have to do ptr.reset(new Myclass()) and the old pointer is deleted.

8. unique_ptr overloads -> and * operators for dereferencing.

9. unique_ptr is an object i.e its a wrapper for a pointer.

10. ptr.get() will return the underlying pointer, it can be useful when passing pointers to functions that accept raw pointers.

11. The copy ctor of unique_ptr is deleted , so we cannot pass by value unique_ptr to a function,so to pass unique_ptr to functions
    we can use std::move() if we no longer need the unique_ptr after passing or we can pass by reference.

	
```
#include<iostream>
#include<memory>
#include "Integer.h"

int main(int argc, char const *argv[])
{
	
	std::unique_ptr<Integer> ptr{GetPointer(40)};
	std::cout<<*(ptr->myInt)<<std::endl; //40
	Integer* ptr2 = ptr.get();
	*ptr2->myInt = 45;
	std::cout<<*ptr->myInt; //45
	std::cout<<(ptr==nullptr); //0
	ptr.reset(new Integer{80});
	return 0;
}
```
	
[Home](./Home.md)    [Next: Shared Pointers](./SharedPointers.md)
	
	
	
