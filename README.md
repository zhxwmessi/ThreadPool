ThreadPool
==========

A simple C++11 Thread Pool implementation.

My usage:
```c++
void task(int i){
    std::cout << "hello " << i << std::endl;
    std::this_thread::sleep_for(std::chrono::seconds(1));
    std::cout << "world " << i << std::endl;
}

int main()
{
    ThreadPool pool(4);
    std::vector< std::future<int> > results;
    for(int i = 0; i < 8; ++i) {
        pool.enqueue(std::bind(task, i));
    }
    return 0;
}
```
Basic usage:

```c++
// create thread pool with 4 worker threads
ThreadPool pool(4);

// enqueue and store future
auto result = pool.enqueue([](int answer) { return answer; }, 42);

// get result from future
std::cout << result.get() << std::endl;

```
