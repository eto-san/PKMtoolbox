---
tags:
  - notes/permanent
created: 2025-02-03
up:
  - "[[Programming Languages]]"
related:
  - "[[C++]]"
  - "[[Rust]]"
  - "[[GO]]"
collection:
  - Languages
aliases:
---
# D


> [!abstract] D
> ![img 100|100](https://upload.wikimedia.org/wikipedia/commons/thumb/2/24/D_Programming_Language_logo.svg/240px-D_Programming_Language_logo.svg.png)
>`Current Version:`
> ![[D.canvas]]


## General Information
- **Name:** D
- **Year Created:** 2001
- **Creator(s):** [Walter Bright](https://en.wikipedia.org/wiki/Walter_Bright "Walter Bright") at [Digital Mars](https://en.wikipedia.org/wiki/Digital_Mars "Digital Mars")
- **Primary Use Cases:** D stands out in system utilities, compilers, network servers, and metaprogramming, focusing on compile-time function execution and domain-specific languages. You also see it used in open-source game engines.
- **Paradigm(s):** [Multi-paradigm](https://en.wikipedia.org/wiki/Multi-paradigm_programming_language "Multi-paradigm programming language"): [functional](https://en.wikipedia.org/wiki/Functional_programming "Functional programming"), [imperative](https://en.wikipedia.org/wiki/Imperative_programming "Imperative programming"), [object-oriented](https://en.wikipedia.org/wiki/Object-oriented_programming "Object-oriented programming")
- **Typing Discipline:** [Inferred](https://en.wikipedia.org/wiki/Inferred_typing "Inferred typing"), [static](https://en.wikipedia.org/wiki/Static_typing "Static typing"), [strong](https://en.wikipedia.org/wiki/Strong_typing "Strong typing")

## Syntax & Structure
Hello D!
  ```D
   import std.stdio;

   void main() {
       writeln("Hello, World!");
   }

     # Hello World Example code snippet
  ```

- **import std.stdio;**  
  This line brings in the standard input/output library, which provides the `writeln` function used for printing to the console.

- **void main() { … }**  
  In D, execution starts from the `main` function. Here, `void main()` indicates that the program does not return a value.

- **writeln("Hello, World!");**  
  The `writeln` function prints the string "Hello, World!" followed by a newline.

#### How to Compile and Run

1. Save the above code to a file named, for example, `hello.d`.
2. Open a terminal and navigate to the directory containing the file.
3. Compile the program using the D compiler (typically `dmd`):

   ```sh
   dmd hello.d
   ```

4. Run the resulting executable:

   - On Unix-like systems:  
     ```sh
     ./hello
     ```
     
   - On Windows:  
     ```sh
     hello.exe
     ```

You should see the output: `Hello, World!`

---
### Basic Syntax Overview:
D’s syntax is designed to be familiar to C and C++ programmers while adding modern features such as contract programming and built‐in support for ranges and parallelism. See code snippets below:

#### Variables & Data Types

D is statically typed but also supports type inference using the `auto` keyword.

```d
import std.stdio;

void main() {
    // Declaration with explicit types
    int a = 42;
    double b = 3.14;
    bool isDGreat = true;
    string greeting = "Hello, D!";
    
    // Using type inference
    auto c = 100;  // c is inferred to be int

    writeln("a = ", a);
    writeln("b = ", b);
    writeln("isDGreat = ", isDGreat);
    writeln("greeting = ", greeting);
}
```

**Key Points:**
- D supports standard types such as `int`, `double`, `bool`, and `string`.
- Use `auto` to let the compiler deduce the type.

##### Arrays, Slices, and Ranges
Dynamic arrays and slicing are built into D.

```d
import std.stdio;

void main() {
    // Create a dynamic array
    int[] arr = [1, 2, 3, 4, 5];
    writeln("Array: ", arr);
    writeln("Length: ", arr.length);
    
    // Append an element
    arr ~= 6;
    writeln("After appending: ", arr);
    
    // Create a slice of the array (elements at indices 2 to 4)
    int[] slice = arr[2 .. 5];
    writeln("Slice: ", slice);
}
```

##### User-Defined Types: Structs
**Structs** define **custom data types** that group multiple variables together.

```d
import std.stdio;

struct Point {
    int x, y;
    
    // Method within a struct
    void display() {
        writeln("Point(", x, ", ", y, ")");
    }
}

void main() {
    Point p = Point(10, 20);
    p.display();
}
```

##### User-Defined Types: Classes
They are **reference types**, meaning they are **allocated on the heap** and support **inheritance and polymorphism**.

```d
import std.stdio;

class Person {
    string name;
    int age;
    
    // Constructor
    this(string name, int age) {
        this.name = name;
        this.age = age;
    }
    
    void greet() {
        writeln("Hello, my name is ", name, " and I am ", age, " years old.");
    }
}

void main() {
    auto person = new Person("Alice", 30);
    person.greet();
}
```

---

#### Control Structures: Conditionals and Loops
##### If-Else Statements

```d
import std.stdio;

void main() {
    int num = 10;
    if (num > 0) {
        writeln("Positive number");
    } else if (num < 0) {
        writeln("Negative number");
    } else {
        writeln("Zero");
    }
}
```
##### For, While, and Foreach Loops

```d
import std.stdio;

void main() {
    // For loop: classic C-style
    for (int i = 0; i < 5; i++) {
        writeln("For loop iteration: ", i);
    }
    
    // While loop
    int j = 0;
    while (j < 5) {
        writeln("While loop iteration: ", j);
        j++;
    }
    
    // Foreach loop: iterates directly over a range or array
    int[] numbers = [10, 20, 30, 40];
    foreach (num; numbers) {
        writeln("Number: ", num);
    }
}
```

##### Exception Handling
D uses `try-catch` blocks for exception handling:

```d
import std.stdio;
import std.exception;

void main() {
    try {
        throw new Exception("Something went wrong!");
    } catch (Exception e) {
        writeln("Caught exception: ", e.msg);
    }
}
```

---

#### Functions & Modules

##### Basic Template (Generic) Functions
Functions in D have a syntax similar to C, but you can also write generic functions using templates.

```d
import std.stdio;

// A simple function
int add(int x, int y) {
    return x + y;
}

// A generic function using a template
T multiply(T)(T a, T b) {
    return a * b;
}

void main() {
    writeln("5 + 7 = ", add(5, 7));
    writeln("3.5 * 2.0 = ", multiply(3.5, 2.0));
}
```
---

#### Other

##### Comments
D supports single-line (`//`) and multi-line comments (`/* ... */`),

```d
// This is a single-line comment

/*
   This is a multi-line comment.
*/
```

##### Contracts
Contracts (`in`, `out`, `assert`) enforce **preconditions, postconditions, and invariants**.

```d
import std.stdio;

int factorial(int n)
in {
    assert(n >= 0, "n must be non-negative");
} out (result) {
    assert(result > 0, "result must be positive");
} body {
    if (n == 0)
        return 1;
    else
        return n * factorial(n - 1);
}

void main() {
    writeln("Factorial of 5: ", factorial(5));
}
```

---

## Ecosystem & Tooling
- **Standard Library:** Phobos (https://dlang.org/phobos/) and Tango (http://dsource.org/projects/tango) are considered the two standard libraries that map to different runtime support structures.  Tango has differentiated itself as a cross-platform open-source software library from the original Phobos library that the community has voiced dissatisfaction with.
- **Package Management System:** [DUB](https://code.dlang.org) replacing legacy DPM 
- **Popular Frameworks/Libraries:** 
	- [Vibe.d](https://vibed.org/) - provide asynchronous I/O and networking capabilities
	- [Hunt Framework]() - Web development Framework
	- [Mir](http://mir-algorithm.libmir.org/mir_numeric.html) - A numerical library for D, offering high-performance linear algebra routines, random number generation, and other scientific computing tools.
- **IDEs & Editors:** DlangIDE, Emacs, vim
- **Compilers:**
	- [DMD](https://github.com/dlang/dmd)
	- GDC ([[GCC]]-based)
	- LDC ([[LLVM]]-based)

## Strengths & Weaknesses
- **Strengths:**
	- Offers automatic memory management while allowing **manual control** when needed.
	- Memory `@safe` functions restrict unsafe operations, preventing buffer overflows and memory leaks.
	- No header files needed! D's **single-module system** makes compilation and organization easier.
- **Weaknesses:**
	- Two competing runtimes bifurcate elements of the ecosystem. 
	- Debugging tools are weaker.
	- Its trying to be to many things preventing a killer feature to outline.
	- Major syntax and features have changed overtime making legacy upkeep difficult.
	- Limited Industry use.
## Industry Adoption
- **Major Companies Using It:** [[Netflix]], eBay, Symmetry Investments, Mercedes Benz Automotive Research
- **Notable Open-Source Projects:**
	- [DMD](https://dlang.org/dmd-linux.html) -official compiler
	- [Tilix]() - terminal emulator for Linux
## Community & Learning Resources
- **Official Documentation:** https://dlang.org/spec/spec.html
- **Community Forums:** 
	- [Official D Forum Learn Group](https://forum.dlang.org/group/learn)
	- [Git/dlang-community](https://github.com/dlang-community)
- **Best Learning Resources:** 
  - Books: [Programming in D by Ali Çehreli](http://ddili.org/)
  - Courses: https://tour.dlang.org/
  - YouTube: [Programming in Dlang](https://www.youtube.com/watch?v=HS7X9ERdjM4&list=PLvv0ScY6vfd9Fso-3cB4CGnSlW0E4btJV&ab_channel=MikeShah) [^ref2]
  - Code Snippets: [Functional Garden](https://garden.dlang.io) [^ref2]

## Comparisons & Alternatives
- **Similar Languages:** [[C++]] & [[Rust]] & [[Go]], [[Swift]]
- **Key Differences:**
  - **Performance** is similar to [[C++]] and [[Rust]]
  - **Ease of Learning** [[D]] is supposedly more readable than [[C++]], No header files like [[C++]]
  - **Scalability** A D codebase is easier to scale than C++ but lacks Rust’s strict safety. Go and Swift excel in developer experience but trade off advanced metaprogramming features.

[[D]]'s lack of a corporate sponsor is a major callout when projecting further adoption and community expansion.
## Future Outlook
- **Current Trends & Developments:**
	- [Possibly forking the language.](https://forum.dlang.org/thread/wfrkwjwpjzrefefzejul%40forum.dlang.org)
	- Enhancing the standard library.
	- Continued support of metaprogramming paradigms and safety features. [ref](https://forum.dlang.org/thread/wfrkwjwpjzrefefzejul%40forum.dlang.org)
- **Future Roadmap:**
	- Simplifying: Enhancing the out-of-the-box user experience by ensuring tools and libraries function seamlessly upon installation.
	- Memory Safety: Addressing memory safety issues to prevent vulnerabilities such as memory corruption and malware exploits.
	- Enhancements to Phobos and DRuntime

## Additional Notes
- If I were to return to some low level programing for myself (i.e. non-production) I'd pick this up.


---
[^ref1]: Lastname, F. M. (Year, Month Date). _Title of page_. Site name.  https://owl.purdue.edu/owl/research_and_citation/apa_style/apa_formatting_and_style_guide/index.html
[^ref2]: https://github.com/dlang-community/awesome-d
[^ref3]: https://forum.dlang.org/thread/wfrkwjwpjzrefefzejul%40forum.dlang.org
