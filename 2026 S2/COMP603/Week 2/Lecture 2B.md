## File I/O

Input/Output

Delimiters 

`BufferedReader` for input, `PrintWriter` for output

- `BufferedReader.readLine()` returns `null` at end of file — that's the loop condition (matches slide 20).
- `PrintWriter` wrapping `FileOutputStream` opens/creates `output.txt`, overwriting it each run unless you use the `(filename, true)` append constructor (slide 15).
- `StringBuilder.reverse()` is the cleanest way to reverse a string in Java — you can't reverse a `String` in place since strings are immutable.