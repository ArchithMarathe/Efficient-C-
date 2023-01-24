# Shared_ptr

1. Allows sharing of underlying pointer with other objects unlinke unique_ptr.

2. shared_ptr supports copy.

3. Always start with a unique_ptr, when you compile the compiler will show places if youre copying the unique_ptr, then we can switch to shared ptr.
<br>
&nbsp;How does a shared_ptr keep track of its copies?<br>
	&nbsp; &nbsp; -> A reference counter is maintained inside a shared_ptr and is shared among all the copies.
	<br><br>
  Eg :<code>std::shared_ptr<Integer> sh{new Integer{5}};  </code>

4. sh.use_count() will give us the reference count of the shared_ptr.

5. When the reference count becomes 0 the underlying pointer will be deleted.

6. The reference count is decremented in the destructor of the shared_ptr, if its 0 the underlying pointer is deleted.

7. ```sh.reset(new Integer{})``` will decrement the reference count & delete underlying pointer if reference count is 0, otherwise take ownership of the new pointer.
   reference count of this new pointer will be 1.
  
  
  ```
  
  #include<memory>
#include<iostream>
#include "Integer.h"


void func(auto p)
{
	std::cout<<p.use_count()<<std::endl; //2
}


int main(int argc, char const *argv[])
{
	std::shared_ptr<Integer> ptr = std::make_shared<Integer>(45);
	
	func(ptr);

	std::cout<<ptr.use_count()<<std::endl; //1

	auto q = ptr;

	std::cout<<ptr.use_count()<<std::endl; //2
	
	return 0;
}
  
```
