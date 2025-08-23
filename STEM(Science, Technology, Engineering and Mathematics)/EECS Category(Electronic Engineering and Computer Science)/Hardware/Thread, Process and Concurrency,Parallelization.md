# Thread vs Process 

thread线程是"工厂"process内的"工人", 多个thread共享一批计算资源. 而每个"工厂"process则独立占据一定量的资源. 

thread和process都可以在单核或多核CPU上运行, 在单核CPU上运行时主要依赖于其concurrency并发机制, 而在多核CPU上则是实现了真正的并行. 

thread和process都是并行概念的抽象层执行者. 
