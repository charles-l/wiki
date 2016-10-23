# Performance

    In reality computers are far too complex for anyone to handle performance problems by “reasoning” alone.

    Think about a routine in a modern jitted language. Right off the bat you face hidden magic like type coercion, boxing, and unboxing. Even if you know the language intimately, unknowns are introduced as your code is optimized first by the compiler, then again by the JIT compiler. It is then fed to the CPU, where optimizations such as branch prediction, memory prefetching and caching have drastic performance implications. What’s worse, much of the above can and does change between different versions of compilers, runtimes, and processors. Your ability to predict what is going to happen is limited indeed.

    - http://duartes.org/gustavo/blog/post/performance-is-a-science/
