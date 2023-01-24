# Weak_ptr

1. std::weak_ptr is always initialised with a shared pointer.

2. A shared pointer has a control block that holds the info about the allocated memory.

3. The control block holds the ref count as well.

4. std::weak_ptr internally points to the control block of shared pointer.

Eg: 
```
std::shared_ptr<int> p{new int{5}};

std::weak_ptr<int> wk = p;

p.reset();
```

5. p.reset will decrement the ref count of shared_ptr to 0, but the weak_ptr will still be pointing to the same control block.

6. There can be multiple weak_ptr pointing to same shared_ptr.

7. There is internally another ref count in shared_ptr control block that holds the count of weak_ptrs.

8. To access the underlying pointer using weak_ptr we have to call a function called expired, which checks if ref count of shared_ptr is 0 and returns true or false.

9. If underlying shared_ptr is still valid, we can call lock function on weak_ptr which will increment the ref count of shared_ptr, so even if the shared_ptr is deleted 
   we can still access it as ref count is not zero, we got a lock on it.
