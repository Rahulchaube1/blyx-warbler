## Distinguish a clipped transient from a sustained overload

Returns [peak, mean square, longest clipped run, alert]. Alert means the longest run exceeded the allowed number of samples. Invalid arguments and nonfinite results return an empty vector.

1. Open an empty file named `warbler-demo.blyx`.
2. Type `blyx-warbler-demo` and select **Warbler — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
1
0.5
2
1
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-warbler)
