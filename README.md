# First post

1. **Optimize Regex Usage in PostCSS**

   - **What:** A costly regex operation in `postcss-custom-properties` plugin was taking 4.6s due to serialization and repeated regex over short strings.
   - **Why:** Regex matching against many short strings is slower and incurs serialization costs compared to longer strings.
   - **How:** Implement a check to avoid unnecessary regex operations when the file doesn't contain relevant comments, thereby reducing build time significantly.

2. **Improve SVG Compression in SVGO**

   - **What:** The `strongRound` function in SVGO was inefficient due to casting between string and number types.
   - **Why:** Frequent type casting increases computation time and can trigger garbage collection.
   - **How:** Rewrite the `strongRound` function to avoid string casting and stay in number-land, leading to a 1.4s improvement in build times.

3. **Avoid Unnecessary Recursion and Transpilation in SVGO and @vanilla-extract/css**
   - **What:** Inefficient recursion in SVGO's `perItem` function and problematic transpilation of `for...of` in @vanilla-extract/css.
   - **Why:** Inner functions are hard to optimize, and transpilation can introduce inefficiencies.
   - **How:** Refactor `perItem` to avoid inner functions and patch `for...of` loop in the local `node_modules` to improve performance.
