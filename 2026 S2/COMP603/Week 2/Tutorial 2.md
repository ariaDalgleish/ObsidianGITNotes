
# Debug Program Task02_1
NetBeans Debugger allows for **breakpoints**, add field watches, step through your code, run into methods, take snapshots, and monitor execution as it occurs. 

Make a breakpoint and run debug file, hover mouse and properties will be shown with their value.
![[Pasted image 20260828170845.png]]

`F8` to step over to next line of code.

Keep pressing F8 to check value or variation of `int i` and `dogName`. What are the bugs?

First F8 (line 32)
`dogArray = #206(length=5), i = 0`

2nd F8 (line 33)
Moves onto next line (below) 
`dogName = "doggy1 ", dogArray = #206 (length=5), i = 0`
`dogName = "doggy1 "`

3rd F8 (line 31)
Moves onto next line (line above) goes up because it's running in a for loop!
`i = 0, dogArray = #206(length=5)`

4th F8 (line 32)
Back to original line
`dogArray = #206(length=5), i = 1`
`i` now is equal to 1

5th F8 (line 33)
`dogName = " doggy2", dogArray = #206(length=5), i = 1`
`dogName = " doggy2"`

6th F8 (line 31)
Start of loop again
`i = 1, dogArray = #206(length=5)`

7th F8 (line 32)
`i = 2`

8th F8 (line 33)
`dogName = "doggy3`

9th F8 (line 31)
`i = 2`

10th F8 (line 32)
`i = 3`

11th F8 (line 33)
`dogName = " doggy4"`

12th (line 31)
`i = 3`

13th (line 32)
`i = 4`

14th (line 33)
`dogName = null`

15th
``` java
 void dispatchUncaughtException(Throwable e) {
        getUncaughtExceptionHandler().uncaughtException(this, e);
    }
```

Once loop reached d5 the dogName is null. Calling dogName.trim() on null throws the NPE

Second bug in the loop: once first one is fixed `i <= dogArray.length` will cause an `ArrayIndexOutOfBoundsException`, since valid indices only go up to `dogArray.length - 1`.
## Task 2.3 File I/O
Create a class with a main function under the Task02_2 package and achieve the
following features:
• ONLY copy all the letters from T02_input.txt to T02_output.txt
• Reverse the letters' order in each line
• Convert all letters to uppercase.

## Task 2.4 Collection and File I/O

using a `HashMap` (from Java Collections) to hold student scores in memory, and file streams (from File I/O) to load and save that data.

|Requirement from the task|List|Set|Map|
|---|---|---|---|
|Store a **name paired with a mark**|✗ — a `List` just holds single elements in order; you'd need parallel lists or a custom object, which is clunky|✗ — same problem, a `Set` holds single elements|✓ — naturally pairs a **key** (name) with a **value** (mark)|
|**Check if a student is already recorded** (`"checks whether the mark of the student was recorded already"`)|✗ — you'd have to loop through the whole list every time (`O(n)` search) checking each entry's name|✗ — a `Set` can check membership fast, but only for whole elements, not "does this name exist regardless of mark"|✓ — `map.containsKey(name)` is a single fast lookup, exactly checking by name|
|**Overwrite an existing record**|✗ — no unique-key concept, you'd have to find the index and replace manually|✗ — Sets don't support "update the value for X", since there's no separate key/value|✓ — `map.put(name, newMark)` automatically replaces the old mark for that name|
|**No duplicate names allowed** (implied by "checks whether already recorded")|✗ — `List` explicitly **permits duplicates** (slide 25: _"List: an ordered collection permitting duplicates"_)|✓ — `Set` guarantees uniqueness, but only of the _whole object_, not just the name field, unless you override `equals()`/`hashCode()` as shown on slide 21|✓ — `Map` guarantees **unique keys** (slide 27: _"No duplicated keys!!!"_) — exactly what "one mark per student" needs|

### Why `Map` wins

The task is fundamentally about a **name → mark relationship**, and every core requirement — look up by name, check existence by name, overwrite by name — maps directly onto `Map`'s built-in operations:

java

```java
map.containsKey(name)   // "checks whether the mark was recorded already"
map.get(name)           // retrieve the existing mark to show the user
map.put(name, mark)     // add a new record OR overwrite an existing one — same method does both!
```

A `List<Student>` (using a custom `Student` class with name+mark fields) _could_ technically work, but you'd be manually reimplementing what `Map` already gives you for free — looping to search, looping to check duplicates, and writing your own overwrite logic. That's exactly the kind of "why would I use this instead of an array" inefficiency your Collections lecture warns about avoiding.

### Which `Map` implementation specifically?

I used **`LinkedHashMap`** rather than plain `HashMap`:

- `HashMap` (slide 27–29): fast, but **doesn't guarantee any particular order** when you iterate it — Andy, Bob, and Alice could come out in a different order than they went in.
- `LinkedHashMap`: same key-uniqueness guarantee and same fast lookups, but **preserves insertion order** — so when you write back to the file, `Andy`, `Bob`, `Alice` stay in the order they were loaded, and new entries (like `Chris`) get appended at the end rather than scattered unpredictably. This keeps your output file looking sensible to a human reading it.