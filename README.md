# Modern C++ Thread Pool

A clean, header-only, priority-aware thread pool for modern C++.

A minimal, embeddable thread pool implementation in C++17+ designed for clarity, correctness, and real-world use.

This project avoids unnecessary abstractions and focuses on a small, readable core that you can understand, modify, and confidently ship.

## ✨ Features

✅ Header-only (#include and go)
✅ Modern C++17 / C++20 compatible
✅ Fixed-size worker pool
✅ Task submission with std::future
✅ Task priorities (simple & predictable)
✅ Exception-safe
✅ Graceful shutdown
✅ No dynamic allocations in hot paths
✅ Cross-platform (Linux, Windows, macOS)

## 🎯 Design Goals

This project is intentionally:

- **Small** – a few hundred lines, not thousands
- **Readable** – no macro magic or template abuse
- **Embeddable** – drop it into any codebase
- **Honest** – no "lock-free miracle" claims

If you need a massive async runtime, this is not it.
If you want a clean, understandable thread pool, this is.

## 🚀 Quick Start

### 1️⃣ Include the header

```cpp
#include "thread_pool.hpp"
```

### 2️⃣ Create a pool

```cpp
thread_pool pool(8); // 8 worker threads
```

### 3️⃣ Submit tasks

```cpp
auto future = pool.submit([] {
    return 42;
});

std::cout << future.get() << std::endl;
```

## 🔥 Task Priorities

Tasks can be submitted with a priority:

```cpp
pool.submit(priority::high, [] {
    heavy_work();
});

pool.submit(priority::low, [] {
    background_task();
});
```

Priority scheduling is simple, explicit, and deterministic — no hidden heuristics.

## 📂 Project Structure

```
modern-cpp-thread-pool/
├── include/
│   └── thread_pool.hpp
├── examples/
│   └── basic.cpp
├── benchmarks/
│   └── compare.cpp
├── README.md
└── LICENSE
```

## 🧠 How It Works (High Level)

- A fixed number of worker threads wait on a condition variable
- Tasks are stored in a priority queue
- Workers pull the highest-priority task available
- `std::packaged_task` is used to provide `std::future`
- Shutdown waits for in-flight tasks to finish cleanly

No busy waiting. No undefined behavior. No surprises.

## ⚡ Performance Philosophy

This project prioritizes:

- Predictable latency
- Low overhead
- Minimal synchronization

It is not a benchmark contest winner — and doesn't try to be.
Benchmarks are included to show reasonable performance, not marketing numbers.

## 📚 What This Is / Is Not

### ✅ This is:

- A practical thread pool for C++ projects
- A learning-friendly implementation
- Suitable for tools, services, and libraries

### ❌ This is not:

- A full async runtime
- A coroutine framework
- A lock-free research project

## 🧪 Benchmarks

Basic comparisons against `std::async` and naive thread spawning are provided in `benchmarks/`.

Results will vary by platform and workload — numbers are provided for transparency, not competition.

## 🛣 Roadmap

- [ ] Optional bounded queue
- [ ] Better shutdown policies
- [ ] Work-stealing experiment (optional)
- [ ] Additional benchmarks

## 🤝 Contributing

Contributions are welcome — especially:

- Bug fixes
- Benchmark improvements
- Documentation clarity
- Platform testing

If you're learning concurrency in C++, this is a great place to contribute.

---

**Made with ❤️ for modern C++ developers**
