# Alternatives to vDOMs:

## Incremental DOM
Incremental DOM doesn't keep a complete copy of a virtual DOM in memory. Instead, it diffs against the actual DOM if the application state changes. That's a tradeoff between memory usage (garbage collection etc.) and rendering performance (layouting and painting).

* GitHub: https://github.com/google/incremental-dom

## Compiling
In recent years, a few frameworks and PoCs have appeared that implement a completely different approach. They allow to write componend-based applications in the same way Vue and React do. However, they are compiled down to low-level, imperative code composed of "real" DOM operations.

Svelte's (https://svelte.dev) a framework that’s built on this design principle. Angualar and React have announced precompilers named Ivy and Prepack, respectively. While rendering optimization might be introduced in the future, both currently only support basic code optimization.

* https://prepack.io/
* https://blog.angular.io/a-plan-for-version-8-0-and-ivy-b3318dfc19f7
