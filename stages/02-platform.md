# Stage 2. Deeper into the .NET platform

**Duration:** 1–2 months after confidently clearing Stage 1.

**Stage goal:** understand how exactly your code runs. This is the line that separates a junior who "writes code that works" from a middle who "writes code that holds up under load and doesn't fall apart."

## Topics

### CLR and compilation

- CLR, JIT, AOT, Tiered Compilation, ReadyToRun.
- What happens between pressing F5 and `Main` running.
- Inspecting generated IL and native code via [SharpLab](https://sharplab.io/).

### Memory management

- Stack, heap, GC generations (Gen 0/1/2, Large Object Heap).
- Server GC vs Workstation GC, when to use which.
- `Span<T>`, `Memory<T>`, `ref struct`, `stackalloc`.
- Pinning, `fixed`, GCHandle — when and why.
- ArrayPool, MemoryPool, RecyclableMemoryStream for hot paths.

### Async/await internals

- SynchronizationContext and why it's critical in UI apps.
- `ConfigureAwait(false)` — when it's required, when it isn't.
- ValueTask vs Task — trade-offs.
- CancellationToken — always propagate it.
- Pitfalls: sync-over-async, async void, `.Result`, `.Wait()`.

### Parallelism and concurrency

- Thread, ThreadPool, Task, Parallel.
- Channels for producer-consumer scenarios.
- Synchronization primitives: lock, SemaphoreSlim, Interlocked, ReaderWriterLockSlim.
- Lock-free structures and the .NET memory model.

### Reflection and Source Generators

- Reflection, attributes, dynamic invocation.
- The cost of reflection on hot paths.
- Source Generators as the modern alternative (System.Text.Json, regex, logging).

### IO

- Streams, BufferedStream, MemoryStream.
- Pipelines (`System.IO.Pipelines`) for high-performance IO.
- Async file operations and their gotchas on Windows/Linux.

### Serialization

- `System.Text.Json` as the default.
- Custom converters, source-generated serialization.
- Comparison with Newtonsoft.Json on performance and features.
- MessagePack, Protobuf-net for binary formats.

## Resources

### Books

- **Konrad Kokosa, "Pro .NET Memory Management"** — a deep dive into the GC.
- **Stephen Cleary, "Concurrency in C# Cookbook"** — recipes for async and parallelism.

### Blogs

- [Stephen Toub on devblogs.microsoft.com](https://devblogs.microsoft.com/dotnet/author/toub/) — the best source on performance and async.
- [Adam Sitnik](https://adamsitnik.com/) — performance and Span.
- [Bartosz Adamczewski](https://leveluppp.ghost.io/) — CLR internals.

### Videos

- Nick Chapsas, the performance and Span series.
- [.NET YouTube channel](https://www.youtube.com/@dotnet) — official talks.
- DotNext, NDC, .NET Conf — recordings free of charge.

## Practice

### Micro-projects

1. **Thread-safe LRU cache.** Measure throughput at different concurrency levels through BenchmarkDotNet.
2. **A simple object pool.** Compare against `ObjectPool<T>` from Microsoft.Extensions.ObjectPool.
3. **A Span-based CSV parser.** Compare allocations against a naive `string.Split` implementation.
4. **Producer-consumer through Channel<T>.** Implement back-pressure and graceful shutdown via CancellationToken.

### Benchmarks

Install [BenchmarkDotNet](https://benchmarkdotnet.org/) and write your first benchmark. The cardinal rule: don't trust your intuition about performance, verify.

```csharp
[MemoryDiagnoser]
public class StringConcatBench
{
    [Params(10, 100, 1000)]
    public int N { get; set; }

    [Benchmark]
    public string PlusOperator()
    {
        var s = "";
        for (var i = 0; i < N; i++) s += i;
        return s;
    }

    [Benchmark]
    public string StringBuilder()
    {
        var sb = new StringBuilder();
        for (var i = 0; i < N; i++) sb.Append(i);
        return sb.ToString();
    }
}
```

## Readiness checklist for Stage 3

- [ ] I can explain the difference between Task and ValueTask
- [ ] I know why `async void` is dangerous
- [ ] I understand what ConfigureAwait does and when it's needed
- [ ] I can write a method that takes `ReadOnlySpan<char>` for zero allocations
- [ ] I understand how Gen 0/1/2 differ in the GC
- [ ] I know what the LOH is and why I shouldn't dump large arrays into it frequently
- [ ] I've run at least one benchmark through BenchmarkDotNet and analyzed the result
- [ ] I understand the .NET memory model at the level of "memory barriers go here"
- [ ] I use Source Generators in at least one of my projects
- [ ] I can read Stephen Toub-style code and see why `stackalloc` is there

## Navigation

[← Stage 1](01-foundation.md) | [All stages](README.md) | [Main README](../README.md) | [Stage 3 →](03-tooling.md)
