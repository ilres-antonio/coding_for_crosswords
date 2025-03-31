# Coding for Crosswords

## Links
Website : [https://codingforcrosswords.com/](https://codingforcrosswords.com/)

Youtube : [https://www.youtube.com/channel/UCzGKCXSeHjDRSmpX9SmQ1fw](https://www.youtube.com/channel/UCzGKCXSeHjDRSmpX9SmQ1fw)

C++ Reference: 
- [https://www.w3schools.com/cpp/](https://www.w3schools.com/cpp/)
- [https://cplusplus.com/reference/](https://cplusplus.com/reference/)

Word Lists :
- [https://github.com/hackerb9/gwordlist](https://github.com/hackerb9/gwordlist)
- [https://en.wiktionary.org/wiki/Wiktionary:Frequency_lists#Top_English_words_lists](https://en.wiktionary.org/wiki/Wiktionary:Frequency_lists#Top_English_words_lists)

Misc :
- [https://blog.leonardotamiano.xyz/posts/crossword-solver-c++/](https://blog.leonardotamiano.xyz/posts/crossword-solver-c++/)

## TODO

- [X] 0. Course Overview
- [X] 1. Crossword puzzles
- [X] 2a. Setup C++ for Windows
- [ ] 2b. ~~Set Up C++ for Browser~~
- [ ] 2c. ~~Set Up C++ for Linux~~
- [ ] 2d. ~~Set Up C++ for Mac~~
- [X] 3. Add 1 plus 1!
- [X] 4. Load a Grid (part 1)
- [X] 5. Load a Grid (part 2)
- [X] 6. The Grid Object
- [X] 7. Read the Grid from a File
- [X] 8. Read the Library from a File
- [X] 9. Search the Library
- [X] 10. Search the Library, Fast!
- [X] 11. How Memory Works
- [x] 12. Pattern Hash
- [x] 13. Points-and-Spans
- [x] 14. Find Spans in the Grid
- [ ] 15. Get Strings from the Grid
- [ ] 16. Solver Class
- [ ] 17. Write Words to the Grid
- [ ] 18. Preventing Duplicates
- [ ] 19. ~~Speeding up the library with partial character hash~~
- [ ] 20. ~~Multi-threading: not as hard as you think!~~
- [ ] 21. ~~Adding points to the library word and scoring~~
- [ ] 22. ~~Ordered map to save the best N solutions~~
- [ ] 23. ~~Finding islands~~
- [ ] 24. ~~Partitions: finding, solving, and integrating~~
- [ ] 25. ~~More efficient incremental state change in recursion~~
- [ ] 26. ~~Recursion limits based on cpu and tree size~~
- [ ] 27. ~~Slot selection policy~~
- [ ] 28. ~~Grid composition (designing "block" black squares)~~
- [ ] 29. ~~Theme entry position permutations~~
- [ ] 30. ~~Screening templates~~


## Chapters

### 0. Course Overview
[https://youtu.be/qxbTN85O_LA](https://youtu.be/qxbTN85O_LA)

Welcome to "Coding for Crosswords", a course designed to teach you how to write a program that constructs crossword puzzles. This course is divided into 19 modules and contains approximately 12 hours of video content, as well as several interactive challenges designed to help you practice your programming skills and apply what you have learned.

We will start by covering the basics of programming and gradually build up to the point where you can create crossword puzzles. The course follows a goal-oriented approach, introducing only the language features and concepts that are necessary to accomplish each specific task. This helps you retain the knowledge better and avoids overwhelming you with too many aspects of the language.

In the first module, we will briefly discuss crossword puzzles and their history. In the second module, we will cover how to set up your compiler infrastructure, which can be done on Windows, in a browser, using Linux, or on a Macintosh. C++ is a standard, text-based programming language that does not require any special libraries or graphics capabilities, so it should be portable to most platforms.

Each module is about 20-40 minutes long, but there will be several challenges for you to complete as you go along. These challenges will ask you to code some piece of functionality, and they will be designed to be incremental, building on what you have learned so far. It is important to actively participate in the course, as programming is not something that can be learned passively by just watching videos.

Throughout this course, we will be focusing on constructing crossword puzzles, rather than solving them by reading clues and reasoning about them. We will start with some seed entries and use our software to fill in the rest of the words in various combinations. We will be using a smaller crossword puzzle as an example, and we will learn how to read in a file that describes the grid, search a library of 12,000 popular English words for patterns, and loop through all the possible solutions to find the best crossword construction. The goal is to produce a crossword puzzle that you can share with your family and friends.

### 1. Crossword puzzles
[https://youtu.be/bSZMj0OJP2A](https://youtu.be/bSZMj0OJP2A)
### 1. Crossword puzzles

In this chapter, we'll explore the fascinating world of crossword puzzles - their history, structure, and the key principles that will guide us as we develop our crossword construction software.

#### A Brief History of Crossword Puzzles

Crossword puzzles have a rich history dating back over a century:

- The first crossword puzzle was created by Arthur Wynne and published in the New York World newspaper on December 21, 1913
- Initially called "word-cross," the name later switched to "crossword"
- The crossword puzzle format gained tremendous popularity in the 1920s
- The New York Times, now famous for its crossword puzzles, didn't publish its first puzzle until 1942
- Today, crossword puzzles appear in newspapers, magazines, websites, and mobile apps worldwide

#### Anatomy of a Crossword Puzzle

Standard American-style crossword puzzles follow these conventions:

1. **Grid Structure**
   - Usually square, typically 15×15 squares for daily puzzles and 21×21 for Sunday puzzles
   - Symmetrical design (rotational symmetry - the grid looks the same when rotated 180 degrees)
   - Black squares ("blocks") separate words and create the puzzle pattern
   - Generally, no more than 1/6 of the squares are black

2. **Words and Entries**
   - **Across entries**: Words reading left to right
   - **Down entries**: Words reading top to bottom
   - Every letter must be part of both an across and a down word (interlocking)
   - Minimum word length is typically 3 letters
   - No duplicate words in the same puzzle

3. **Clues**
   - Each word has a corresponding numbered clue
   - Clues are listed separately for across and down entries
   - Clue difficulty varies by publication and day of the week (typically harder later in the week)

#### Crossword Construction Principles

When constructing crosswords, these principles guide the process:

1. **Theme Development**
   - Many puzzles have a theme with related entries
   - Themes might be based on puns, wordplay, or connected concepts
   - Theme entries are usually the longest entries in the puzzle

2. **Grid Design**
   - Start with placing theme entries in the grid
   - Design the black square pattern while maintaining symmetry
   - Create a pattern that allows for smooth word placement

3. **Word Selection**
   - Choose common, interesting words that solvers will recognize
   - Avoid obscure abbreviations, partial phrases, and foreign words when possible
   - Balance the difficulty level of vocabulary

4. **Fill Process**
   - The "fill" refers to placing all non-theme words in the grid
   - This is often the most challenging part of construction
   - Each word must interlock correctly with crossing words

#### Crossword Construction Software

Our project focuses on the fill process, which is the most computationally intensive part of crossword construction:

1. **Why We Need Software**
   - Manual filling is extremely time-consuming and difficult
   - Computers can quickly test thousands of word combinations
   - Software can optimize for the best possible fill

2. **The Solver's Algorithm**
   - We'll build a program that recursively tries words in empty slots
   - The program will backtrack when it reaches dead ends
   - We'll use heuristics to prioritize common, familiar words

3. **Word Libraries**
   - Our software will use a library of common English words
   - Words will be scored based on familiarity and usage
   - The library can be customized and expanded

#### What We'll Build

Throughout this course, we'll develop a program that can:

1. Read a grid template with some pre-placed words and black squares
2. Load a dictionary of words to use as our word library
3. Find all possible words that fit each empty slot in the grid
4. Recursively fill the grid to find the best possible solution
5. Score different solutions based on word quality
6. Output a completed crossword grid

#### Conclusion

Understanding the fundamentals of crossword puzzles is essential before we dive into coding. In the next chapter, we'll set up our development environment and begin building the foundation of our crossword construction software.

Remember, our goal is not to build a program that creates and solves crosswords based on clues, but rather one that constructs well-formed crossword grids from a word library, which is a fundamental step in the crossword creation process.

### 2a. Setup C++ for Windows
[https://youtu.be/Rov1Hm14ZoY](https://youtu.be/Rov1Hm14ZoY)

In this chapter, we'll walk through the process of setting up C++ development environment on Windows for our crossword puzzle project. This setup will allow you to compile and run the C++ code we'll be developing throughout the course.

#### Required Software

1. **Visual Studio Community Edition**
   - This is a free, full-featured IDE from Microsoft that provides everything you need to develop C++ applications on Windows
   - It includes a C++ compiler, debugger, and code editor all in one package

#### Installation Steps

1. **Download Visual Studio Community Edition**
   - Go to the Microsoft Visual Studio website
   - Select the Community Edition (free for individual developers)
   - Start the download process

2. **Run the Visual Studio Installer**
   - Launch the downloaded installer
   - This is a small program that will help you download and install the components you need

3. **Select Development Workload**
   - Choose "Desktop development with C++" workload
   - This will install the C++ compiler, standard libraries, and other tools needed

4. **Optional Components**
   - Make sure the Windows SDK is selected (typically included by default)
   - C++ CMake tools for Windows can be useful but isn't required for our course

5. **Complete the Installation**
   - Click Install and wait for the process to complete
   - This may take some time depending on your internet connection

#### Creating Your First Project

1. **Launch Visual Studio**
   - Open Visual Studio from the Start menu

2. **Create a New Project**
   - Select "Create a new project"
   - Choose "Console App" for C++
   - Name it "CrosswordTester" or something similar
   - Choose a location to save your project

3. **Basic Project Structure**
   - Visual Studio will create a basic project with a main.cpp file
   - This file contains a simple "Hello World" program by default

4. **Build and Run**
   - Press F5 or click the "Local Windows Debugger" button to build and run
   - You should see a console window appear with the output
   - The window will close automatically when the program finishes

#### Important Settings

1. **C++ Language Standard**
   - Right-click on your project in Solution Explorer
   - Select "Properties"
   - Go to: Configuration Properties > C/C++ > Language
   - Set "C++ Language Standard" to C++14 or higher

2. **Character Set**
   - Under Configuration Properties > Advanced
   - Set "Character Set" to "Use Multi-Byte Character Set"

3. **Build Configuration**
   - Learn the difference between Debug and Release configurations
   - Debug: Includes debugging information, useful during development
   - Release: Optimized code for final distribution

#### Troubleshooting Common Issues

1. **Compiler Errors**
   - Check that your C++ compiler is properly installed
   - Ensure you've selected the "Desktop development with C++" workload

2. **Missing Libraries**
   - Make sure the standard libraries are installed
   - If you see errors about missing headers, you may need to reinstall

3. **Path Issues**
   - Visual Studio should set up the environment paths automatically
   - If you're running from command line, you may need to set up paths manually

#### Next Steps

Once your environment is set up, you're ready to begin coding. In the next chapter, we'll create our first real C++ program for the crossword project and start exploring the language.

Remember: The C++ we'll be using is standard and should work on any platform, but the setup process differs between operating systems. This chapter focuses specifically on Windows setup with Visual Studio, which provides an integrated environment that's beginner-friendly.

### 3. Add 1 plus 1!
[https://youtu.be/Wf5mfSYXdZg](https://youtu.be/Wf5mfSYXdZg)
### 3. Add 1 plus 1!

In this chapter, we'll write our first C++ program for our crossword puzzle project. We'll start with the fundamentals of C++ programming by creating a simple program that adds two numbers together. This will help us get comfortable with the development environment and basic C++ syntax before we dive into more complex code.

#### Your First C++ Program

Let's start by writing a simple program that adds 1 plus 1:

```cpp
#include <iostream>

int main() {
    int result = 1 + 1;
    std::cout << "1 + 1 = " << result << std::endl;
    return 0;
}
```

This program may look simple, but it introduces several important C++ concepts:

1. **#include directive**: `#include <iostream>` tells the compiler to include the input/output stream library, which allows us to print to the console.

2. **main function**: Every C++ program needs a `main()` function, which is the entry point where execution begins.

3. **Variables**: We declare a variable `result` of type `int` (integer) and assign it the value of `1 + 1`.

4. **Output statement**: `std::cout` is used to display output to the console.

5. **Return statement**: `return 0;` indicates that the program executed successfully.

#### Building and Running the Program

1. Open your C++ development environment (like Visual Studio for Windows users).
2. Create a new project or file as we learned in Chapter 2.
3. Type the code above into your editor.
4. Build and run the program.

You should see output like:
```
1 + 1 = 2
```

#### Understanding the C++ Syntax

Let's break down some of the C++ syntax we've used:

1. **std::cout**:
   - `cout` is an object representing the console output
   - `std::` is a namespace prefix (we'll learn more about namespaces soon)
   - The `<<` operator is used to send data to cout

2. **std::endl**:
   - Ends the current line and flushes the output buffer
   - Equivalent to printing a newline character (`\n`) and flushing the buffer

3. **Semicolons**:
   - Each statement in C++ must end with a semicolon (`;`)
   - Missing semicolons are a common source of compiler errors

#### Making Our Program More Flexible

Let's enhance our program to add any two numbers provided by the user:

```cpp
#include <iostream>

int main() {
    int a, b;
    
    std::cout << "Enter the first number: ";
    std::cin >> a;
    
    std::cout << "Enter the second number: ";
    std::cin >> b;
    
    int sum = a + b;
    std::cout << a << " + " << b << " = " << sum << std::endl;
    
    return 0;
}
```

New concepts introduced:

1. **std::cin**:
   - Used to read input from the console
   - The `>>` operator extracts data from cin into variables

2. **Multiple variables**:
   - We declared two integer variables, `a` and `b`, on a single line

#### Using the Standard Namespace

To simplify our code, we can use the `using namespace std;` directive to avoid typing `std::` repeatedly:

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    
    cout << "Enter the first number: ";
    cin >> a;
    
    cout << "Enter the second number: ";
    cin >> b;
    
    int sum = a + b;
    cout << a << " + " << b << " = " << sum << endl;
    
    return 0;
}
```

#### Basic Data Types in C++

For our crossword puzzle project, we'll need to work with various data types. Here are the fundamental ones:

1. **int**: Integer values (e.g., 1, 42, -7)
2. **float**: Single-precision floating-point numbers (e.g., 3.14, -0.5)
3. **double**: Double-precision floating-point numbers (more precise than float)
4. **char**: Single characters (e.g., 'A', '7', '$')
5. **bool**: Boolean values (true or false)
6. **string**: Text strings (e.g., "Hello", "Crossword")

Let's modify our program to work with different data types:

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    // Integer addition
    int a = 5, b = 7;
    int sum = a + b;
    cout << "Integer: " << a << " + " << b << " = " << sum << endl;
    
    // Floating-point addition
    double x = 3.14, y = 2.71;
    double result = x + y;
    cout << "Double: " << x << " + " << y << " = " << result << endl;
    
    // String concatenation
    string first = "cross", second = "word";
    string combined = first + second;
    cout << "String: " << first << " + " << second << " = " << combined << endl;
    
    return 0;
}
```

#### Control Flow: if Statements

Let's introduce a basic control flow structure using an `if` statement:

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    
    cout << "Enter two numbers: ";
    cin >> a >> b;
    
    int sum = a + b;
    cout << a << " + " << b << " = " << sum << endl;
    
    if (sum > 10) {
        cout << "The sum is greater than 10!" << endl;
    } else if (sum == 10) {
        cout << "The sum is exactly 10!" << endl;
    } else {
        cout << "The sum is less than 10!" << endl;
    }
    
    return 0;
}
```

#### Functions in C++

Functions help us organize code into reusable blocks. Let's create a function to add two numbers:

```cpp
#include <iostream>
using namespace std;

// Function declaration
int add(int x, int y) {
    return x + y;
}

int main() {
    int a, b;
    
    cout << "Enter two numbers: ";
    cin >> a >> b;
    
    // Call the add function
    int sum = add(a, b);
    cout << a << " + " << b << " = " << sum << endl;
    
    return 0;
}
```

#### Conclusion

In this chapter, we've created our first C++ programs and learned the basic syntax for:
- Including libraries
- Writing the main function
- Declaring variables of different types
- Reading input and displaying output
- Using if statements for decision making
- Creating and calling functions

These fundamentals will serve as building blocks as we develop our crossword puzzle construction software in the upcoming chapters. In the next chapter, we'll begin working with more complex structures as we start loading and representing our crossword grid.

#### Practice Exercises

1. Modify the program to add three numbers instead of two.
2. Create a program that calculates the area of a rectangle (length × width).
3. Write a function that checks if a number is even or odd.
4. Create a program that converts a temperature from Celsius to Fahrenheit.

### 4. Load a Grid (part 1)
[https://youtu.be/Gs7H9GOZjow](https://youtu.be/Gs7H9GOZjow)
### 4. Load a Grid (part 1)

In this chapter, we'll take our first step toward building our crossword puzzle solver by creating code to load and represent a crossword grid. This is a fundamental component that we'll build upon in subsequent chapters.

#### Understanding Crossword Grid Representation

Before we dive into coding, let's understand how we'll represent a crossword grid programmatically:

1. A crossword grid is essentially a 2D array of characters
2. Each cell in the grid can contain:
   - A letter (A-Z)
   - A black square/block (we'll use '.' to represent these)
   - An empty space to be filled (we'll use '-' to represent these)
3. The grid has a fixed number of rows and columns

#### Introducing Vectors in C++

For our grid representation, we'll use a C++ data structure called a `vector`. Vectors are dynamic arrays that can grow or shrink in size.

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main() {
    // Declare a vector of strings
    vector<string> grid;
    
    // Print information about our (empty) vector
    cout << "Grid size: " << grid.size() << endl;
    
    return 0;
}
```

When you run this program, it will output:
```
Grid size: 0
```

This indicates that our grid vector is currently empty.

#### Adding Data to Our Grid

Now, let's add some rows to our grid to represent a simple crossword puzzle:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main() {
    // Declare a vector of strings
    vector<string> grid;
    
    // Add rows to our grid
    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    // Print grid size
    cout << "Grid size: " << grid.size() << endl;
    
    return 0;
}
```

Now when you run the program, it will output:
```
Grid size: 7
```

This indicates that our grid now has 7 rows.

#### Displaying the Grid

Let's modify our program to display the entire grid:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main() {
    // Declare a vector of strings
    vector<string> grid;
    
    // Add rows to our grid
    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    // Print grid size
    cout << "Grid size: " << grid.size() << endl;
    
    // Display the grid
    for (string row : grid) {
        cout << row << endl;
    }
    
    return 0;
}
```

This will output the entire grid, row by row:
```
Grid size: 7
DOG....
---....
----...
-------
...----
....---
...CATS
```

#### Analyzing Grid Dimensions

Let's add code to determine the dimensions of our grid:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main() {
    // Declare a vector of strings
    vector<string> grid;
    
    // Add rows to our grid
    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    // Calculate dimensions
    int rows = grid.size();
    int columns = 0;
    
    for (string row : grid) {
        // Find the maximum length of any row
        columns = max(columns, int(row.length()));
    }
    
    // Display grid and dimensions
    for (string row : grid) {
        cout << row << endl;
    }
    
    cout << "Rows: " << rows << endl;
    cout << "Columns: " << columns << endl;
    
    return 0;
}
```

The output will now include the grid dimensions:
```
DOG....
---....
----...
-------
...----
....---
...CATS
Rows: 7
Columns: 7
```

#### Range-Based For Loops vs. Traditional For Loops

In the examples above, we used a range-based for loop:
```cpp
for (string row : grid) {
    // Do something with row
}
```

This is a modern C++ feature that simplifies iteration. The equivalent traditional for loop would be:
```cpp
for (int i = 0; i < grid.size(); i++) {
    string row = grid[i];
    // Do something with row
}
```

Both approaches work, but the range-based loop is more concise and less prone to errors.

#### Ensuring Grid Consistency

A valid crossword grid should have all rows of the same length. Let's add some validation:

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <assert.h>

using namespace std;

int main() {
    // Declare a vector of strings
    vector<string> grid;
    
    // Add rows to our grid
    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    // Calculate dimensions
    int rows = grid.size();
    int cols = grid[0].size();  // Length of the first row
    
    // Validate grid
    for (string s : grid) {
        // All rows should have the same length
        assert(s.size() == cols);
    }
    
    // Display grid and dimensions
    for (string row : grid) {
        cout << row << endl;
    }
    
    cout << "Rows: " << rows << endl;
    cout << "Columns: " << cols << endl;
    
    return 0;
}
```

The `assert` statement is a debugging tool that will terminate the program if the condition is false. In this case, we're asserting that each row has the same length as the first row.

#### Using Algorithm Functions

Let's improve our grid analysis using C++ algorithm functions:

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <assert.h>
#include <algorithm>

using namespace std;

int main() {
    // Declare a vector of strings
    vector<string> grid;
    
    // Add rows to our grid
    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    // Calculate dimensions
    int rows = grid.size();
    
    // Find the maximum row length using std::max_element
    auto longest_row = max_element(grid.begin(), grid.end(), 
        [](const string& a, const string& b) {
            return a.length() < b.length();
        });
    
    int cols = longest_row->length();
    
    // Validate grid
    for (string s : grid) {
        assert(s.size() == cols);
    }
    
    // Display grid and dimensions
    for (string row : grid) {
        cout << row << endl;
    }
    
    cout << "Rows: " << rows << endl;
    cout << "Columns: " << cols << endl;
    
    return 0;
}
```

In this example, we used the `max_element` algorithm and a lambda function to find the longest row in the grid.

#### Conclusion

In this chapter, we've:
- Learned how to represent a crossword grid using a vector of strings
- Added data to our grid
- Displayed the grid
- Calculated and validated the grid dimensions
- Explored different C++ loop constructs and algorithms

We now have a basic structure for representing our crossword grid. In the next chapter, "Load a Grid (part 2)," we'll enhance this structure and start working with the grid content more deeply.

#### Practice Exercises

1. Modify the program to count how many cells contain letters (A-Z).
2. Add a function that counts how many cells are empty (-) and how many are blocks (.).
3. Create a function that checks if a grid is symmetrical (a common requirement for crossword puzzles).
4. Modify the program to accept a grid of different dimensions (e.g., 5×5, 10×10).
   
### 5. Load a Grid (part 2)
[https://youtu.be/aMBiDC-Az-c](https://youtu.be/aMBiDC-Az-c)
### 5. Load a Grid (part 2)

In this chapter, we'll expand on our grid loading functionality from Chapter 4. We'll refine our code to make it more robust and begin organizing our program structure to prepare for the more complex features we'll add in future chapters.

#### Review of Our Current Code

Let's start by reviewing the code we developed in Chapter 4:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>

using namespace std;

int main()
{
    vector<string> grid;

    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");

    cout << grid.size() << endl;

    int rows = grid.size();
    int columns = 0;
    int cols = grid[0].size();

    for (string s : grid) {
        cout << s << endl;
        columns = max(columns, int(s.length()));
        assert(s.size() == cols);
    }

    cout << "Rows : " << rows << endl;
    cout << "Columns : " << columns << endl;
}
```

This code successfully loads a simple grid and ensures all rows have the same length. Now, let's enhance it.

#### Understanding Character Representations

In our grid representation:
- Letters (A-Z) represent filled cells with specific letters
- Hyphens ('-') represent empty cells that need to be filled
- Periods ('.') represent black squares/blocks that separate words

Let's explore how characters are represented in C++:

```cpp
int main()
{
    // Characters are represented by their ASCII values
    int aa = 'A';
    cout << "The ASCII value of 'A' is: " << aa << endl;  // Outputs: 65
    
    // We can check character types
    char c = 'D';
    if (c >= 'A' && c <= 'Z') {
        cout << c << " is an uppercase letter" << endl;
    }
    
    c = '-';
    if (c == '-') {
        cout << c << " represents an empty cell" << endl;
    }
    
    c = '.';
    if (c == '.') {
        cout << c << " represents a black square" << endl;
    }
}
```

Understanding character representation will be important when we start parsing and manipulating the grid.

#### Grid Cell Access and Modification

Let's look at how we can access and modify individual cells in our grid:

```cpp
int main()
{
    vector<string> grid;

    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    // Access a specific cell (row 0, column 0)
    char topLeftCell = grid[0][0];
    cout << "Top left cell contains: " << topLeftCell << endl;
    
    // Access a specific cell (row 3, column 3)
    char middleCell = grid[3][3];
    cout << "Middle cell contains: " << middleCell << endl;
    
    // Modify a cell
    grid[1][0] = 'X';
    
    // Display the modified grid
    for (string row : grid) {
        cout << row << endl;
    }
}
```

This demonstrates how we can both read and write to specific cells in our grid.

#### Grid Analysis Functions

Let's create some functions to analyze our grid:

```cpp
// Count empty cells in the grid
int countEmptyCells(const vector<string>& grid) {
    int count = 0;
    for (const string& row : grid) {
        for (char cell : row) {
            if (cell == '-') {
                count++;
            }
        }
    }
    return count;
}

// Count black squares in the grid
int countBlackSquares(const vector<string>& grid) {
    int count = 0;
    for (const string& row : grid) {
        for (char cell : row) {
            if (cell == '.') {
                count++;
            }
        }
    }
    return count;
}

// Count letter cells in the grid
int countLetterCells(const vector<string>& grid) {
    int count = 0;
    for (const string& row : grid) {
        for (char cell : row) {
            if (cell >= 'A' && cell <= 'Z') {
                count++;
            }
        }
    }
    return count;
}

int main()
{
    vector<string> grid;

    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    // Analyze the grid
    cout << "Empty cells: " << countEmptyCells(grid) << endl;
    cout << "Black squares: " << countBlackSquares(grid) << endl;
    cout << "Letter cells: " << countLetterCells(grid) << endl;
}
```

These functions help us understand the composition of our grid.

#### Working with Nested Loops

When working with a 2D grid, we often need to use nested loops. Let's practice with some examples:

```cpp
// Print the grid with row and column coordinates
void printGridWithCoordinates(const vector<string>& grid) {
    // Print column headers
    cout << "  ";
    for (int col = 0; col < grid[0].size(); col++) {
        cout << col;
    }
    cout << endl;
    
    // Print rows with row numbers
    for (int row = 0; row < grid.size(); row++) {
        cout << row << " " << grid[row] << endl;
    }
}

// Check if the grid has symmetry (common in crossword puzzles)
bool hasRotationalSymmetry(const vector<string>& grid) {
    int rows = grid.size();
    int cols = grid[0].size();
    
    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {
            // Check if a cell and its opposite have the same block/non-block status
            char cell = grid[r][c];
            char oppositeCell = grid[rows - 1 - r][cols - 1 - c];
            
            bool isBlock = (cell == '.');
            bool isOppositeBlock = (oppositeCell == '.');
            
            if (isBlock != isOppositeBlock) {
                return false;
            }
        }
    }
    return true;
}

int main()
{
    vector<string> grid;

    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    printGridWithCoordinates(grid);
    
    if (hasRotationalSymmetry(grid)) {
        cout << "The grid has rotational symmetry." << endl;
    } else {
        cout << "The grid does not have rotational symmetry." << endl;
    }
}
```

Nested loops allow us to efficiently process all cells in the grid.

#### Assertions for Grid Validation

In our previous code, we used assertions to validate the grid. Let's expand on this:

```cpp
void validateGrid(const vector<string>& grid) {
    // Check that the grid is not empty
    assert(!grid.empty() && "Grid cannot be empty");
    
    int rows = grid.size();
    int cols = grid[0].size();
    
    // Check that all rows have the same length
    for (const string& row : grid) {
        assert(row.size() == cols && "All rows must have the same length");
    }
    
    // Check that all characters are valid
    for (const string& row : grid) {
        for (char cell : row) {
            assert((cell == '.' || cell == '-' || (cell >= 'A' && cell <= 'Z')) && 
                   "Grid cells must contain only '.', '-', or uppercase letters A-Z");
        }
    }
    
    cout << "Grid validation passed!" << endl;
}

int main()
{
    vector<string> grid;

    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    validateGrid(grid);
}
```

Assertions help us catch potential issues early in development.

#### Putting It All Together

Let's combine everything we've learned to create a comprehensive grid loading and analysis program:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>

using namespace std;

// Grid validation and analysis functions
void validateGrid(const vector<string>& grid) {
    // Check that the grid is not empty
    assert(!grid.empty() && "Grid cannot be empty");
    
    int rows = grid.size();
    int cols = grid[0].size();
    
    // Check that all rows have the same length
    for (const string& row : grid) {
        assert(row.size() == cols && "All rows must have the same length");
    }
    
    // Check that all characters are valid
    for (const string& row : grid) {
        for (char cell : row) {
            assert((cell == '.' || cell == '-' || (cell >= 'A' && cell <= 'Z')) && 
                   "Grid cells must contain only '.', '-', or uppercase letters A-Z");
        }
    }
}

int countEmptyCells(const vector<string>& grid) {
    int count = 0;
    for (const string& row : grid) {
        for (char cell : row) {
            if (cell == '-') {
                count++;
            }
        }
    }
    return count;
}

int countBlackSquares(const vector<string>& grid) {
    int count = 0;
    for (const string& row : grid) {
        for (char cell : row) {
            if (cell == '.') {
                count++;
            }
        }
    }
    return count;
}

int countLetterCells(const vector<string>& grid) {
    int count = 0;
    for (const string& row : grid) {
        for (char cell : row) {
            if (cell >= 'A' && cell <= 'Z') {
                count++;
            }
        }
    }
    return count;
}

bool hasRotationalSymmetry(const vector<string>& grid) {
    int rows = grid.size();
    int cols = grid[0].size();
    
    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {
            char cell = grid[r][c];
            char oppositeCell = grid[rows - 1 - r][cols - 1 - c];
            
            bool isBlock = (cell == '.');
            bool isOppositeBlock = (oppositeCell == '.');
            
            if (isBlock != isOppositeBlock) {
                return false;
            }
        }
    }
    return true;
}

void printGridInfo(const vector<string>& grid) {
    int rows = grid.size();
    int cols = grid[0].size();
    
    cout << "Grid dimensions: " << rows << " rows × " << cols << " columns" << endl;
    cout << "Empty cells: " << countEmptyCells(grid) << endl;
    cout << "Black squares: " << countBlackSquares(grid) << endl;
    cout << "Letter cells: " << countLetterCells(grid) << endl;
    
    if (hasRotationalSymmetry(grid)) {
        cout << "The grid has rotational symmetry." << endl;
    } else {
        cout << "The grid does not have rotational symmetry." << endl;
    }
}

int main()
{
    vector<string> grid;

    grid.push_back("DOG....");
    grid.push_back("---....");
    grid.push_back("----...");
    grid.push_back("-------");
    grid.push_back("...----");
    grid.push_back("....---");
    grid.push_back("...CATS");
    
    // Validate the grid
    validateGrid(grid);
    
    // Display the grid
    cout << "Crossword Grid:" << endl;
    for (const string& row : grid) {
        cout << row << endl;
    }
    cout << endl;
    
    // Print grid analysis
    printGridInfo(grid);
    
    return 0;
}
```

This program provides a solid foundation for loading and analyzing crossword grids.

#### Conclusion

In this chapter, we've significantly enhanced our grid loading and analysis capabilities:

1. We've learned how to access and modify specific cells in the grid
2. We've created utility functions to analyze the grid content
3. We've implemented validation functions to ensure grid consistency
4. We've explored nested loops for processing 2D grids
5. We've added functionality to check for grid symmetry

In the next chapter, we'll start organizing our code into a more structured format by creating a Grid class, which will encapsulate the functionality we've developed so far.

#### Practice Exercises

1. Add a function to check if all words in the grid have a minimum length of 3 (a common crossword rule).
2. Create a function that identifies all the starting points of words in the grid.
3. Implement a function that counts the number of across and down words in the grid.
4. Add functionality to convert the grid to a different format (e.g., using '#' for blocks instead of '.').

### 6. The Grid Object
[https://youtu.be/aJELHElkBTo](https://youtu.be/aJELHElkBTo)
### 6. The Grid Object

In this chapter, we'll refactor our grid code from Chapters 4 and 5 into a proper C++ object. This represents a fundamental step in our journey from procedural programming to object-oriented programming, which will make our crossword solver more maintainable and extensible.

#### Why Create a Grid Object?

Before we start coding, let's understand why we're creating a Grid object:

1. **Encapsulation**: Group related data (the grid contents) and functions (grid operations) together
2. **Organization**: Make our code more structured and easier to navigate
3. **Reusability**: Allow grid functionality to be easily reused in different parts of our program
4. **Abstraction**: Hide implementation details and provide a clear interface

#### Understanding C++ Structs

For our Grid object, we'll start by using a C++ struct. A struct in C++ is similar to a class, but with all members public by default.

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>

using namespace std;

struct Grid {
    // Data members
    vector<string> lines;
    string name;
    
    // Function members will go here
};

int main() {
    Grid grid;
    grid.name = "My First Grid";
    grid.lines.push_back("DOG....");
    
    cout << "Grid name: " << grid.name << endl;
    cout << "First line: " << grid.lines[0] << endl;
    
    return 0;
}
```

#### Adding a Constructor

Let's add a constructor to initialize our Grid with a name:

```cpp
struct Grid {
    // Constructor
    Grid(string n) {
        name = n;
    }
    
    // Data members
    vector<string> lines;
    string name;
};

int main() {
    Grid grid("My First Grid");
    grid.lines.push_back("DOG....");
    
    cout << "Grid name: " << grid.name << endl;
    cout << "First line: " << grid.lines[0] << endl;
    
    return 0;
}
```

#### Adding Member Functions

Now, let's add member functions to query grid properties:

```cpp
struct Grid {
    // Constructor
    Grid(string n) {
        name = n;
    }
    
    // Member functions
    int rows() const { 
        return lines.size(); 
    }
    
    int cols() const {
        if (lines.empty()) {
            return 0;
        } else {
            return lines[0].size(); 
        }
    }
    
    // Data members
    vector<string> lines;
    string name;
};

int main() {
    Grid grid("My First Grid");
    grid.lines.push_back("DOG....");
    grid.lines.push_back("---....");
    
    cout << "Grid name: " << grid.name << endl;
    cout << "Rows: " << grid.rows() << endl;
    cout << "Columns: " << grid.cols() << endl;
    
    return 0;
}
```

Note the `const` keyword in function declarations. This indicates that these functions don't modify the Grid object, which is important for code safety and optimization.

#### Loading and Checking Grid Data

Let's add functions to load grid data and check its validity:

```cpp
struct Grid {
    Grid(string n) {
        name = n;
    }

    int rows() const { 
        return lines.size(); 
    }

    int cols() const {
        if (lines.empty()) {
            return 0;
        } else {
            return lines[0].size(); 
        }
    }
    
    void Load() {
        lines.push_back("DOG....");
        lines.push_back("---....");
        lines.push_back("----...");
        lines.push_back("-------");
        lines.push_back("...----");
        lines.push_back("....---");
        lines.push_back("...CATS");
    }

    int Check() const {
        for (string s : lines) {
            assert(s.size() == cols());
        }
        return 0;
    }
    
    vector<string> lines;
    string name;
};

int main() {
    Grid grid("Hello Grid");
    
    grid.Load();
    grid.Check();
    
    cout << "Grid loaded and checked successfully." << endl;
    cout << "Rows: " << grid.rows() << endl;
    cout << "Columns: " << grid.cols() << endl;
    
    return 0;
}
```

#### Adding a Print Function

Now, let's add a function to print the grid:

```cpp
struct Grid {
    Grid(string n) {
        name = n;
    }

    int rows() const { 
        return lines.size(); 
    }

    int cols() const {
        if (lines.empty()) {
            return 0;
        } else {
            return lines[0].size(); 
        }
    }
    
    void Load() {
        lines.push_back("DOG....");
        lines.push_back("---....");
        lines.push_back("----...");
        lines.push_back("-------");
        lines.push_back("...----");
        lines.push_back("....---");
        lines.push_back("...CATS");
    }

    int Check() const {
        for (string s : lines) {
            assert(s.size() == cols());
        }
        return 0;
    }
    
    int Print() const {
        cout << "Grid : " << name << endl << endl;
        
        for (string s : lines) {
            cout << s << endl;
        }
        
        cout << endl << "Rows : " << rows() << endl;
        cout << "Columns : " << cols() << endl;
        
        return 0;
    }
    
    vector<string> lines;
    string name;
};

int main() {
    Grid grid("Hello Grid");
    
    grid.Load();
    grid.Check();
    grid.Print();
    
    return 0;
}
```

#### Putting It All Together

Here's our complete Grid object code, which forms the foundation for our crossword solver:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>

using namespace std;

struct Grid {

    Grid(string n) {
        name = n;
    }

    int rows() const { return lines.size(); }

    int cols() const {
        
        if (lines.empty()) {
            return 0;
        }
        else {
            return lines[0].size(); 
        }
    }

    void Load() {
        lines.push_back("DOG....");
        lines.push_back("---....");
        lines.push_back("----...");
        lines.push_back("-------");
        lines.push_back("...----");
        lines.push_back("....---");
        lines.push_back("...CATS");
    }

    int Check() const {
        for (string s : lines) {
            assert(s.size() == cols());
        }
        return 0;
    }
    
    int Print() const {
        cout << "Grid : " << name << endl << endl;

        for (string s : lines) {
            cout << s << endl;
        }

        cout << endl << "Rows : " << rows() << endl;
        cout << "Columns : " << cols() << endl;

        return 0;
    }

    vector<string> lines;
    string name;
};

int main()
{
    Grid grid("Hello Grid");

    grid.Load();
    grid.Check();
    grid.Print();
    
    return 0;
};
```

#### Understanding Object-Oriented Design

With our Grid object, we've taken a significant step toward object-oriented programming:

1. **Encapsulation**: We've grouped the grid data (lines, name) and operations (rows, cols, Load, Check, Print) into a single unit.

2. **Abstraction**: We've defined a clear interface for interacting with the grid, hiding the internal details.

3. **Const Correctness**: We've marked functions that don't modify the object as `const`, which helps prevent bugs and enables certain optimizations.

In C++, structs and classes are very similar:
- The only difference is that struct members are public by default, while class members are private by default.
- As our code becomes more complex, we might choose to convert our struct to a class and make some members private for better encapsulation.

#### Adding Grid Cell Access Functions

Let's enhance our Grid object with functions to access and check individual cells:

```cpp
struct Grid {
    // ... previous code ...
    
    // Returns character value of the box at row r, column c
    char box(int r, int c) const {
        assert(r >= 0 && r < rows());
        assert(c >= 0 && c < cols());
        return lines[r][c];
    }
    
    // Returns true if the cell is a block ('.')
    bool is_block(int r, int c) const {
        return box(r, c) == '.';
    }
    
    // Returns true if the cell is empty ('-')
    bool is_empty(int r, int c) const {
        return box(r, c) == '-';
    }
    
    // Returns true if the cell contains a letter
    bool is_letter(int r, int c) const {
        char ch = box(r, c);
        return ch >= 'A' && ch <= 'Z';
    }
    
    // ... remaining code ...
};
```

These functions provide a cleaner way to access and check grid cells, adding another layer of abstraction.

#### Advanced Cell Manipulation

We can also add functions to modify grid cells:

```cpp
struct Grid {
    // ... previous code ...
    
    // Set a cell to a specific character
    void set_box(int r, int c, char ch) {
        assert(r >= 0 && r < rows());
        assert(c >= 0 && c < cols());
        lines[r][c] = ch;
    }
    
    // Fill an empty cell with a letter
    bool fill_cell(int r, int c, char letter) {
        if (is_empty(r, c)) {
            set_box(r, c, letter);
            return true;
        }
        return false;
    }
    
    // Clear a letter cell, making it empty
    bool clear_cell(int r, int c) {
        if (is_letter(r, c)) {
            set_box(r, c, '-');
            return true;
        }
        return false;
    }
    
    // ... remaining code ...
};
```

#### Conclusion

In this chapter, we've transformed our grid code into a well-structured C++ object. This represents a significant step in our software development journey, moving from procedural to object-oriented programming.

Our Grid object:
- Encapsulates grid data and operations
- Provides a clear interface for grid interactions
- Uses const correctness for safer code
- Adds abstraction for cell access and manipulation

In the next chapter, we'll enhance our Grid object by adding functionality to load grid data from a file, which will make our program much more flexible.

#### Practice Exercises

1. Add a function to create an empty grid of a specified size.
2. Implement a function to check if the grid is completely filled (no empty cells).
3. Add a function to count how many words (sequences of 2 or more letters/empty cells) are in the grid.
4. Create a function that checks if the grid follows standard crossword rules (e.g., no 1 or 2-letter words, all words connected).
5. Implement a function to create a new grid that is the transpose of the original (rows become columns and vice versa).

### 7. Read the Grid from a File
[https://youtu.be/mibylIzx_sE](https://youtu.be/mibylIzx_sE)
### 7. Read the Grid from a File

In this chapter, we'll enhance our Grid object by adding functionality to read grid data from a file. This is a crucial step in making our crossword puzzle solver more practical and versatile, as it will allow us to easily work with different grid layouts without modifying our code.

#### Why Read from Files?

Until now, we've been hard-coding our grid data directly in the program. This works for testing but has several limitations:

1. Every time we want to use a different grid, we need to modify and recompile the code
2. Storing large grids in the code is unwieldy
3. Non-programmers can't easily create or modify grid layouts

By reading from files, we address all these issues and make our program more flexible.

#### Introduction to File I/O in C++

C++ provides several ways to work with files. For our purposes, we'll use the standard library's file stream classes:

```cpp
#include <fstream> // Required for file operations
```

The main classes we'll use are:

- `ifstream`: Input file stream (for reading from files)
- `ofstream`: Output file stream (for writing to files)
- `fstream`: General file stream (for both reading and writing)

#### Basic File Reading

Let's start with a simple example of reading from a file:

```cpp
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

int main() {
    ifstream inFile;
    inFile.open("test.txt");
    
    if (!inFile) {
        cerr << "Unable to open file test.txt";
        return 1;
    }
    
    string line;
    while (getline(inFile, line)) {
        cout << line << endl;
    }
    
    inFile.close();
    return 0;
}
```

This code:
1. Creates an input file stream
2. Opens the file "test.txt"
3. Checks if the file was opened successfully
4. Reads the file line by line
5. Closes the file when done

#### File Format for Grid Data

Before we implement file reading in our Grid class, let's establish a simple file format for our grid data:

- Each line in the file represents a row in the grid
- Comments can be included with a '#' at the start of the line
- Empty lines are ignored

Example file content (`test.txt`):
```
# This is a comment - it will be ignored
DOG....
---....
----...
-------
...----
....---
...CATS
```

#### Handling Line Endings in Different Operating Systems

When working with text files, we need to be aware of different line ending conventions:

- Windows: `'\r\n'` (carriage return + line feed)
- Unix/Linux/macOS: `'\n'` (line feed only)
- Classic Mac (OS 9 and earlier): `'\r'` (carriage return only)

Our file reading code should handle these differences gracefully. The `getline` function helps with this, but we may still need to handle trailing `'\r'` characters.

#### Adding File Reading to Our Grid Class

Now, let's enhance our Grid struct to include a method for loading grid data from a file:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>
#include <fstream>

using namespace std;

struct Grid {

    Grid(string n) {
        name = n;
    }

    int rows() const { return lines.size(); }

    int cols() const {
        if (lines.empty()) {
            return 0;
        }
        else {
            return lines[0].size(); 
        }
    }

    void LoadFromFile(string filename) {
        ifstream f;
        f.open(filename);
        
        if (!f) {
            cerr << "Unable to open file " << filename << endl;
            return;
        }
        
        while (!f.eof()) {
            string line;
            getline(f, line);
            
            // Skip empty lines and comments
            if (!line.empty() && line[0] != '#') {
                lines.push_back(line);
            }
        }
        
        f.close();
    }

    int Check() const {
        for (string s : lines) {
            assert(s.size() == cols());
        }
        return 0;
    }
    
    int Print() const {
        cout << "Grid : " << name << endl << endl;

        for (string s : lines) {
            cout << s << endl;
        }

        cout << endl << "Rows : " << rows() << endl;
        cout << "Columns : " << cols() << endl;

        return 0;
    }

    vector<string> lines;
    string name;
};

int main() {
    Grid grid("MY GRID");

    grid.LoadFromFile("test.txt");
    grid.Check();
    grid.Print();
    
    return 0;
}
```

In this code, we've added a `LoadFromFile` method that:
1. Opens the specified file
2. Reads it line by line
3. Skips empty lines and comments
4. Adds valid lines to our grid data
5. Closes the file when done

#### Handling Windows/Unix Line Ending Differences

In some cases, we might need to explicitly handle carriage return characters, especially when working with files created on different operating systems:

```cpp
void LoadFromFile(string filename) {
    ifstream f;
    f.open(filename);
    
    if (!f) {
        cerr << "Unable to open file " << filename << endl;
        return;
    }
    
    while (!f.eof()) {
        string line;
        getline(f, line);
        
        // Remove carriage return if present (for Windows files read on Unix)
        if (!line.empty() && line[line.length() - 1] == '\r') {
            line = line.substr(0, line.length() - 1);
        }
        
        // Skip empty lines and comments
        if (!line.empty() && line[0] != '#') {
            lines.push_back(line);
        }
    }
    
    f.close();
}
```

#### Understanding Character Processing

When working with text files and character data, it's useful to understand how characters are represented in C++:

```cpp
int main() {
    // Characters are represented by their ASCII values
    int aa = 'A';
    cout << "The ASCII value of 'A' is: " << aa << endl;  // Outputs: 65
    
    // We can test this with our grid data
    string s = "DOG";
    for (char c : s) {
        int val = c;
        cout << "Character '" << c << "' has ASCII value " << val << endl;
    }
    
    return 0;
}
```

This shows that each character is represented by a numeric value according to the ASCII standard.

#### Handling File Opening Errors

In a robust application, we should provide proper error handling for file operations:

```cpp
void LoadFromFile(string filename) {
    ifstream f;
    f.open(filename);
    
    if (!f.is_open()) {
        cerr << "Error: Unable to open file '" << filename << "'" << endl;
        return;
    }
    
    lines.clear();  // Clear any existing data
    
    while (!f.eof()) {
        string line;
        getline(f, line);
        
        // Remove carriage return if present
        if (!line.empty() && line[line.length() - 1] == '\r') {
            line = line.substr(0, line.length() - 1);
        }
        
        // Skip empty lines and comments
        if (!line.empty() && line[0] != '#') {
            lines.push_back(line);
        }
    }
    
    f.close();
    
    if (lines.empty()) {
        cerr << "Warning: No valid grid data found in file '" << filename << "'" << endl;
    }
}
```

This version:
1. Checks if the file was opened successfully
2. Clears any existing grid data
3. Warns if no valid grid data was found in the file

#### Putting It All Together

Here's our complete Grid class with file reading capabilities:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>
#include <fstream>

using namespace std;

struct Grid {

    Grid(string n) {
        name = n;
    }

    int rows() const { return lines.size(); }

    int cols() const {
        if (lines.empty()) {
            return 0;
        }
        else {
            return lines[0].size(); 
        }
    }

    void LoadFromFile(string filename) {
        ifstream f;
        f.open(filename);
        
        if (!f.is_open()) {
            cerr << "Error: Unable to open file '" << filename << "'" << endl;
            return;
        }
        
        lines.clear();  // Clear any existing data
        
        while (!f.eof()) {
            string line;
            getline(f, line);
            
            // Remove carriage return if present
            if (!line.empty() && line[line.length() - 1] == '\r') {
                line = line.substr(0, line.length() - 1);
            }
            
            // Skip empty lines and comments
            if (!line.empty() && line[0] != '#') {
                lines.push_back(line);
            }
        }
        
        f.close();
        
        if (lines.empty()) {
            cerr << "Warning: No valid grid data found in file '" << filename << "'" << endl;
        }
    }

    int Check() const {
        for (string s : lines) {
            assert(s.size() == cols());
        }
        return 0;
    }
    
    int Print() const {
        cout << "Grid : " << name << endl << endl;

        for (string s : lines) {
            cout << s << endl;
        }

        cout << endl << "Rows : " << rows() << endl;
        cout << "Columns : " << cols() << endl;

        return 0;
    }

    vector<string> lines;
    string name;
};

int main() {
    Grid grid("MY GRID");

    grid.LoadFromFile("test.txt");
    grid.Check();
    grid.Print();
    
    return 0;
}
```

#### File Paths and Working Directories

When specifying filenames, it's important to understand how file paths are resolved:

1. **Relative Paths**: Files are located relative to the current working directory.
   - If you specify `"test.txt"`, the file is looked for in the directory where the program is executed.
   - If you specify `"data/test.txt"`, the file is looked for in a subdirectory named "data".

2. **Absolute Paths**: Files are located using a complete path from the root of the file system.
   - On Windows: `"C:\\Users\\Username\\Documents\\test.txt"`
   - On Unix/Linux/macOS: `"/home/username/documents/test.txt"`

In most cases, using relative paths is more portable across different systems.

#### Conclusion

In this chapter, we've enhanced our Grid object by adding the ability to read grid data from files. This makes our crossword puzzle solver much more flexible and user-friendly, as we can now easily work with different grid layouts without modifying our code.

We've covered:
- Basic file I/O in C++
- Creating a simple file format for grid data
- Handling differences in line endings between operating systems
- Character representation and processing
- Proper error handling for file operations
- Understanding file paths and working directories

In the next chapter, we'll continue building our crossword solver by adding functionality to read a dictionary of words from a file, which we'll use to fill the empty cells in our grid.

#### Practice Exercises

1. Enhance the `LoadFromFile` method to validate that all rows in the file have the same length.
2. Add a method to save the current grid to a file.
3. Implement a function that can import grid data from a different file format (e.g., CSV).
4. Add support for a grid file format that includes metadata (e.g., grid title, author).
5. Create a function that can merge two grid files, combining their data into a single grid.

### 8. Read the Library from a File
[https://youtu.be/xxQWf-60hI8 ](https://youtu.be/xxQWf-60hI8 )
### 8. Read the Library from a File

In this chapter, we'll expand our crossword puzzle solver by adding a Library class that reads and manages a dictionary of words. This library will be used to find suitable words to fill our crossword grid.

#### Why Create a Library Class?

For our crossword puzzle solver, we need a dictionary of valid words that we can search through. The Library class will:

1. Load words from a file
2. Store them efficiently in memory
3. Allow us to search for words matching specific patterns
4. Provide statistics about the available words

#### Understanding Classes in C++

So far, we've been using structs for our objects. In this chapter, we'll use a class instead. The main difference between struct and class in C++ is the default access level:

- `struct`: Members are public by default
- `class`: Members are private by default

Using a class helps us enforce better encapsulation, as we'll need to explicitly decide which members to make public.

```cpp
class Library {
public:
    // Public methods go here
    
private:
    // Private data members go here
};
```

#### Setting Up the Library Class

Let's start by defining our Library class structure:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>
#include <fstream>

using namespace std;

class Library {
public:
    void ReadFromFile(string filename);
    string GetWord(int i) const;
    void ComputeStats();
    void PrintStats() const;
    
private:
    vector<string> words;
    vector<int> counts;
};
```

In this initial structure:
- `words` will store all the words from our dictionary
- `counts` will store statistics about word lengths
- Public methods provide an interface to interact with the library

#### Reading Words from a File

Now, let's implement the `ReadFromFile` method:

```cpp
void Library::ReadFromFile(string filename) {
    ifstream f;
    f.open(filename);
    
    if (!f.is_open()) {
        cerr << "Error: Unable to open file '" << filename << "'" << endl;
        return;
    }
    
    while (!f.eof()) {
        string line;
        getline(f, line);
        
        if (!line.empty()) {
            // Convert to uppercase for consistency
            for (char& c : line) {
                c = toupper(c);
            }
            
            // Remove carriage return if present
            int len = line.length();
            if (len > 0 && line[len - 1] == '\r') {
                line = line.substr(0, len - 1);
            }
            
            words.push_back(line);
        }
    }
    
    f.close();
    
    cout << "Read " << words.size() << " words from file '" << filename << "'" << endl;
}
```

This method:
1. Opens the specified file
2. Reads it line by line, considering each line as a word
3. Converts each word to uppercase for consistency
4. Removes any trailing carriage returns
5. Adds valid words to our vector
6. Displays how many words were read

#### Converting to Uppercase

Notice that we're converting all words to uppercase. This is a common approach in crossword puzzles, where typically all letters are uppercase. By standardizing our data, we make pattern matching simpler.

We could also create a helper function for this:

```cpp
string ToUpper(string s) {
    string result = s;
    for (char& c : result) {
        c = toupper(c);
    }
    return result;
}

// Then in ReadFromFile:
line = ToUpper(line);
```

#### Accessing Words

We'll need a way to access words from our library:

```cpp
string Library::GetWord(int i) const {
    assert(i >= 0 && i < words.size());
    return words[i];
}
```

This method provides safe access to individual words, with bounds checking via assert.

#### Computing and Displaying Statistics

To better understand our word library, let's add methods to compute and display statistics about word lengths:

```cpp
void Library::ComputeStats() {
    assert(counts.empty());
    // Resize vector that won't grow in time
    // Vector initialized to 0
    counts.resize(18);  // Assuming no words longer than 17 characters
    
    for (string s : words) {
        int len = s.length();
        if (len < 18) {
            counts[len]++;
        }
    }
}

void Library::PrintStats() const {
    for (int i = 1; i < counts.size(); i++) {
        cout << counts[i] << " words of " << i << " character(s)" << endl;
    }
}
```

The `ComputeStats` method creates a histogram of word lengths, and `PrintStats` displays this information.

#### Creating a Word Structure

As our project evolves, we'll need more information about words than just the string itself. Let's create a Word structure to encapsulate word-related data:

```cpp
struct Word {
    Word() {}
    Word(string s) : word(s) {}
    string word;
};
```

Now, let's modify our Library class to use this structure:

```cpp
class Library {
public:
    void ReadFromFile(string filename);
    string GetWord(int i) const;
    void ComputeStats();
    void PrintStats() const;
    
private:
    vector<Word> words;
    vector<int> counts;
};

void Library::ReadFromFile(string filename) {
    // Same as before, but using Word objects
    // ...
    words.push_back(Word(line));
    // ...
}

string Library::GetWord(int i) const {
    assert(i >= 0 && i < words.size());
    return words[i].word;
}

void Library::ComputeStats() {
    assert(counts.empty());
    counts.resize(18);
    
    for (Word w : words) {
        int len = w.word.length();
        if (len < 18) {
            counts[len]++;
        }
    }
}
```

#### Examining Character Encodings

When working with word lists, it's important to understand character encodings:

```cpp
void Library::ReadFromFile(string filename) {
    // ... existing code ...
    
    // Debugging: Examine the first word's characters
    if (!words.empty()) {
        cout << words[0].word << endl;
        cout << words[0].word.length() << endl;
        
        for (char c : words[0].word) {
            int x = c;
            cout << c << " " << x << endl;
        }
    }
    
    // ... rest of the method ...
}
```

This code prints each character in the first word along with its ASCII value, which can help identify encoding issues.

#### Putting It All Together

Here's our complete Library class implementation:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>
#include <fstream>

using namespace std;

// Helper function to convert a string to uppercase
string ToUpper(string s) {
    string s2;
    for (char c : s) {
        s2.push_back(toupper(c));
    }
    return s2;
}

struct Word {
    Word() {}
    Word(string s) : word(s) {}
    string word;
};

class Library {
public:
    void ComputeStats() {
        assert(counts.empty());
        // resize vector that don't grow in time
        // vector initialized to 0
        counts.resize(18);
        for (Word w : words) {
            int len = w.word.length();
            if (len < 18) {
                counts[len]++;
            }
        }
    }

    void PrintStats() const {
        for (int i = 1; i < counts.size(); i++) {
            cout << counts[i] << " words of " << i << " character(s) " << endl;
        }
    }

    string GetWord(int i) const {
        assert(i >= 0 && i < words.size());
        return words[i].word;
    }

    void ReadFromFile(string filename) {
        ifstream f;
        f.open(filename);
        
        if (!f.is_open()) {
            cerr << "Error: Unable to open file '" << filename << "'" << endl;
            return;
        }
        
        while (!f.eof()) {
            string line;
            getline(f, line);
            
            if (!line.empty()) {
                line = ToUpper(line);
                int len = line.length();
                if (len > 0 && line[len - 1] == '\r') {
                    line = line.substr(0, len - 1);
                }
                words.push_back(Word(line));
            }
        }

        // Debugging output for the first word
        if (!words.empty()) {
            cout << words[0].word << endl;
            cout << words[0].word.length() << endl;
            for (char c : words[0].word) {
                int x = c;
                cout << c << " " << x << endl;
            }
        }

        f.close();

        cout << "Read " << words.size() << " words from file '" << filename << "'" << endl;
    }

private:
    vector<Word> words;
    vector<int> counts;
};

struct Grid {
    // ... Grid implementation from previous chapter ...
};

int main() {
    Library lib;
    lib.ReadFromFile("top_12000.txt");
    
    cout << lib.GetWord(876) << endl;  // Display a random word
    
    lib.ComputeStats();
    lib.PrintStats();
    
    return 0;
}
```

#### Public vs. Private in Classes

Notice how we've structured our Library class with:

- Public methods (`ReadFromFile`, `GetWord`, `ComputeStats`, `PrintStats`) that form our interface
- Private data members (`words`, `counts`) that store the internal state

This distinction is a key aspect of object-oriented programming. By making our data members private:

1. We control how they can be accessed and modified
2. We can ensure they remain in a consistent state
3. We can change the internal implementation without affecting code that uses our class

#### The Difference Between Struct and Class

In our code, we use both structs (for Word and Grid) and classes (for Library). The practical difference is:

```cpp
struct Word {
    // Members are public by default
    string word;
};

class Library {
    // Members are private by default
    vector<Word> words;  // This is private
public:
    // We explicitly make these methods public
    void ReadFromFile(string filename);
};
```

As a general rule of thumb:
- Use structs for simple data containers with public members
- Use classes when you need more encapsulation and control

#### Conclusion

In this chapter, we've built a Library class that reads and manages a dictionary of words for our crossword puzzle solver. We've introduced:

1. The concept of classes in C++
2. Public vs. private members
3. Encapsulation of related data and operations
4. Reading and processing a word list
5. Computing and displaying statistics about our word library

With our Grid and Library classes now in place, we have the foundation for our crossword puzzle solver. In the next chapter, we'll implement methods to search our library for words matching specific patterns, which is essential for filling crossword grids.

#### Practice Exercises

1. Enhance the Library class to filter out words with special characters or numbers.
2. Add a method to find the longest and shortest words in the library.
3. Implement a function to save a subset of words (e.g., words of a specific length) to a new file.
4. Create a method to search for words containing a specific substring.
5. Add functionality to import words from multiple files into a single library.

### 9. Search the Library
[https://youtu.be/s-0j5KZ92-E ](https://youtu.be/s-0j5KZ92-E )
### 9. Search the Library

In this chapter, we'll implement functionality to search our word library for specific patterns. This is a crucial component of our crossword puzzle solver, as we need to efficiently find words that match the constraints imposed by the crossword grid.

#### The Pattern Matching Problem

When solving a crossword puzzle, we often have partial information about a word. For example, we might know that it's a 3-letter word with 'D' as the first letter. We need a way to quickly find all words in our library that match this pattern.

In our case, patterns will consist of:
- Uppercase letters (A-Z) for known positions
- Dashes ('-') for unknown positions

For example:
- "D--" matches any 3-letter word starting with 'D'
- "--G" matches any 3-letter word ending with 'G'
- "C-T" matches any 3-letter word starting with 'C' and ending with 'T'

#### Naive Approach: Linear Search

The simplest way to find matching words is to scan through the entire library and check each word against our pattern:

```cpp
vector<string> FindMatches(const vector<string>& words, const string& pattern) {
    vector<string> matches;
    
    for (const string& word : words) {
        if (word.length() == pattern.length()) {
            bool isMatch = true;
            
            for (int i = 0; i < pattern.length(); i++) {
                if (pattern[i] != '-' && pattern[i] != word[i]) {
                    isMatch = false;
                    break;
                }
            }
            
            if (isMatch) {
                matches.push_back(word);
            }
        }
    }
    
    return matches;
}
```

While this approach works, it's inefficient for large word libraries because we need to check every word for each search.

#### Hash-Based Approach

To improve efficiency, we'll use a hash-based approach. We'll create "buckets" of words based on a hash of their pattern, which will allow us to quickly look up matches.

Let's start by creating a simple hashing function:

```cpp
const int num_buckets = 1001;

int bucket(string s) {
    assert(!s.empty());
    unsigned int i = 0;
    for (char c : s) {
        i = (i * 217) + c;
    }
    int b = i % num_buckets;

    assert(b >= 0 && b < num_buckets);
    return b;
}
```

This function:
1. Takes a string as input
2. Computes a hash value based on its characters
3. Returns a bucket index between 0 and num_buckets-1

#### Organizing Words into Buckets

Now, let's modify our Library class to use this hashing approach:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>
#include <fstream>

using namespace std;

string ToUpper(string s) {
    string s2;

    for (char c : s) {
        s2.push_back(toupper(c));
    }
    return s2;
};

struct Word {
    Word(string s) {
        word = s;
    }
    string word;
};
typedef vector<Word> Words;

const int num_buckets = 1001;

int bucket(string s) {
    assert(!s.empty());
    unsigned int i = 0;
    for (char c : s) {
        i = (i * 217) + c;
    }
    int b = i % num_buckets;

    assert(b >= 0 && b < num_buckets);
    return b;
};

class Library {
public:
    Library() {
        shelves.resize(num_buckets);
    }

    bool IsWord(string s) const {
        cout << "bucket is " << bucket(s) << endl;
        for (Word w : shelves[bucket(s)]) {
            if (s == w.word) {
                return true;
            }
        }
        return false;
    }

    void ComputeStats() {
        assert(counts.empty());
        // resize vector that don't grow in time
        // vector initialized to 0
        counts.resize(18);
        for (Word w : words) {
            int len = w.word.length();
            if (len < 18) {
                counts[len]++;
            }
        }
    }

    void PrintStats() const {
        for (int i = 1; i < counts.size(); i++) {
            cout << counts[i] << " words of " << i << " character(s) " << endl;
        }
    }

    string GetWord(int i) const {
        assert(i >= 0 && i < words.size());
        return words[i].word;
    }

    void ReadFromFile(string filename) {
        ifstream f;
        f.open(filename);
        while (!f.eof()) {
            string line;
            getline(f, line);
            if (!line.empty()) {
                line = ToUpper(line);
                int len = line.length();
                if (line[len - 1] == '\r') {
                    line = line.substr(0, len - 1);
                }
                Word w(line);
                words.push_back(w);
                shelves[bucket(line)].push_back(w);
            }
        }

        f.close();

        cout << "Read " << words.size() << " words from file '" << filename << "'" << endl;
    }

    void DebugBuckets() const {
        for (int i = 0; i < shelves.size(); i++) {
            cout << "[" << i << "] " << shelves[i].size() << endl;
        };
    }

private:
    Words words;
    vector<Words> shelves;
    vector<int> counts;
};
```

In this implementation:
- We've added a `shelves` vector to store words organized by their hash bucket
- During `ReadFromFile`, we add each word to both `words` and its corresponding bucket in `shelves`
- The `IsWord` method checks if a word exists by looking only in its specific bucket
- We've added a `DebugBuckets` method to display the distribution of words across buckets

#### Testing Our Search Functionality

Let's test our search functionality with some examples:

```cpp
int main() {
    Library lib;

    lib.ReadFromFile("top_12000.txt");

    cout << lib.IsWord("DOG") << endl;
    cout << lib.IsWord("GOD") << endl;
    cout << lib.IsWord("ASDFEW") << endl;
    cout << lib.IsWord("THANKS") << endl;
    lib.DebugBuckets();

    return 0;
}
```

This code:
1. Loads our word library from a file
2. Tests if various words exist in the library
3. Displays the distribution of words across buckets

#### Understanding Hash Collisions

With any hash function, there's a possibility of different strings mapping to the same bucket (a "collision"). Our solution handles this by storing all words with the same hash in the same bucket and then linearly searching within that bucket.

The efficiency of our approach depends on:
1. The quality of our hash function
2. The number of buckets
3. The distribution of words across buckets

If too many words map to the same bucket, our search becomes less efficient. The `DebugBuckets` method helps us analyze this distribution.

#### Handling Case Sensitivity

To ensure consistent searching, we convert all words to uppercase. This is common in crossword puzzles, where all letters are usually uppercase.

However, we need to be careful when the user inputs a query:

```cpp
string userQuery = "dog";
bool found = lib.IsWord(ToUpper(userQuery));  // Convert to uppercase before searching
```

#### Enhancing the Search Functionality

Currently, our `IsWord` method only checks if an exact word exists in the library. Let's add a method to find all words matching a pattern:

```cpp
Words Library::FindPatternMatches(const string& pattern) const {
    Words matches;
    
    for (const Word& w : words) {
        if (w.word.length() == pattern.length()) {
            bool isMatch = true;
            
            for (int i = 0; i < pattern.length(); i++) {
                if (pattern[i] != '-' && pattern[i] != w.word[i]) {
                    isMatch = false;
                    break;
                }
            }
            
            if (isMatch) {
                matches.push_back(w);
            }
        }
    }
    
    return matches;
}
```

This implementation searches the entire word list, which is inefficient. In a future chapter, we'll improve this using a more sophisticated pattern hashing technique.

#### Putting It All Together

Here's our complete code for this chapter:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>
#include <fstream>

using namespace std;

string ToUpper(string s) {
    string s2;

    for (char c : s) {
        s2.push_back(toupper(c));
    }
    return s2;
};

struct Word {
    Word(string s) {
        word = s;
    }
    string word;
};
typedef vector<Word> Words;

const int num_buckets = 1001;

int bucket(string s) {
    assert(!s.empty());
    unsigned int i = 0;
    for (char c : s) {
        i = (i * 217) + c;
    }
    int b = i % num_buckets;

    assert(b >= 0 && b < num_buckets);
    return b;
};

class Library {
public:
    Library() {
        shelves.resize(num_buckets);
    }

    bool IsWord(string s) const {
        cout << "bucket is " << bucket(s) << endl;
        for (Word w : shelves[bucket(s)]) {
            if (s == w.word) {
                return true;
            }
        }
        return false;
    }
    
    Words FindPatternMatches(const string& pattern) const {
        Words matches;
        
        for (const Word& w : words) {
            if (w.word.length() == pattern.length()) {
                bool isMatch = true;
                
                for (int i = 0; i < pattern.length(); i++) {
                    if (pattern[i] != '-' && pattern[i] != w.word[i]) {
                        isMatch = false;
                        break;
                    }
                }
                
                if (isMatch) {
                    matches.push_back(w);
                }
            }
        }
        
        return matches;
    }

    void ComputeStats() {
        assert(counts.empty());
        // resize vector that don't grow in time
        // vector initialized to 0
        counts.resize(18);
        for (Word w : words) {
            int len = w.word.length();
            if (len < 18) {
                counts[len]++;
            }
        }
    }

    void PrintStats() const {
        for (int i = 1; i < counts.size(); i++) {
            cout << counts[i] << " words of " << i << " character(s) " << endl;
        }
    }

    string GetWord(int i) const {
        assert(i >= 0 && i < words.size());
        return words[i].word;
    }

    void ReadFromFile(string filename) {
        ifstream f;
        f.open(filename);
        while (!f.eof()) {
            string line;
            getline(f, line);
            if (!line.empty()) {
                line = ToUpper(line);
                int len = line.length();
                if (line[len - 1] == '\r') {
                    line = line.substr(0, len - 1);
                }
                Word w(line);
                words.push_back(w);
                shelves[bucket(line)].push_back(w);
            }
        }

        f.close();

        cout << "Read " << words.size() << " words from file '" << filename << "'" << endl;
    }

    void DebugBuckets() const {
        for (int i = 0; i < shelves.size(); i++) {
            cout << "[" << i << "] " << shelves[i].size() << endl;
        };
    }

private:
    Words words;
    vector<Words> shelves;
    vector<int> counts;
};

struct Grid {
    // ... Grid implementation from previous chapters ...
};

int main() {
    Library lib;

    lib.ReadFromFile("top_12000.txt");

    cout << "Testing exact word matches:" << endl;
    cout << "DOG: " << lib.IsWord("DOG") << endl;
    cout << "GOD: " << lib.IsWord("GOD") << endl;
    cout << "ASDFEW: " << lib.IsWord("ASDFEW") << endl;
    cout << "THANKS: " << lib.IsWord("THANKS") << endl;
    
    cout << "\nTesting pattern matches:" << endl;
    string pattern = "D-G";
    Words matches = lib.FindPatternMatches(pattern);
    cout << "Words matching '" << pattern << "':" << endl;
    for (const Word& w : matches) {
        cout << "  " << w.word << endl;
    }
    
    lib.DebugBuckets();

    return 0;
}
```

#### Understanding the Performance Implications

Our current implementation has different performance characteristics:

1. `IsWord`: Very efficient (O(B) where B is the average bucket size)
2. `FindPatternMatches`: Less efficient (O(N) where N is the total number of words)

This is because `IsWord` uses our hash-based bucketing system, while `FindPatternMatches` still scans the entire word list. In Chapter 10, we'll explore a more efficient approach for pattern matching.

#### Conclusion

In this chapter, we've implemented a basic search functionality for our word library using a hash-based approach. We can now quickly check if a word exists in our library and find words matching a given pattern.

Key concepts covered include:
- Hashing functions and their use for efficient searching
- Organizing data into buckets for quick lookup
- Handling hash collisions
- Pattern matching for crossword puzzles
- Performance considerations for different search operations

In the next chapter, we'll refine our search functionality to make pattern matching more efficient, which is crucial for a fast crossword puzzle solver.

#### Practice Exercises

1. Modify the hash function to improve the distribution of words across buckets.
2. Implement a method to find words of a specific length.
3. Add functionality to find anagrams of a given word.
4. Create a method to find words containing a specific substring.
5. Enhance the `FindPatternMatches` method to return results ordered by word frequency or another metric.

### 10. Search the Library, Fast!
[https://youtu.be/nSW4uXS3gJU ](https://youtu.be/nSW4uXS3gJU )
### 10. Search the Library, Fast!

In this chapter, we'll significantly improve the efficiency of our library search by implementing a more sophisticated data structure. We'll transition from our current bucket-based approach to using a standard C++ container called `unordered_map`, which provides fast lookup capabilities.

#### Limitations of Our Current Approach

In Chapter 9, we implemented a basic hash-based search using custom buckets. While this works, it has several limitations:

1. Our hand-written hash function may not distribute words optimally
2. We're handling collisions by linear search within buckets
3. The code is more complex than necessary
4. Pattern matching still requires scanning the entire word list

#### Introduction to unordered_map

C++ provides a standard container called `unordered_map` that implements a hash table, offering fast key-based lookups:

```cpp
#include <unordered_map>  // Required for unordered_map
```

An `unordered_map` associates keys with values, and uses hashing internally for efficient access:

```cpp
unordered_map<string, int> wordCount;  // Maps words to their count
wordCount["hello"] = 1;                // Insert or update a value
int count = wordCount["hello"];        // Fast lookup
bool exists = (wordCount.find("world") != wordCount.end());  // Check if a key exists
```

#### Refactoring Our Word Structure

Before implementing the new search, let's refine our `Word` structure with a proper constructor:

```cpp
struct Word {
    Word() {}                // Default constructor
    Word(string s) : word(s) {}  // Constructor with initializer list
    string word;
};
```

The line `Word(string s) : word(s) {}` is a constructor with an initializer list, which is more efficient than assigning values inside the constructor body.

#### Using typedef for Type Aliases

To make our code more readable, we'll use typedefs to create aliases for our complex types:

```cpp
typedef vector<Word> Words;
typedef unordered_map<string, Word> WordMap;
```

This allows us to write `Words` instead of `vector<Word>` and `WordMap` instead of `unordered_map<string, Word>`.

#### Implementing Fast Word Search

Now, let's refactor our Library class to use `unordered_map`:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
#include <assert.h>
#include <fstream>

using namespace std;

string ToUpper(string s) {
    string s2;

    for (char c : s) {
        s2.push_back(toupper(c));
    }
    return s2;
};

struct Word {
    Word() {}
    Word(string s) : word(s) {}
    string word;
};
typedef vector<Word> Words;
typedef unordered_map<string, Word> WordMap;

class Library {
public:
    Library() {}
    bool IsWord(string s) const {
        // method 1
        auto it = word_map_.find(s);
        return it != word_map_.end();
        // method 2
        // return word_map_.count(s) > 0;
    }

    void ComputeStats() {
        assert(counts_.empty());
        // resize vector that don't grow in time
        // vector initialized to 0
        counts_.resize(18);
        for (Word w : words_) {
            int len = w.word.length();
            if (len < 18) {
                counts_[len]++;
            }
        }
    }

    void PrintStats() const {
        for (int i = 1; i < counts_.size(); i++) {
            cout << counts_[i] << " words of " << i << " character(s) " << endl;
        }
    }

    string GetWord(int i) const {
        assert(i >= 0 && i < words_.size());
        return words_[i].word;
    }

    void ReadFromFile(string filename) {
        ifstream f;
        f.open(filename);
        while (!f.eof()) {
            string line;
            getline(f, line);
            // cout << line << "   (" << line.length() << ")" << endl;
            if (!line.empty()) {
                line = ToUpper(line);
                int len = line.length();
                if (line[len - 1] == '\r') {
                    line = line.substr(0, len - 1);
                }
                words_.push_back(Word(line));
                word_map_[line] = Word(line);
                // cout << "DEBUG: new bucket_count=" << word_map_.bucket_count() << " load_factor=" << word_map_.load_factor() << endl;
            }
        }

        // cout << words[0].word << endl;
        // cout << words[0].word.length() << endl;
        for (char c : words_[0].word) {
            int x = c;
            // cout << c << " " << x << endl;
        }

        f.close();

        cout << "Read " << words_.size() << " words from file '" << filename << "'" << endl;
    }

    void DebugBuckets() const {
        for (int i = 0; i < word_map_.bucket_count(); i++) {
            cout << "[" << i << "] " << word_map_.bucket_size(i) << endl;
        };
    }

private:
    Words words_;           // master vector of words
    WordMap word_map_;      // maps strings to Word objects
    vector<int> counts_;
};
```

Key changes in this implementation:

1. We now use a `WordMap` (an `unordered_map<string, Word>`) instead of our custom bucket system
2. The `IsWord` method uses the map's `find` function for efficient lookups
3. During `ReadFromFile`, we store each word in both `words_` (a vector) and `word_map_` (a map)
4. The `DebugBuckets` method now shows the distribution of the standard library's hash function

#### Understanding the Implementation

Let's examine some key aspects of this implementation:

1. **Member Variable Naming**: We're now using trailing underscores for private members (e.g., `words_` instead of `words`). This is a common convention to distinguish member variables from local variables or parameters.

2. **Two Ways to Check Existence**: We've shown two equivalent methods to check if a key exists in a map:
   ```cpp
   // Method 1
   auto it = word_map_.find(s);
   return it != word_map_.end();
   
   // Method 2
   return word_map_.count(s) > 0;
   ```
   Both accomplish the same thing, but the first approach is often preferred as it's more explicit.

3. **Auto Keyword**: The use of `auto it = word_map_.find(s)` demonstrates the `auto` keyword, which automatically deduces the variable type from its initializer. In this case, `it` will be of type `unordered_map<string, Word>::const_iterator`.

#### Performance Characteristics

Our new implementation has significant performance advantages:

1. **Fast Exact Word Lookup**: The `IsWord` method now runs in O(1) average time complexity (constant time) instead of O(B) where B was the average bucket size in our previous approach.

2. **Standard Library Optimization**: The `unordered_map` implementation in the C++ standard library is highly optimized and likely performs better than our hand-written hash table.

3. **Automatic Rehashing**: The `unordered_map` automatically resizes and rehashes as needed to maintain performance.

We can observe these characteristics by adding instrumentation:

```cpp
void ReadFromFile(string filename) {
    // ... existing code ...
    
    word_map_[line] = Word(line);
    cout << "DEBUG: bucket_count=" << word_map_.bucket_count() 
         << " load_factor=" << word_map_.load_factor() << endl;
    
    // ... rest of the method ...
}
```

This will show how the map's bucket count and load factor change as we add words.

#### Testing the Performance

Let's test the performance of our new search implementation:

```cpp
int main() {
    Library lib;

    lib.ReadFromFile("top_12000.txt");

    // Measure search time for multiple words
    cout << "\nTesting search performance:\n";
    
    clock_t start = clock();
    for (int i = 0; i < 1000; i++) {
        lib.IsWord("DOG");
        lib.IsWord("CAT");
        lib.IsWord("HOUSE");
        lib.IsWord("XYZZYX");  // A word that doesn't exist
    }
    clock_t end = clock();
    
    double time_taken = double(end - start) / CLOCKS_PER_SEC * 1000.0;  // in milliseconds
    cout << "Time taken for 4000 searches: " << time_taken << " ms\n";
    
    return 0;
}
```

This code measures the time taken to perform 4000 word lookups, which gives us a sense of the search performance.

#### Still Missing: Fast Pattern Matching

While we've significantly improved exact word lookups, we still haven't addressed efficient pattern matching (e.g., finding all words that match "C-T"). This will be covered in a future chapter when we implement pattern hashing.

#### Putting It All Together

Here's our complete implementation for this chapter:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
#include <assert.h>
#include <fstream>
#include <ctime>  // For performance testing

using namespace std;

string ToUpper(string s) {
    string s2;

    for (char c : s) {
        s2.push_back(toupper(c));
    }
    return s2;
};

struct Word {
    Word() {}
    Word(string s) : word(s) {}
    string word;
};
typedef vector<Word> Words;
typedef unordered_map<string, Word> WordMap;

class Library {
public:
    Library() {}
    bool IsWord(string s) const {
        // method 1
        auto it = word_map_.find(s);
        return it != word_map_.end();
        // method 2
        // return word_map_.count(s) > 0;
    }

    void ComputeStats() {
        assert(counts_.empty());
        // resize vector that don't grow in time
        // vector initialized to 0
        counts_.resize(18);
        for (Word w : words_) {
            int len = w.word.length();
            if (len < 18) {
                counts_[len]++;
            }
        }
    }

    void PrintStats() const {
        for (int i = 1; i < counts_.size(); i++) {
            cout << counts_[i] << " words of " << i << " character(s) " << endl;
        }
    }

    string GetWord(int i) const {
        assert(i >= 0 && i < words_.size());
        return words_[i].word;
    }

    void ReadFromFile(string filename) {
        ifstream f;
        f.open(filename);
        while (!f.eof()) {
            string line;
            getline(f, line);
            // cout << line << "   (" << line.length() << ")" << endl;
            if (!line.empty()) {
                line = ToUpper(line);
                int len = line.length();
                if (line[len - 1] == '\r') {
                    line = line.substr(0, len - 1);
                }
                words_.push_back(Word(line));
                word_map_[line] = Word(line);
                // cout << "DEBUG: new bucket_count=" << word_map_.bucket_count() << " load_factor=" << word_map_.load_factor() << endl;
            }
        }

        f.close();

        cout << "Read " << words_.size() << " words from file '" << filename << "'" << endl;
    }

    void DebugBuckets() const {
        for (int i = 0; i < word_map_.bucket_count(); i++) {
            cout << "[" << i << "] " << word_map_.bucket_size(i) << endl;
        };
    }

    // Performance testing method
    void BenchmarkSearch() const {
        const int iterations = 1000;
        const vector<string> testWords = {"DOG", "CAT", "HOUSE", "XYZZYX"};
        
        clock_t start = clock();
        
        for (int i = 0; i < iterations; i++) {
            for (const string& word : testWords) {
                IsWord(word);
            }
        }
        
        clock_t end = clock();
        double time_taken = double(end - start) / CLOCKS_PER_SEC * 1000.0;  // in ms
        
        cout << "Time taken for " << iterations * testWords.size() << " searches: " 
             << time_taken << " ms" << endl;
        cout << "Average time per search: " << time_taken / (iterations * testWords.size()) 
             << " ms" << endl;
    }

private:
    Words words_;           // master vector of words
    WordMap word_map_;      // maps strings to Word objects
    vector<int> counts_;
};

struct Grid {
    // ... Grid implementation from previous chapters ...
};

int main() {
    Library lib;

    lib.ReadFromFile("top_12000.txt");

    cout << lib.IsWord("DOG") << endl;
    cout << lib.IsWord("GOD") << endl;
    cout << lib.IsWord("ASDFEW") << endl;
    cout << lib.IsWord("THANKS") << endl;
    
    // Performance test
    lib.BenchmarkSearch();
    
    // Display some information about the hash distribution
    cout << "\nHash distribution information:\n";
    // We'll just display a few buckets for brevity
    for (int i = 0; i < 10; i++) {
        cout << "Bucket " << i << ": ";
        // Display bucket details
    }
    
    return 0;
}
```

#### Conclusion

In this chapter, we've significantly improved the efficiency of our word search by:

1. **Using the Standard Library**: Replacing our custom hash table with the highly optimized `unordered_map` from the C++ standard library.

2. **Simplifying Our Code**: Reducing complexity while improving performance.

3. **Adding Performance Benchmarking**: Measuring and testing our search speed.

4. **Learning Advanced C++ Features**: Exploring `auto`, typedefs, and initializer lists.

These improvements will make our crossword puzzle solver more efficient, especially when checking if specific words exist. In future chapters, we'll extend this approach to handle pattern matching, which is crucial for finding valid words to fill crossword grid cells.

#### Practice Exercises

1. Add a method to find all words of a specific length.
2. Implement a case-insensitive word search.
3. Create a function to find words that are anagrams of a given word.
4. Add functionality to load words from multiple files, keeping track of the source file for each word.
5. Implement a method to save the most frequently searched words to improve performance further.

### 11. How Memory Works
[https://youtu.be/-o8DVeVvA4s ](https://youtu.be/-o8DVeVvA4s )
### 11. How Memory Works

In this chapter, we'll take a step back from our crossword solver to explore a fundamental concept in C++ programming: memory management. Understanding how memory works is crucial for building efficient and robust applications, especially when dealing with complex data structures like those in our crossword puzzle solver.

#### Why Memory Management Matters

As we continue to develop our crossword solver, we'll need to:
- Store and manipulate large lists of words
- Create and modify grid objects
- Share data between different parts of our program
- Ensure our program doesn't leak memory

Proper memory management helps us achieve these goals while avoiding common pitfalls like memory leaks, dangling pointers, and inefficient data copying.

#### Stack vs. Heap Memory

C++ uses two main regions of memory:

1. **Stack**: For local variables with automatic lifetime
   - Fast allocation and deallocation
   - Limited size (typically a few MB)
   - Memory is automatically managed
   - Variables are destroyed when they go out of scope

2. **Heap**: For dynamically allocated memory
   - Much larger size (limited by system memory)
   - Manual memory management (allocation and deallocation)
   - Variables persist until explicitly freed
   - Slower than stack allocation

```cpp
void ExampleFunction() {
    // Stack allocation
    int stackVar = 42;           // Allocated on the stack
    char stackArray[100];        // Also on the stack
    
    // Heap allocation
    int* heapVar = new int(42);  // Allocated on the heap
    char* heapArray = new char[100]; // Also on the heap
    
    // Must free heap memory to avoid leaks
    delete heapVar;
    delete[] heapArray;
} // stackVar and stackArray are automatically freed here
```

#### Pointers and References

C++ provides two main ways to work with memory addresses:

1. **Pointers** (`void*`, `int*`, etc.)
   - Store the memory address of an object
   - Can be reassigned to point to different objects
   - Can be null (not pointing to anything)
   - Require dereferencing (`*p`) to access the value

2. **References** (`int&`, etc.)
   - Alias for an existing object
   - Cannot be reassigned to refer to a different object
   - Cannot be null
   - No dereferencing syntax needed

```cpp
#include <iostream>
using namespace std;

int main() {
    char c = 'A';
    int i = 10;
    
    // Pointers
    void* p0 = &c;  // Address of c
    void* p1 = &i;  // Address of i
    
    cout << "Address of c: " << p0 << endl;
    cout << "Address of i: " << p1 << endl;
    cout << "Size of char: " << sizeof(c) << " bytes" << endl;
    cout << "Size of int: " << sizeof(i) << " bytes" << endl;
    
    // Using typed pointers
    char* cp = &c;
    int* ip = &i;
    
    cout << "Value of c: " << c << endl;
    *cp = 'B';  // Modify through pointer
    cout << "New value of c: " << c << endl;
    
    cout << "Value of i: " << i << endl;
    *ip = 2000;  // Modify through pointer
    cout << "New value of i: " << i << endl;
    
    return 0;
}
```

#### Passing Parameters to Functions

There are three main ways to pass parameters to functions in C++:

1. **Pass by Value**
   - A copy of the argument is made
   - Changes to the parameter don't affect the original argument
   - Example: `void Foo(int x) {x += 1;}`

2. **Pass by Reference**
   - The parameter becomes an alias for the argument
   - Changes to the parameter affect the original argument
   - Example: `void Foo(int& x) {x += 1;}`

3. **Pass by Pointer**
   - A pointer to the argument is passed
   - Changes can be made through dereferencing
   - Example: `void Foo(int* x) {*x += 3;}`

Let's see these in action:

```cpp
#include <iostream>
using namespace std;

void Foo(int x, int& y, int* z) {
    cout << "FOO x = " << x << endl;
    cout << "FOO y = " << y << endl;
    cout << "FOO z = " << *z << endl;
    
    x += 1;   // Modifies the copy
    y += 2;   // Modifies the original through reference
    *z += 3;  // Modifies the original through pointer
    
    cout << "MODIFIED x = " << x << endl;
    cout << "MODIFIED y = " << y << endl;
    cout << "MODIFIED z = " << *z << endl;
}

int main() {
    int i = 10;
    int j = 20;
    int k = 30;
    
    cout << "ORIGINAL i = " << i << endl;
    cout << "ORIGINAL j = " << j << endl;
    cout << "ORIGINAL k = " << k << endl;
    
    Foo(i, j, &k);
    
    cout << "AFTER i = " << i << endl;  // Unchanged (pass by value)
    cout << "AFTER j = " << j << endl;  // Changed (pass by reference)
    cout << "AFTER k = " << k << endl;  // Changed (pass by pointer)
    
    return 0;
}
```

#### Dynamic Memory Allocation

When we need memory that persists beyond the scope of a function or need to allocate memory whose size is determined at runtime, we use dynamic memory allocation:

```cpp
#include <iostream>
using namespace std;

int main() {
    // Allocate a single integer
    int* p = new int(8);
    cout << *p << endl;  // 8
    
    // Use the allocated memory
    int x = *p;
    cout << x << endl;  // 8
    
    // Free the memory when done
    delete p;
    
    // Allocate an array of integers
    int size = 5;
    int* arr = new int[size];
    
    // Initialize the array
    for (int i = 0; i < size; i++) {
        arr[i] = i * 10;
    }
    
    // Use the array
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";  // 0 10 20 30 40
    }
    cout << endl;
    
    // Free the array
    delete[] arr;
    
    return 0;
}
```

Key points about dynamic allocation:
- Use `new` to allocate memory
- Use `delete` to free memory for single objects
- Use `delete[]` to free memory for arrays
- Failing to delete allocated memory causes memory leaks

#### Smart Pointers

C++ provides smart pointers that help manage dynamically allocated memory and prevent memory leaks:

1. **unique_ptr**
   - Owns and manages a single object
   - Automatically deletes the object when the unique_ptr goes out of scope
   - Cannot be copied, only moved

2. **shared_ptr**
   - Shares ownership of an object among multiple pointers
   - Uses reference counting to determine when to delete the object
   - The object is deleted when the last shared_ptr referencing it is destroyed

3. **weak_ptr**
   - Holds a non-owning reference to an object managed by shared_ptr
   - Does not affect reference count
   - Used to break circular references

```cpp
#include <iostream>
#include <memory>  // Required for smart pointers
using namespace std;

int main() {
    // Using unique_ptr
    unique_ptr<int> up(new int(8));
    cout << *up << endl;  // 8
    
    // Memory is automatically freed when up goes out of scope
    
    // Using shared_ptr
    shared_ptr<int> sp1 = make_shared<int>(42);
    cout << *sp1 << endl;  // 42
    
    {
        shared_ptr<int> sp2 = sp1;  // Both point to the same object
        cout << "sp1 use count: " << sp1.use_count() << endl;  // 2
        cout << *sp2 << endl;  // 42
        
        *sp2 = 100;  // Modifies the shared object
    }  // sp2 is destroyed here, but the object survives
    
    cout << "sp1 use count: " << sp1.use_count() << endl;  // 1
    cout << *sp1 << endl;  // 100
    
    return 0;
}  // sp1 is destroyed here, and the object is deleted
```

In modern C++, smart pointers are preferred over raw pointers for managing dynamic memory.

#### Memory Layout of Objects

Understanding how objects are laid out in memory is important for efficient programming:

```cpp
#include <iostream>
using namespace std;

struct Point {
    int x;
    int y;
};

class String {
public:
    String(const char* s) {
        size_ = strlen(s);
        data_ = new char[size_ + 1];
        strcpy(data_, s);
    }
    
    ~String() {
        delete[] data_;
    }
    
    int size() const { return size_; }
    const char* data() const { return data_; }
    
private:
    int size_;
    char* data_;  // Points to dynamically allocated memory
};

int main() {
    // Simple object on the stack
    Point p = {10, 20};
    cout << "Size of Point: " << sizeof(p) << " bytes" << endl;
    cout << "Address of p: " << &p << endl;
    cout << "Address of p.x: " << &p.x << endl;
    cout << "Address of p.y: " << &p.y << endl;
    
    // Object with dynamic memory
    String s("Hello");
    cout << "Size of String: " << sizeof(s) << " bytes" << endl;
    cout << "String content size: " << s.size() << " bytes" << endl;
    cout << "Address of s: " << &s << endl;
    cout << "Address of string data: " << static_cast<const void*>(s.data()) << endl;
    
    return 0;
}
```

Key observations:
- Simple objects like `Point` have a size that's the sum of their member sizes (plus possible padding)
- Objects that manage dynamic memory like `String` have a fixed size for the object itself, but can control variable amounts of heap memory

#### Applying Memory Concepts to Our Crossword Solver

Now, let's consider how these memory concepts apply to our crossword solver:

1. **Word Storage**: We're using a vector of Word objects and an unordered_map for fast lookup. These containers manage memory for us, but understanding their memory behavior helps us use them efficiently.

2. **Grid Representation**: Our Grid object currently stores the grid as a vector of strings. We might consider alternative memory layouts for performance optimization.

3. **Parameter Passing**: When passing large objects like our Grid or Library, we should consider passing by reference or const reference to avoid unnecessary copying.

4. **Smart Pointers**: In future chapters, we might use smart pointers to manage complex relationships between objects in our solver.

Let's rewrite a portion of our Library class with these considerations in mind:

```cpp
class Library {
public:
    // Pass large strings by const reference
    void AddWord(const string& word) {
        Word w(word);
        words_.push_back(w);
        word_map_[word] = w;
    }
    
    // Return by const reference to avoid copying
    const vector<Word>& GetAllWords() const {
        return words_;
    }
    
    // Use const for methods that don't modify the object
    bool IsWord(const string& s) const {
        auto it = word_map_.find(s);
        return it != word_map_.end();
    }
    
    // ...rest of the class...
};
```

#### Conclusion

In this chapter, we've explored fundamental memory concepts in C++:

1. **Stack vs. Heap Memory**: Understanding the two main memory regions and when to use each.

2. **Pointers and References**: Learning different ways to work with memory addresses.

3. **Parameter Passing**: Exploring pass by value, reference, and pointer.

4. **Dynamic Memory Allocation**: Using `new` and `delete` to manage heap memory.

5. **Smart Pointers**: Leveraging modern C++ features for safer memory management.

6. **Memory Layout**: Understanding how objects are organized in memory.

These concepts are crucial for developing efficient and robust C++ programs, including our crossword puzzle solver. In the following chapters, we'll apply these concepts as we continue to enhance our solver with more advanced features.

#### Practice Exercises

1. Modify the Word class to use dynamic memory allocation for storing the word text.
2. Implement a deep copy constructor and assignment operator for the Word class.
3. Create a function that takes a Grid object by reference and modifies it.
4. Implement a function that efficiently swaps two large strings without copying their contents.
5. Refactor part of the Library class to use smart pointers for managing Word objects.

### 12. Pattern Hash
[https://youtu.be/PJqoQMKlKjQ](https://youtu.be/PJqoQMKlKjQ)
### 12. Pattern Hash

In this chapter, we'll implement a powerful pattern matching system for our crossword solver. This "pattern hash" will allow us to efficiently find words that match specific patterns of known and unknown letters, which is essential for filling in the crossword grid.

#### The Pattern Matching Challenge

In our crossword solver, we frequently need to answer questions like:
- What 3-letter words start with 'D'? (pattern: "D--")
- What 5-letter words have 'A' as the third letter? (pattern: "--A--")
- What words match "C-T"? (words with 'C' first and 'T' last)

While we could scan through our entire word list each time, this would be inefficient. Instead, we'll build a specialized data structure to make these lookups nearly instantaneous.

#### Rethinking Our Word Structure

First, let's enhance our Word structure to make it more robust and efficient:

```cpp
struct Word {
  Word() {}
  Word(string s) : word(s) {}
  int len() const { return word.length(); }
  string word;
};
```

We've added a `len()` method that returns the word length. Using a method instead of directly accessing `word.length()` provides a consistent interface and makes future changes easier.

#### Memory Management with Pointers

In our enhanced implementation, we'll use pointers to Word objects. This approach has several advantages:
- We can store the same Word in multiple lookup structures without duplication
- We have more control over object lifetimes
- We can modify a Word in one place and have the changes visible everywhere

However, we must be careful to properly manage memory to avoid leaks. We'll use a proper destructor in our Library class:

```cpp
typedef vector<Word*> Words;
typedef unordered_map<string, Words> WordMap;

class Library {
public:
  Library() {}
  ~Library() {
    for (Word* w : words_) {
      delete w;
    }
  }
  
  // ... rest of the class
};
```

This destructor ensures that all Word objects are properly deleted when the Library is destroyed.

#### The Pattern Hash Concept

Our pattern hash will work as follows:
1. For each word in our library, we'll generate all possible patterns that could match it
2. We'll store the word in a map, with each pattern as a key
3. When we need to find words matching a pattern, we'll simply look up that pattern

For example, for the word "DOG", we'll generate these patterns:
- "DOG" (exact match)
- "DO-" (first two letters match)
- "D-G" (first and last letters match)
- "-OG" (last two letters match)
- "D--" (only first letter matches)
- "-O-" (only middle letter matches)
- "--G" (only last letter matches)
- "---" (any 3-letter word)

#### Implementing the Pattern Hash

Let's implement the pattern hash functionality in our Library class:

```cpp
void CreatePatternHash(Word* w) {
  int len = w->len();
  int num_patterns = 1 << len;  // 2^len possible patterns
  
  for (int i = 0; i < num_patterns; i++) {
    string temp = w->word;
    for (int j = 0; j < len; j++) {
      if ((i >> j) & 1) {
        temp[j] = '-';  // Replace with wildcard
      }
    }
    word_map_[temp].push_back(w);
  }
}
```

This function:
1. Takes a Word pointer as input
2. Calculates the number of possible patterns (2^len)
3. For each pattern, creates a new string with some characters replaced by '-'
4. Adds the Word to the appropriate entry in word_map_

The bit manipulation `(i >> j) & 1` checks if the jth bit of i is set. If it is, we replace the character with a wildcard.

#### The BitPattern Approach

Let's break down the bit pattern approach with an example for the word "DOG":

- Length of "DOG" is 3, so we have 2^3 = 8 possible patterns
- For each i from 0 to 7:
  - i = 0 (binary 000): No bits set, no replacements -> "DOG"
  - i = 1 (binary 001): Bit 0 set, replace char 0 -> "-OG"
  - i = 2 (binary 010): Bit 1 set, replace char 1 -> "D-G"
  - i = 3 (binary 011): Bits 0,1 set, replace chars 0,1 -> "--G"
  - i = 4 (binary 100): Bit 2 set, replace char 2 -> "DO-"
  - i = 5 (binary 101): Bits 0,2 set, replace chars 0,2 -> "-O-"
  - i = 6 (binary 110): Bits 1,2 set, replace chars 1,2 -> "D--"
  - i = 7 (binary 111): All bits set, replace all chars -> "---"

This approach generates all possible patterns systematically.

#### Optimizing for Longer Words

The number of patterns grows exponentially with word length. For a 10-letter word, we'd generate 2^10 = 1,024 patterns, which is manageable. But for longer words, this could become excessive.

Let's add a length limit:

```cpp
void CreatePatternHash(Word* w) {
  int len = w->len();
  if (len > 7) return;  // Skip words longer than 7 characters
  
  int num_patterns = 1 << len;
  // ... rest of the function
}
```

This prevents pattern explosion for very long words. In crossword puzzles, most words are relatively short anyway.

#### Updating the ReadFromFile Method

Now let's update our `ReadFromFile` method to create pattern hashes for each word:

```cpp
void ReadFromFile(string filename) {
  ifstream f;
  f.open(filename);
  while (f.is_open() && !f.eof()) {
    string line;
    getline(f, line);
    
    if (!line.empty()) {
      line = ToUpper(line);
      int len = line.length();
      if (line[len - 1] == '\r') {
        line = line.substr(0, len - 1);
      }
      Word* w = new Word(line);
      words_.push_back(w);
      CreatePatternHash(w);
    }
  }
  
  f.close();
  
  cout << "Read " << words_.size() << " words from file '" << filename << "'"
       << endl;
}
```

The key change is that we now call `CreatePatternHash(w)` for each word.

#### Finding Words That Match a Pattern

With our pattern hash in place, finding words that match a pattern becomes trivial:

```cpp
void FindWord(const string& s) const {
  auto it = word_map_.find(s);
  if (it != word_map_.end()) {
    for (const Word* w : it->second) {
      cout << " " << w->word;
    }
    cout << endl;
  }
}
```

This function:
1. Looks up the pattern in our word_map_
2. If found, prints all words that match the pattern

#### Understanding const Correctness

In our implementation, we use the `const` keyword extensively. This is important for:
- Preventing unintended modifications
- Enabling compiler optimizations
- Clearly communicating intent

For example:

```cpp
void FindWord(const string& s) const {
  // ...
}
```

This method declaration indicates:
- The input string `s` won't be modified (const reference)
- The method won't modify the Library object (trailing const)

#### Memory Safety Considerations

When working with pointers, we must be careful to avoid memory leaks and dangling pointers. Our implementation:
1. Creates Word objects with `new` in ReadFromFile
2. Stores pointers to these objects
3. Deletes them in the Library destructor

This ensures that all memory is properly managed.

#### Putting It All Together

Here's our complete implementation of the pattern hash:

```cpp
#include <assert.h>
#include <fstream>
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

string ToUpper(string s) {
  string s2;

  for (char c : s) {
    s2.push_back(toupper(c));
  }
  return s2;
};

// ----------------------------------------------------------------
//-Word
struct Word {
  Word() {}
  Word(string s) : word(s) {}
  int len() const { return word.length(); }
  string word;
};
typedef vector<Word*> Words;
typedef unordered_map<string, Words> WordMap;

// ----------------------------------------------------------------
//-Library
class Library {
 public:
  Library() {}
  ~Library() {
    for (Word* w : words_) {
      delete w;
    }
  }
  void FindWord(const string& s) const {
    auto it = word_map_.find(s);
    if (it != word_map_.end()) {
      for (const Word* w : it->second) {
        cout << " " << w->word;
      }
      cout << endl;
    }
  }

  bool IsWord(string s) const {
    // method 1
    auto it = word_map_.find(s);
    return it != word_map_.end();
    // method 2
    // return word_map_.count(s) > 0;
  }

  void ComputeStats() {
    assert(counts_.empty());
    // resize vector that don't grow in time
    // vector initialized to 0
    counts_.resize(18);
    for (const Word* w : words_) {
      int len = w->word.length();
      if (len < 18) {
        counts_[len]++;
      }
    }
  }

  void PrintStats() const {
    for (int i = 1; i < counts_.size(); i++) {
      cout << counts_[i] << " words of " << i << " character(s) " << endl;
    }
  }

  string GetWord(int i) const {
    assert(i >= 0 && i < words_.size());
    return words_[i]->word;
  }

  void CreatePatternHash(Word* w) {
    int len = w->len();
    if (len > 7) return;
    int num_patterns = 1 << len;  // pow(2, len)
    // cout << "PATTERN HASH on " << w->word << endl;
    for (int i = 0; i < num_patterns; i++) {
      // cout << "  " << i << endl;
      string temp = w->word;
      for (int j = 0; j < len; j++) {
        if ((i >> j) & 1) {
          temp[j] = '-';
        }
      }
      // cout << "  " << temp << endl;
      word_map_[temp].push_back(w);
    }
  }

  void ReadFromFile(string filename) {
    ifstream f;
    f.open(filename);
    while (f.is_open() && !f.eof()) {
      string line;
      getline(f, line);
      // cout << line << "   (" << line.length() << ")" << endl;
      if (!line.empty()) {
        line = ToUpper(line);
        int len = line.length();
        if (line[len - 1] == '\r') {
          line = line.substr(0, len - 1);
        }
        Word* w = new Word(line);
        words_.push_back(w);
        CreatePatternHash(w);
      }
    }

    // cout << words[0].word << endl;
    // cout << words[0].word.length() << endl;
    // for (char c : words_[0].word) {
    //   int x = c;
    //   // cout << c << " " << x << endl;
    // }

    f.close();

    cout << "Read " << words_.size() << " words from file '" << filename << "'"
         << endl;
  }

  void DebugBuckets() const {
    for (int i = 0; i < word_map_.bucket_count(); i++) {
      cout << "[" << i << "] " << word_map_.bucket_size(i) << endl;
    };
  }

 private:
  Words words_;       // master vector of words
  WordMap word_map_;  // pattern hash ("D--" returns vector of all <DAD, DUD,
                      // ...>)
  vector<int> counts_;
};

// ----------------------------------------------------------------
//-Grid
struct Grid {
  // ... Grid implementation from previous chapters ...
};

int main() {
  Library lib;

  lib.ReadFromFile("top_12000.txt");

  lib.FindWord("D--");

  // Grid grid("MY GRID");

  // grid.LoadFromFile("test.txt");
  // grid.Check();
  // grid.Print();
};
```

#### Testing the Pattern Hash

Let's test our pattern hash with various patterns:

```cpp
int main() {
  Library lib;
  lib.ReadFromFile("top_12000.txt");

  cout << "Words matching 'D--':" << endl;
  lib.FindWord("D--");

  cout << "Words matching 'C-T':" << endl;
  lib.FindWord("C-T");

  cout << "Words matching '--G':" << endl;
  lib.FindWord("--G");

  cout << "Words matching '----S':" << endl;
  lib.FindWord("----S");

  return 0;
}
```

This will display all words matching each pattern, demonstrating the power of our pattern hash.

#### Performance Considerations

Our pattern hash significantly improves performance for pattern matching:
- Without pattern hash: O(n) time to scan all words
- With pattern hash: O(1) time to look up a pattern

The tradeoff is increased memory usage, as we store multiple references to each word. For a typical dictionary, this is a worthwhile tradeoff.

#### Conclusion

In this chapter, we've implemented a powerful pattern hash that allows our crossword solver to efficiently find words matching specific patterns. This is a crucial component for our solver, as it enables us to quickly identify candidate words for each position in the grid.

Key concepts covered include:
- Creating a flexible pattern matching system
- Using bit manipulation to generate patterns
- Managing memory with pointers
- Ensuring const correctness
- Optimizing for performance

In the next chapter, we'll build on this foundation by developing the "Points-and-Spans" system, which will help us represent and navigate the crossword grid.

#### Practice Exercises

1. Modify the pattern hash to handle longer words efficiently.
2. Add functionality to find words that match a pattern with specific constraints (e.g., words where certain positions must be different letters).
3. Implement a method to find words that are anagrams of a given pattern.
4. Create a function that returns the number of words matching a pattern without retrieving the actual words.
5. Extend the pattern hash to support character classes (e.g., vowels, consonants).

### 13. Points and Spans
[https://youtu.be/7uS0hrpERcY](https://youtu.be/7uS0hrpERcY)
### 13. Points and Spans

In this chapter, we'll develop two fundamental structures for our crossword puzzle solver: Points and Spans. These structures will help us represent and navigate the grid, identify word positions, and manage the relationships between intersecting words.

#### The Need for Grid Navigation

Before we dive into implementation, let's understand why we need these structures:

1. We need to represent positions in the grid (rows and columns)
2. We need to identify spans where words can be placed (horizontally and vertically)
3. We need to track the intersections between horizontal and vertical words
4. We need a way to navigate the grid efficiently

#### Implementing the Point Structure

A Point represents a specific location in our grid, defined by a row and column. Let's implement it:

```cpp
#include <assert.h>
#include <fstream>
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

// ----------------------------------------------------------------
//-Point
struct Point {
  Point() {}
  Point(int r, int c) : row(r), col(c) {}

  friend ostream& operator<<(ostream& os, const Point& p);
  int row = 0;
  int col = 0;
};

ostream& operator<<(ostream& os, const Point& p) {
  os << "(" << p.row << "," << p.col << ")";
  return os;
};
```

This implementation includes:
- A default constructor and a parameterized constructor
- Member variables for row and column (initialized to 0)
- An overloaded `<<` operator to make Points easy to print

The `friend` declaration allows the `operator<<` function to access private members of the Point class.

#### Implementing the Span Structure

A Span represents a sequence of cells in the grid where a word can be placed. It's defined by:
- A starting point
- A length
- A direction (horizontal or vertical)

Let's implement it:

```cpp
// ----------------------------------------------------------------
//-Span
struct Span {
  Span(Point p, int l, bool v) : point(p), len(l), vert(v) {}

  friend ostream& operator<<(ostream& os, const Span& s);
  Point point;
  int len;
  bool vert;
};

ostream& operator<<(ostream& os, const Span& s) {
  os << "[" << s.point << "len=" << s.len << " vert=" << s.vert << "]";
  return os;
};
```

Similar to Point, we've included:
- A constructor to initialize all members
- An overloaded `<<` operator for easy printing

#### Testing Points and Spans

Let's create a simple test to ensure our structures work as expected:

```cpp
int main() {
  Point p1;
  Point p2(2, 1);

  cout << "point1 is " << p1 << endl;
  cout << "point2 is " << p2 << endl;

  Span s1(p1, 3, true);
  Span s2(p2, 5, false);

  cout << "span1 is " << s1 << endl;
  cout << "span2 is " << s2 << endl;

  return 0;
}
```

This should output:
```
point1 is (0,0)
point2 is (2,1)
span1 is [(0,0)len=3 vert=1]
span2 is [(2,1)len=5 vert=0]
```

#### Integrating with the Grid

Now that we have our Point and Span structures, let's enhance our Grid class to use them. First, we'll add methods to work with Points:

```cpp
struct Grid {
  // ... existing code ...

  // Returns character value of the box at point 'p'.
  char box(const Point& p) const {
    assert(in_bounds(p));
    return lines[p.row][p.col];
  }

  // Returns true if the point p is a '.' "block" in the grid.
  // 'p' must be in bounds.
  bool is_block(const Point& p) const { return box(p) == '.'; }

  bool is_blank(const Point& p) const { return box(p) == '-'; }

  bool is_letter(const Point& p) const {
    char c = box(p);
    return c >= 'A' && c <= 'Z';
  }

  bool in_bounds(const Point& p) const {
    return (p.row >= 0 && p.row < rows() && p.col >= 0 && p.col < cols());
  }
};
```

These methods make it easy to query the grid at specific points and check cell types.

#### Grid Traversal

We need a way to methodically traverse the grid. Let's add a method that advances a point to the next position:

```cpp
struct Grid {
  // ... existing code ...

  // Next increments the point across the grid, one box at a time.
  // Returns true if point is still in bounds
  bool Next(Point& p, bool vert) {
    if (vert) {
      p.row++;
      if (p.row >= rows()) {
        p.row = 0;
        p.col++;
      }
    } else {
      p.col++;
      if (p.col >= cols()) {
        p.col = 0;
        p.row++;
      }
    }
    return in_bounds(p);
  }
};
```

This method advances the point either vertically (down then right) or horizontally (right then down), and returns whether the point is still within the grid bounds.

#### Finding Spans in the Grid

Now, let's add methods to identify all spans in the grid where words can be placed:

```cpp
typedef vector<Span> Spans;

struct Grid {
  // ... existing code ...

  void FillSpans(bool vert) {
    Point p;
    while (in_bounds(p)) {
      while (in_bounds(p) && is_block((p))) {
        Next(p, vert);
      }
      if (!in_bounds(p)) return;
      Point startp = p;
      // cout << "SPAN START: " << p << endl;

      int len = 0;
      do {
        Next(p, vert);
        len++;
      } while (in_bounds(p) && !is_block(p));
      // cout << "END OF SPAN!!! len = " << len << endl;
      spans.push_back(Span(startp, len, vert));
    }
  }

  // Add to 'spans' vector with all viable spans in the grid
  void FillSpans() {
    assert(spans.empty());
    FillSpans(false);  // horiz
    FillSpans(true);   // vert
  }

  void PrintSpans() const {
    cout << "Spans:" << endl;
    for (const Span& s : spans) {
      cout << "  " << s << endl;
    }
  }

  // ... existing code ...
  Spans spans;  // All viable spans in the grid
};
```

The `FillSpans` method works by:
1. Starting at the top-left of the grid
2. Skipping any blocks
3. When it finds a non-block cell, recording it as the start of a span
4. Continuing until it hits another block or the edge of the grid
5. Creating a Span and adding it to the spans vector
6. Repeating for both horizontal and vertical directions

#### Putting It All Together

Let's combine all these elements into a complete implementation:

```cpp
#include <assert.h>
#include <fstream>
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

string ToUpper(string s) {
  string s2;

  for (char c : s) {
    s2.push_back(toupper(c));
  }
  return s2;
};

// ----------------------------------------------------------------
//-Point
struct Point {
  Point() {}
  Point(int r, int c) : row(r), col(c) {}

  friend ostream& operator<<(ostream& os, const Point& p);
  int row = 0;
  int col = 0;
};

ostream& operator<<(ostream& os, const Point& p) {
  os << "(" << p.row << "," << p.col << ")";
  return os;
};

// ----------------------------------------------------------------
//-Span
struct Span {
  Span(Point p, int l, bool v) : point(p), len(l), vert(v) {}

  friend ostream& operator<<(ostream& os, const Span& s);
  Point point;
  int len;
  bool vert;
};
typedef vector<Span> Spans;

ostream& operator<<(ostream& os, const Span& s) {
  os << "[" << s.point << "len=" << s.len << " vert=" << s.vert << "]";
  return os;
};

// ----------------------------------------------------------------
//-Word
struct Word {
  Word() {}
  Word(string s) : word(s) {}
  int len() const { return word.length(); }
  string word;
};
typedef vector<Word*> Words;
typedef unordered_map<string, Words> WordMap;

// ----------------------------------------------------------------
//-Library
class Library {
 public:
  // ... Library implementation from previous chapters ...
};

// ----------------------------------------------------------------
//-Grid
struct Grid {
  Grid(string n) { name = n; }

  int rows() const { return lines.size(); }

  int cols() const {
    if (lines.empty()) {
      return 0;
    } else {
      return lines[0].size();
    }
  }

  // Returns character value of the box at point 'p'.
  char box(const Point& p) const {
    assert(in_bounds(p));
    return lines[p.row][p.col];
  }

  // Returns true if the point p is a '.' "block" in the grid.
  // 'p' must be in bounds.
  bool is_block(const Point& p) const { return box(p) == '.'; }

  bool is_blank(const Point& p) const { return box(p) == '-'; }

  bool is_letter(const Point& p) const {
    char c = box(p);
    return c >= 'A' && c <= 'Z';
  }

  bool in_bounds(const Point& p) const {
    return (p.row >= 0 && p.row < rows() && p.col >= 0 && p.col < cols());
  }

  // Next increments the point across the grid, one box at a time.
  // Returns true if point is still in bounds
  bool Next(Point& p, bool vert) {
    if (vert) {
      p.row++;
      if (p.row >= rows()) {
        p.row = 0;
        p.col++;
      }
    } else {
      p.col++;
      if (p.col >= cols()) {
        p.col = 0;
        p.row++;
      }
    }
    return in_bounds(p);
  }

  void FillSpans(bool vert) {
    Point p;
    while (in_bounds(p)) {
      while (in_bounds(p) && is_block((p))) {
        Next(p, vert);
      }
      if (!in_bounds(p)) return;
      Point startp = p;
      // cout << "SPAN START: " << p << endl;

      int len = 0;
      do {
        Next(p, vert);
        len++;
      } while (in_bounds(p) && !is_block(p));
      // cout << "END OF SPAN!!! len = " << len << endl;
      spans.push_back(Span(startp, len, vert));
    }
  }

  // Add to 'spans' vector with all viable spans in the grid
  void FillSpans() {
    assert(spans.empty());
    FillSpans(false);  // horiz
    FillSpans(true);   // vert
  }

  void LoadFromFile(string filename) {
    ifstream f;
    f.open(filename);
    while (f.is_open() && !f.eof()) {
      string line;
      getline(f, line);
      // cout << line << "   (" << line.length() << ")" << endl;
      if (!line.empty() && line[0] != '#') {
        lines.push_back(line);
      }
    }
    f.close();

    // lines.pop_back();
  }

  int Check() const {
    for (string s : lines) {
      assert(s.size() == cols());
    }
    return 0;
  }

  void Print() const {
    cout << "Grid : " << name << " (rows=" << rows() << ", cols=" << cols()
         << endl;
    for (string s : lines) {
      cout << s << endl;
    }
  }

  void PrintSpans() const {
    cout << "Spans:" << endl;
    for (const Span& s : spans) {
      cout << "  " << s << endl;
    }
  }

  string name;
  vector<string> lines;
  Spans spans;
};

int main() {
  Library lib;
  lib.ReadFromFile("top_12000.txt");

  Grid grid("MY GRID");
  grid.LoadFromFile("test.txt");
  grid.Check();
  grid.Print();
  grid.FillSpans();
  grid.PrintSpans();

  return 0;
}
```

#### Testing on a Real Grid

Let's test our implementation with a real grid file:

```
# test.txt
DOG....
---....
----...
-------
...----
....---
...CATS
```

When we run our program with this grid, it should:
1. Load the grid from the file
2. Identify all spans (both horizontal and vertical)
3. Print the grid and spans

The output will show us all viable word slots in the grid, which is exactly what we need for our crossword solver.

#### Understanding Operator Overloading

In this chapter, we used operator overloading to make our Point and Span objects easier to work with. The `<<` operator allows us to print these objects directly to an output stream:

```cpp
friend ostream& operator<<(ostream& os, const Point& p);
```

This is a non-member function declared as a friend, which gives it access to the object's private members. The implementation:

```cpp
ostream& operator<<(ostream& os, const Point& p) {
  os << "(" << p.row << "," << p.col << ")";
  return os;
};
```

Returns a reference to the stream, allowing for chained operations like `cout << p1 << p2`.

#### The Importance of const Correctness

Throughout our implementation, we've been careful with const correctness:

```cpp
char box(const Point& p) const {
  assert(in_bounds(p));
  return lines[p.row][p.col];
}
```

The first `const` indicates that the Point parameter won't be modified. The second `const` (after the parameter list) indicates that the method won't modify the Grid object itself.

This is important for:
- Preventing unintended modifications
- Enabling compiler optimizations
- Clearly communicating intent

#### Conclusion

In this chapter, we've implemented two fundamental structures for our crossword puzzle solver:

1. **Points**: Representing specific locations in the grid
2. **Spans**: Representing sequences of cells where words can be placed

We've also enhanced our Grid class to:
- Work with Points efficiently
- Navigate the grid systematically
- Identify all viable spans for word placement

These components form the foundation for the next phase of our project: matching words from our library to spans in the grid.

In the next chapter, "Find Spans in the Grid," we'll build on this foundation to extract the current state of spans from the grid, which will allow us to find appropriate words to fill them.

#### Practice Exercises

1. Add methods to the Grid class to set and get letters at specific Points.
2. Implement a method to check if two Spans intersect and find the intersection Point.
3. Create a function that identifies all Spans of a specific length.
4. Add validation to ensure that Spans are only created for sequences of at least 3 cells (a common crossword rule).
5. Implement a method to check if a given word can be placed in a specific Span, considering existing letters.

### 14. Find Spans in the Grid
[https://youtu.be/_LlUZLRsxcU](https://youtu.be/_LlUZLRsxcU)
### 14. Find Spans in the Grid

In this chapter, we'll build on our Points and Spans foundations from Chapter 13 to implement functionality that identifies and extracts all viable spans from a crossword grid. This is a crucial step that enables our solver to identify where words can be placed and what constraints they must satisfy.

#### Review of Points and Spans

Before we dive into finding spans, let's quickly review our Point and Span structures:

- A **Point** represents a specific location in the grid, defined by a row and column.
- A **Span** represents a sequence of cells where a word can be placed, defined by a starting point, a length, and a direction (horizontal or vertical).

In Chapter 13, we laid the groundwork for these structures. Now we'll put them to work to scan the grid and identify all viable spans.

#### Enhancing Our Grid Class

Let's start by making our Grid class fully capable of working with Points and Spans. We'll ensure our function signatures use const where appropriate and update our type definitions:

```cpp
#include <assert.h>
#include <fstream>
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

// ----------------------------------------------------------------
//-Point
struct Point {
  Point() {}
  Point(int r, int c) : row(r), col(c) {}

  friend ostream& operator<<(ostream& os, const Point& p);
  int row = 0;
  int col = 0;
};

ostream& operator<<(ostream& os, const Point& p) {
  os << "(" << p.row << "," << p.col << ")";
  return os;
};

// ----------------------------------------------------------------
//-Span
struct Span {
  Span(Point p, int l, bool v) : point(p), len(l), vert(v) {}

  friend ostream& operator<<(ostream& os, const Span& s);
  Point point;
  int len;
  bool vert;
};
typedef vector<Span> Spans;

ostream& operator<<(ostream& os, const Span& s) {
  os << "[" << s.point << "len=" << s.len << " vert=" << s.vert << "]";
  return os;
};
```

#### Grid Cell Access Methods

Next, we'll implement methods to access and check cells in the grid:

```cpp
struct Grid {
  // ... existing constructor and basic methods ...

  // Returns character value of the box at point 'p'.
  char box(const Point& p) const {
    assert(in_bounds(p));
    return lines[p.row][p.col];
  }

  // Returns true if the point p is a '.' "block" in the grid.
  // 'p' must be in bounds.
  bool is_block(const Point& p) const { return box(p) == '.'; }

  bool is_blank(const Point& p) const { return box(p) == '-'; }

  bool is_letter(const Point& p) const {
    char c = box(p);
    return c >= 'A' && c <= 'Z';
  }

  bool in_bounds(const Point& p) const {
    return (p.row >= 0 && p.row < rows() && p.col >= 0 && p.col < cols());
  }
};
```

These methods make it easy to query the grid at specific points and check cell types. Note the use of `const` to ensure these methods don't modify the grid.

#### Grid Traversal Logic

To find spans, we need to systematically traverse the grid. Let's implement a `Next` method that advances a point to the next position:

```cpp
struct Grid {
  // ... existing methods ...

  // Next increments the point across the grid, one box at a time.
  // Returns true if point is still in bounds
  bool Next(Point& p, bool vert) {
    if (vert) {
      p.row++;
      if (p.row >= rows()) {
        p.row = 0;
        p.col++;
      }
    } else {
      p.col++;
      if (p.col >= cols()) {
        p.col = 0;
        p.row++;
      }
    }
    return in_bounds(p);
  }
};
```

This method advances the point either vertically (down then right) or horizontally (right then down), and returns whether the point is still within the grid bounds.

#### The Core Algorithm: Finding Spans

Now we'll implement the core algorithm for finding spans in the grid. We'll scan the grid, identify sequences of non-block cells, and create Span objects for each:

```cpp
struct Grid {
  // ... existing methods ...

  void FillSpans(bool vert) {
    Point p;
    while (in_bounds(p)) {
      // Skip blocks until we find a non-block cell
      while (in_bounds(p) && is_block(p)) {
        Next(p, vert);
      }
      if (!in_bounds(p)) return;
      
      // Found the start of a potential span
      Point startp = p;

      // Count how long this span is
      int len = 0;
      do {
        Next(p, vert);
        len++;
      } while (in_bounds(p) && !is_block(p));
      
      // Only add spans that are at least 2 cells long (typical crossword constraint)
      if (len >= 2) {
        spans.push_back(Span(startp, len, vert));
      }
    }
  }

  // Add to 'spans' vector with all viable spans in the grid
  void FillSpans() {
    assert(spans.empty());
    FillSpans(false);  // horizontal spans
    FillSpans(true);   // vertical spans
  }
};
```

The algorithm works as follows:

1. Start at the top-left of the grid (0,0)
2. Skip any blocks until we find a non-block cell
3. When a non-block cell is found, mark it as the start of a span
4. Continue until we hit another block or the edge of the grid
5. Create a Span object and add it to our spans vector
6. Repeat the process for both horizontal and vertical directions

#### Debugging and Visualization

To help debug and visualize our spans, let's add methods to print the grid and its spans:

```cpp
struct Grid {
  // ... existing methods ...

  void Print() const {
    cout << "Grid : " << name << " (rows=" << rows() << ", cols=" << cols() << ")" << endl;
    for (string s : lines) {
      cout << s << endl;
    }
  }

  void PrintSpans() const {
    cout << "Spans:" << endl;
    for (const Span& s : spans) {
      cout << "  " << s << endl;
    }
  }
};
```

#### Additional Span Analysis

Let's add some methods to analyze and work with spans:

```cpp
struct Grid {
  // ... existing methods ...
  
  // Get the current content of a span as a string
  string GetSpanContent(const Span& s) const {
    string content;
    Point p = s.point;
    
    for (int i = 0; i < s.len; i++) {
      content.push_back(box(p));
      
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
    
    return content;
  }
  
  // Count spans by length
  void AnalyzeSpans() const {
    int maxlen = 0;
    for (const Span& s : spans) {
      maxlen = max(maxlen, s.len);
    }
    
    vector<int> hcount(maxlen + 1, 0);
    vector<int> vcount(maxlen + 1, 0);
    
    for (const Span& s : spans) {
      if (s.vert) {
        vcount[s.len]++;
      } else {
        hcount[s.len]++;
      }
    }
    
    cout << "Span analysis:" << endl;
    for (int i = 2; i <= maxlen; i++) {
      cout << "  Length " << i << ": " << hcount[i] << " horizontal, " 
           << vcount[i] << " vertical" << endl;
    }
  }
};
```

The `GetSpanContent` method extracts the current content of a span (including letters, blanks, and any other characters), which will be useful for determining what words can fit in each span.

The `AnalyzeSpans` method provides statistics about the spans in the grid, counting how many spans of each length exist in both horizontal and vertical directions.

#### Finding Intersections

An important aspect of crossword puzzles is that words intersect. Let's add a method to find intersections between spans:

```cpp
struct Grid {
  // ... existing methods ...
  
  // Check if two spans intersect
  bool SpansIntersect(const Span& s1, const Span& s2, Point& intersection) const {
    // Spans must be in different directions to intersect
    if (s1.vert == s2.vert) return false;
    
    const Span& hspan = s1.vert ? s2 : s1;
    const Span& vspan = s1.vert ? s1 : s2;
    
    // Check if horizontal span's row is within vertical span's row range
    if (hspan.point.row < vspan.point.row || 
        hspan.point.row >= vspan.point.row + vspan.len) {
      return false;
    }
    
    // Check if vertical span's column is within horizontal span's column range
    if (vspan.point.col < hspan.point.col || 
        vspan.point.col >= hspan.point.col + hspan.len) {
      return false;
    }
    
    // Calculate the intersection point
    intersection.row = hspan.point.row;
    intersection.col = vspan.point.col;
    return true;
  }
  
  // Build a map of intersections between spans
  void FindIntersections() {
    for (size_t i = 0; i < spans.size(); i++) {
      for (size_t j = i + 1; j < spans.size(); j++) {
        Point intersection;
        if (SpansIntersect(spans[i], spans[j], intersection)) {
          cout << "Spans " << i << " and " << j << " intersect at " 
               << intersection << endl;
        }
      }
    }
  }
};
```

The `SpansIntersect` method determines if two spans intersect and, if they do, calculates the intersection point. The `FindIntersections` method identifies all intersections in the grid, which will be crucial for our solving algorithm.

#### Putting It All Together

Now, let's combine all these components into a complete implementation:

```cpp
#include <assert.h>
#include <fstream>
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

string ToUpper(string s) {
  string s2;
  for (char c : s) {
    s2.push_back(toupper(c));
  }
  return s2;
};

// ----------------------------------------------------------------
//-Point
struct Point {
  Point() {}
  Point(int r, int c) : row(r), col(c) {}

  friend ostream& operator<<(ostream& os, const Point& p);
  int row = 0;
  int col = 0;
};

ostream& operator<<(ostream& os, const Point& p) {
  os << "(" << p.row << "," << p.col << ")";
  return os;
};

// ----------------------------------------------------------------
//-Span
struct Span {
  Span(Point p, int l, bool v) : point(p), len(l), vert(v) {}

  friend ostream& operator<<(ostream& os, const Span& s);
  Point point;
  int len;
  bool vert;
};
typedef vector<Span> Spans;

ostream& operator<<(ostream& os, const Span& s) {
  os << "[" << s.point << "len=" << s.len << " vert=" << s.vert << "]";
  return os;
};

// ----------------------------------------------------------------
//-Word
struct Word {
  Word() {}
  Word(string s) : word(s) {}
  int len() const { return word.length(); }
  string word;
};
typedef vector<Word*> Words;
typedef unordered_map<string, Words> WordMap;

// ----------------------------------------------------------------
//-Library
class Library {
 public:
  // ... Library implementation from previous chapters ...
};

// ----------------------------------------------------------------
//-Grid
struct Grid {
  Grid(string n) { name = n; }

  int rows() const { return lines.size(); }

  int cols() const {
    if (lines.empty()) {
      return 0;
    } else {
      return lines[0].size();
    }
  }

  // Returns character value of the box at point 'p'.
  char box(const Point& p) const {
    assert(in_bounds(p));
    return lines[p.row][p.col];
  }

  // Returns true if the point p is a '.' "block" in the grid.
  // 'p' must be in bounds.
  bool is_block(const Point& p) const { return box(p) == '.'; }

  bool is_blank(const Point& p) const { return box(p) == '-'; }

  bool is_letter(const Point& p) const {
    char c = box(p);
    return c >= 'A' && c <= 'Z';
  }

  bool in_bounds(const Point& p) const {
    return (p.row >= 0 && p.row < rows() && p.col >= 0 && p.col < cols());
  }

  // Next increments the point across the grid, one box at a time.
  // Returns true if point is still in bounds
  bool Next(Point& p, bool vert) {
    if (vert) {
      p.row++;
      if (p.row >= rows()) {
        p.row = 0;
        p.col++;
      }
    } else {
      p.col++;
      if (p.col >= cols()) {
        p.col = 0;
        p.row++;
      }
    }
    return in_bounds(p);
  }

  void FillSpans(bool vert) {
    Point p;
    while (in_bounds(p)) {
      while (in_bounds(p) && is_block(p)) {
        Next(p, vert);
      }
      if (!in_bounds(p)) return;
      Point startp = p;

      int len = 0;
      do {
        Next(p, vert);
        len++;
      } while (in_bounds(p) && !is_block(p));
      
      if (len >= 2) {  // Only add spans of length 2 or more
        spans.push_back(Span(startp, len, vert));
      }
    }
  }

  // Add to 'spans' vector with all viable spans in the grid
  void FillSpans() {
    assert(spans.empty());
    FillSpans(false);  // horiz
    FillSpans(true);   // vert
  }
  
  string GetSpanContent(const Span& s) const {
    string content;
    Point p = s.point;
    
    for (int i = 0; i < s.len; i++) {
      content.push_back(box(p));
      
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
    
    return content;
  }
  
  bool SpansIntersect(const Span& s1, const Span& s2, Point& intersection) const {
    if (s1.vert == s2.vert) return false;
    
    const Span& hspan = s1.vert ? s2 : s1;
    const Span& vspan = s1.vert ? s1 : s2;
    
    if (hspan.point.row < vspan.point.row || 
        hspan.point.row >= vspan.point.row + vspan.len) {
      return false;
    }
    
    if (vspan.point.col < hspan.point.col || 
        vspan.point.col >= hspan.point.col + hspan.len) {
      return false;
    }
    
    intersection.row = hspan.point.row;
    intersection.col = vspan.point.col;
    return true;
  }
  
  void FindIntersections() {
    for (size_t i = 0; i < spans.size(); i++) {
      for (size_t j = i + 1; j < spans.size(); j++) {
        Point intersection;
        if (SpansIntersect(spans[i], spans[j], intersection)) {
          cout << "Spans " << i << " and " << j << " intersect at " 
               << intersection << endl;
        }
      }
    }
  }
  
  void AnalyzeSpans() const {
    int maxlen = 0;
    for (const Span& s : spans) {
      maxlen = max(maxlen, s.len);
    }
    
    vector<int> hcount(maxlen + 1, 0);
    vector<int> vcount(maxlen + 1, 0);
    
    for (const Span& s : spans) {
      if (s.vert) {
        vcount[s.len]++;
      } else {
        hcount[s.len]++;
      }
    }
    
    cout << "Span analysis:" << endl;
    for (int i = 2; i <= maxlen; i++) {
      cout << "  Length " << i << ": " << hcount[i] << " horizontal, " 
           << vcount[i] << " vertical" << endl;
    }
  }

  void LoadFromFile(string filename) {
    ifstream f;
    f.open(filename);
    while (f.is_open() && !f.eof()) {
      string line;
      getline(f, line);
      if (!line.empty() && line[0] != '#') {
        lines.push_back(line);
      }
    }
    f.close();
  }

  int Check() const {
    for (string s : lines) {
      assert(s.size() == cols());
    }
    return 0;
  }

  void Print() const {
    cout << "Grid : " << name << " (rows=" << rows() << ", cols=" << cols()
         << ")" << endl;
    for (string s : lines) {
      cout << s << endl;
    }
  }

  void PrintSpans() const {
    cout << "Spans:" << endl;
    for (size_t i = 0; i < spans.size(); i++) {
      const Span& s = spans[i];
      cout << "  " << i << ": " << s << " content: \"" << GetSpanContent(s) << "\"" << endl;
    }
  }

  string name;
  vector<string> lines;
  Spans spans;
};

int main() {
  Grid grid("MY GRID");
  grid.LoadFromFile("test.txt");
  grid.Check();
  grid.Print();
  grid.FillSpans();
  grid.PrintSpans();
  grid.AnalyzeSpans();
  grid.FindIntersections();

  return 0;
}
```

#### Testing with a Real Grid

Let's test our implementation with a sample grid:

```
# test.txt
DOG....
---....
----...
-------
...----
....---
...CATS
```

When we run our program with this grid, it will:
1. Load the grid from the file
2. Find all viable spans in both horizontal and vertical directions
3. Print the grid and spans
4. Analyze the spans by length
5. Identify all intersections between spans

This output gives us a complete picture of the word slots in our crossword puzzle, which is exactly what we need for our solving algorithm.

#### Understanding the Algorithm

Let's analyze the key parts of our algorithm:

1. **Grid Scanning**: We start at (0,0) and scan the grid systematically, either horizontally (right then down) or vertically (down then right).

2. **Span Identification**: Whenever we find a non-block cell followed by one or more non-block cells, we identify this as a span.

3. **Constraint Enforcement**: We only consider spans of length 2 or more, which is a common constraint in crossword puzzles.

4. **Intersection Detection**: We identify where horizontal and vertical spans cross, which creates additional constraints for word selection.

5. **Content Extraction**: We extract the current content of each span, which helps us determine what words can fit there.

This approach gives us a complete representation of the crossword grid structure, which we'll use in subsequent chapters to implement our solving algorithm.

#### Conclusion

In this chapter, we've implemented robust functionality for finding and analyzing spans in a crossword grid. We can now:

1. Identify all viable spans where words can be placed
2. Extract the current content of spans
3. Find intersections between spans
4. Analyze the distribution of span lengths

These capabilities form the foundation for our crossword solver. In the next chapter, "Get Strings from the Grid," we'll build on this foundation to extract the current state of the grid and prepare for filling in words.

#### Practice Exercises

1. Modify the `FillSpans` method to enforce a minimum span length of 3 (a common rule in many crossword puzzles).
2. Implement a method to find all spans that contain a specific point.
3. Create a function that determines if a word can legally be placed in a span, considering the existing letters.
4. Add functionality to identify "isolated" spans that don't intersect with any other spans.
5. Implement a visualization method that displays the grid with span indices, to make it easier to see which spans correspond to which positions.

### 15. Get Strings from the Grid
[https://youtu.be/IyqaPP-I6UQ](https://youtu.be/IyqaPP-I6UQ)
### 15. Get Strings from the Grid

In this chapter, we'll build on our previous work to extract string patterns from the grid based on the spans we identified in Chapter 14. This is a critical step toward our ultimate goal of filling in the crossword grid with valid words.

#### The Challenge of String Extraction

Now that we can identify all the spans in our grid, we need to extract the current content of each span. This will give us patterns like "D--" or "C-T" that we can use to search our word library. These patterns will include:

- Known letters that are already filled in the grid
- Empty cells represented by dashes ('-')
- Any other constraints we need to consider

#### Enhancing GetSpanContent

In Chapter 14, we introduced a basic `GetSpanContent` method to extract the content of a span. Let's refine this method to make it more useful for our solver:

```cpp
string GetSpanContent(const Span& s) const {
  string content;
  Point p = s.point;
  
  for (int i = 0; i < s.len; i++) {
    content.push_back(box(p));
    
    if (s.vert) {
      p.row++;
    } else {
      p.col++;
    }
  }
  
  return content;
}
```

This method works by:
1. Starting at the span's beginning point
2. Moving through the span one cell at a time
3. Adding each cell's character to a string
4. Returning the complete string pattern

#### Creating a Pattern Structure

To better organize our code, let's create a dedicated structure for patterns:

```cpp
struct Pattern {
  Pattern(Span s, string p) : span(s), pattern(p) {}
  
  Span span;
  string pattern;
  
  friend ostream& operator<<(ostream& os, const Pattern& pat);
};

ostream& operator<<(ostream& os, const Pattern& pat) {
  os << pat.pattern << " at " << pat.span;
  return os;
}
```

This structure associates a pattern string with its corresponding span, which will be useful when we need to update the grid.

#### Extracting All Patterns from the Grid

Now, let's implement a method to extract patterns for all spans in the grid:

```cpp
typedef vector<Pattern> Patterns;

struct Grid {
  // ... existing methods ...
  
  Patterns GetAllPatterns() const {
    Patterns result;
    
    for (const Span& s : spans) {
      string content = GetSpanContent(s);
      result.push_back(Pattern(s, content));
    }
    
    return result;
  }
};
```

This method builds a collection of Pattern objects by extracting the content of each span.

#### Pattern Analysis and Classification

Different patterns have different levels of constraint. Let's add methods to analyze patterns:

```cpp
struct Pattern {
  // ... existing code ...
  
  // Count how many empty cells are in the pattern
  int EmptyCellCount() const {
    int count = 0;
    for (char c : pattern) {
      if (c == '-') count++;
    }
    return count;
  }
  
  // Check if the pattern is completely empty
  bool IsEmpty() const {
    for (char c : pattern) {
      if (c != '-') return false;
    }
    return true;
  }
  
  // Check if the pattern is completely filled (no empty cells)
  bool IsFilled() const {
    return EmptyCellCount() == 0;
  }
};
```

These methods help us understand how constrained each pattern is, which will be useful for our solving algorithm.

#### Finding the Most Constrained Patterns

A common strategy in crossword solving is to start with the most constrained patterns - those with the fewest empty cells. Let's add a method to sort patterns by constraint level:

```cpp
struct Grid {
  // ... existing methods ...
  
  Patterns GetSortedPatterns() const {
    Patterns result = GetAllPatterns();
    
    // Sort by number of empty cells (ascending)
    sort(result.begin(), result.end(), 
         [](const Pattern& a, const Pattern& b) {
           int a_empty = a.EmptyCellCount();
           int b_empty = b.EmptyCellCount();
           
           // If equal empty counts, prefer shorter patterns
           if (a_empty == b_empty) {
             return a.pattern.length() < b.pattern.length();
           }
           
           return a_empty < b_empty;
         });
    
    return result;
  }
};
```

This method sorts patterns by:
1. Number of empty cells (ascending)
2. Pattern length (ascending) as a tiebreaker

This gives us a sequence of patterns to fill, starting with the most constrained.

#### Finding Pattern Intersections

Patterns intersect at specific positions, creating additional constraints. Let's enhance our intersection detection:

```cpp
struct Grid {
  // ... existing methods ...
  
  // Find where a specific pattern intersects with other patterns
  vector<pair<Pattern, int>> FindIntersectingPatterns(const Pattern& pat) const {
    vector<pair<Pattern, int>> result;
    
    for (const Span& s : spans) {
      // Skip the span corresponding to our pattern
      if (s.point.row == pat.span.point.row && 
          s.point.col == pat.span.point.col && 
          s.len == pat.span.len && 
          s.vert == pat.span.vert) {
        continue;
      }
      
      Point intersection;
      if (SpansIntersect(pat.span, s, intersection)) {
        // Calculate position within each pattern
        int pos_in_pat;
        if (pat.span.vert) {
          pos_in_pat = intersection.row - pat.span.point.row;
        } else {
          pos_in_pat = intersection.col - pat.span.point.col;
        }
        
        string other_content = GetSpanContent(s);
        result.push_back(make_pair(Pattern(s, other_content), pos_in_pat));
      }
    }
    
    return result;
  }
};
```

This method:
1. Takes a pattern as input
2. Finds all other patterns that intersect with it
3. Calculates the position of intersection within the input pattern
4. Returns a collection of intersecting patterns and positions

This information will be crucial for ensuring that word placements are consistent at intersections.

#### Validating Word Placement

Now let's implement a method to check if a word can legally be placed in a span:

```cpp
struct Grid {
  // ... existing methods ...
  
  // Check if a word can be placed in a span
  bool CanPlaceWord(const Span& s, const string& word) const {
    if (word.length() != s.len) return false;
    
    string current = GetSpanContent(s);
    
    for (size_t i = 0; i < current.length(); i++) {
      if (current[i] != '-' && current[i] != word[i]) {
        return false;
      }
    }
    
    return true;
  }
};
```

This method checks if:
1. The word length matches the span length
2. The word is compatible with any existing letters in the span

#### Placing a Word in the Grid

Once we've verified that a word can be placed, we need a method to actually update the grid:

```cpp
struct Grid {
  // ... existing methods ...
  
  // Place a word in the grid at the specified span
  void PlaceWord(const Span& s, const string& word) {
    assert(word.length() == s.len);
    
    Point p = s.point;
    for (size_t i = 0; i < word.length(); i++) {
      // Only update empty cells or cells that already match
      if (is_blank(p) || box(p) == word[i]) {
        // Update the grid
        lines[p.row][p.col] = word[i];
      } else {
        assert(box(p) == word[i]); // Ensure consistency
      }
      
      // Move to next position
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
  }
};
```

This method:
1. Verifies that the word length matches the span length
2. Updates the grid one cell at a time
3. Only modifies empty cells or cells that already match
4. Uses assertions to catch any inconsistencies

#### Putting It All Together

Let's combine all these methods into our Grid class:

```cpp
#include <assert.h>
#include <algorithm>
#include <fstream>
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

// ... Point and Span structures from previous chapters ...

struct Pattern {
  Pattern(Span s, string p) : span(s), pattern(p) {}
  
  Span span;
  string pattern;
  
  // Count how many empty cells are in the pattern
  int EmptyCellCount() const {
    int count = 0;
    for (char c : pattern) {
      if (c == '-') count++;
    }
    return count;
  }
  
  // Check if the pattern is completely empty
  bool IsEmpty() const {
    for (char c : pattern) {
      if (c != '-') return false;
    }
    return true;
  }
  
  // Check if the pattern is completely filled (no empty cells)
  bool IsFilled() const {
    return EmptyCellCount() == 0;
  }
  
  friend ostream& operator<<(ostream& os, const Pattern& pat);
};

ostream& operator<<(ostream& os, const Pattern& pat) {
  os << pat.pattern << " at " << pat.span;
  return os;
}

typedef vector<Pattern> Patterns;

struct Grid {
  // ... existing methods from previous chapters ...
  
  string GetSpanContent(const Span& s) const {
    string content;
    Point p = s.point;
    
    for (int i = 0; i < s.len; i++) {
      content.push_back(box(p));
      
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
    
    return content;
  }
  
  Patterns GetAllPatterns() const {
    Patterns result;
    
    for (const Span& s : spans) {
      string content = GetSpanContent(s);
      result.push_back(Pattern(s, content));
    }
    
    return result;
  }
  
  Patterns GetSortedPatterns() const {
    Patterns result = GetAllPatterns();
    
    // Sort by number of empty cells (ascending)
    sort(result.begin(), result.end(), 
         [](const Pattern& a, const Pattern& b) {
           int a_empty = a.EmptyCellCount();
           int b_empty = b.EmptyCellCount();
           
           // If equal empty counts, prefer shorter patterns
           if (a_empty == b_empty) {
             return a.pattern.length() < b.pattern.length();
           }
           
           return a_empty < b_empty;
         });
    
    return result;
  }
  
  vector<pair<Pattern, int>> FindIntersectingPatterns(const Pattern& pat) const {
    vector<pair<Pattern, int>> result;
    
    for (const Span& s : spans) {
      // Skip the span corresponding to our pattern
      if (s.point.row == pat.span.point.row && 
          s.point.col == pat.span.point.col && 
          s.len == pat.span.len && 
          s.vert == pat.span.vert) {
        continue;
      }
      
      Point intersection;
      if (SpansIntersect(pat.span, s, intersection)) {
        // Calculate position within each pattern
        int pos_in_pat;
        if (pat.span.vert) {
          pos_in_pat = intersection.row - pat.span.point.row;
        } else {
          pos_in_pat = intersection.col - pat.span.point.col;
        }
        
        string other_content = GetSpanContent(s);
        result.push_back(make_pair(Pattern(s, other_content), pos_in_pat));
      }
    }
    
    return result;
  }
  
  bool CanPlaceWord(const Span& s, const string& word) const {
    if (word.length() != s.len) return false;
    
    string current = GetSpanContent(s);
    
    for (size_t i = 0; i < current.length(); i++) {
      if (current[i] != '-' && current[i] != word[i]) {
        return false;
      }
    }
    
    return true;
  }
  
  void PlaceWord(const Span& s, const string& word) {
    assert(word.length() == s.len);
    
    Point p = s.point;
    for (size_t i = 0; i < word.length(); i++) {
      // Only update empty cells or cells that already match
      if (is_blank(p) || box(p) == word[i]) {
        // Update the grid
        lines[p.row][p.col] = word[i];
      } else {
        assert(box(p) == word[i]); // Ensure consistency
      }
      
      // Move to next position
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
  }
  
  void PrintPatterns() const {
    Patterns patterns = GetAllPatterns();
    cout << "Patterns:" << endl;
    for (size_t i = 0; i < patterns.size(); i++) {
      const Pattern& pat = patterns[i];
      cout << "  " << i << ": " << pat << " (empty: " << pat.EmptyCellCount() << ")" << endl;
    }
  }
  
  void PrintSortedPatterns() const {
    Patterns patterns = GetSortedPatterns();
    cout << "Sorted Patterns (by constraint):" << endl;
    for (size_t i = 0; i < patterns.size(); i++) {
      const Pattern& pat = patterns[i];
      cout << "  " << i << ": " << pat << " (empty: " << pat.EmptyCellCount() << ")" << endl;
    }
  }
};

int main() {
  Grid grid("MY GRID");
  grid.LoadFromFile("test.txt");
  grid.Check();
  grid.Print();
  grid.FillSpans();
  
  cout << "\nAll patterns:" << endl;
  grid.PrintPatterns();
  
  cout << "\nSorted patterns:" << endl;
  grid.PrintSortedPatterns();
  
  // Test pattern intersections
  Patterns patterns = grid.GetAllPatterns();
  if (!patterns.empty()) {
    Pattern& first_pattern = patterns[0];
    cout << "\nIntersections for pattern " << first_pattern << ":" << endl;
    
    auto intersections = grid.FindIntersectingPatterns(first_pattern);
    for (const auto& pair : intersections) {
      cout << "  Intersects with " << pair.first << " at position " << pair.second << endl;
    }
    
    // Test word placement if we have a partially filled pattern
    if (!first_pattern.IsEmpty() && !first_pattern.IsFilled()) {
      string test_word = first_pattern.pattern;
      // Replace all dashes with 'X' as a test
      for (char& c : test_word) {
        if (c == '-') c = 'X';
      }
      
      cout << "\nTesting word placement:" << endl;
      cout << "  Can place '" << test_word << "' in " << first_pattern.span << "? ";
      bool can_place = grid.CanPlaceWord(first_pattern.span, test_word);
      cout << (can_place ? "Yes" : "No") << endl;
      
      if (can_place) {
        cout << "  Placing word and updating grid:" << endl;
        grid.PlaceWord(first_pattern.span, test_word);
        grid.Print();
        
        // Show updated patterns
        cout << "\nUpdated patterns:" << endl;
        grid.PrintPatterns();
      }
    }
  }
  
  return 0;
}
```

#### Testing with a Real Grid

Let's test our implementation with a sample grid:

```
# test.txt
DOG....
---....
----...
-------
...----
....---
...CATS
```

When we run our program with this grid, it will:
1. Extract patterns for all spans
2. Sort patterns by constraint level
3. Test pattern intersections
4. Demonstrate word placement

This gives us all the tools we need to manipulate patterns and words within the grid.

#### Understanding the Algorithm

Let's analyze the key aspects of our string extraction and manipulation:

1. **Pattern Extraction**: We extract string patterns from spans, capturing the current state of the grid.

2. **Pattern Classification**: We analyze patterns based on their constraint level (number of empty cells).

3. **Pattern Sorting**: We sort patterns to prioritize the most constrained ones, which is an efficient solving strategy.

4. **Intersection Detection**: We identify where patterns intersect, which creates additional constraints.

5. **Word Placement Validation**: We check if a word can legally be placed in a span, considering existing letters.

6. **Grid Updates**: We place words in the grid, updating only the appropriate cells.

These capabilities form the core of our crossword solving algorithm. By manipulating patterns and words in this way, we can systematically fill the grid with valid words.

#### Conclusion

In this chapter, we've implemented robust functionality for extracting and manipulating string patterns in a crossword grid. We can now:

1. Extract patterns from all spans in the grid
2. Analyze and classify patterns by constraint level
3. Find intersections between patterns
4. Validate word placements
5. Update the grid with new words

These capabilities complete the foundation for our crossword solver. In the next chapter, "Solver Class," we'll bring all these components together to create a comprehensive solving algorithm.

#### Practice Exercises

1. Modify the Pattern structure to include a score based on how difficult it will be to fill (considering both empty cells and available words).
2. Implement a method to find all valid words from a dictionary that can fit a specific pattern.
3. Create a function that suggests the best word to place next, considering both pattern constraints and word frequency.
4. Add functionality to backtrack when a pattern cannot be filled, undoing previous word placements.
5. Implement a visualization method that highlights patterns with different colors based on their constraint level.

### 16. Solver Class
[https://youtu.be/b05M5oPZGgc](https://youtu.be/b05M5oPZGgc)
### 16. Solver Class

In this chapter, we'll bring together all the components we've built so far to create a Solver class that can automatically fill a crossword grid with valid words. This represents the culmination of our work and will demonstrate how our various algorithms work together to solve the crossword puzzle.

#### The Solving Challenge

Solving a crossword grid is a complex task that involves:
1. Finding all possible locations (spans) where words can be placed
2. Identifying the current state of the grid (existing letters and empty cells)
3. Finding words that fit the constraints at each position
4. Dealing with intersections between horizontal and vertical words
5. Potentially backtracking when we reach a dead end

Our Solver class will handle all these challenges using a recursive approach with backtracking.

#### Designing the Solver Class

Let's start by defining the structure of our Solver class:

```cpp
class Solver {
public:
  Solver(Grid& g, Library& l) : grid_(g), lib_(l) {}
  
  bool Solve();
  
private:
  bool SolveRecursive(const Patterns& patterns, size_t index);
  vector<string> FindCandidateWords(const Pattern& pattern);
  
  Grid& grid_;
  Library& lib_;
};
```

Our Solver takes references to a Grid and a Library, which it will use to fill the grid with words from the library. The main solving logic is in the `Solve` method, which prepares the grid and initiates the recursive solving process.

#### Implementing the Main Solve Method

Let's implement the main `Solve` method:

```cpp
bool Solver::Solve() {
  // Make sure spans are calculated
  if (grid_.spans.empty()) {
    grid_.FillSpans();
  }
  
  // Get patterns sorted by constraint
  Patterns patterns = grid_.GetSortedPatterns();
  
  // Start the recursive solving process
  return SolveRecursive(patterns, 0);
}
```

This method:
1. Ensures that spans have been identified in the grid
2. Gets patterns sorted by constraint (most constrained first)
3. Starts the recursive solving process with the first pattern

#### Finding Candidate Words

Before we implement the recursive solver, let's create a method to find candidate words that match a pattern:

```cpp
vector<string> Solver::FindCandidateWords(const Pattern& pattern) {
  vector<string> candidates;
  
  // Find all words in the library that match this pattern
  auto matches = lib_.FindMatchingWords(pattern.pattern);
  
  for (const Word* word : matches) {
    // Verify that the word fits the pattern
    if (grid_.CanPlaceWord(pattern.span, word->word)) {
      candidates.push_back(word->word);
    }
  }
  
  return candidates;
}
```

This method:
1. Uses the Library to find words that match the pattern
2. Verifies each word against the grid to ensure it can be placed
3. Returns a list of valid candidate words

#### The Recursive Solving Algorithm

Now, let's implement the core recursive solving algorithm:

```cpp
bool Solver::SolveRecursive(const Patterns& patterns, size_t index) {
  // Base case: we've filled all patterns
  if (index >= patterns.size()) {
    return true;  // Success!
  }
  
  // Get the current pattern to fill
  const Pattern& current = patterns[index];
  
  // If the pattern is already filled, move to the next one
  if (current.IsFilled()) {
    return SolveRecursive(patterns, index + 1);
  }
  
  // Find candidate words for this pattern
  vector<string> candidates = FindCandidateWords(current);
  
  // Try each candidate
  for (const string& word : candidates) {
    // Place the word in the grid
    grid_.PlaceWord(current.span, word);
    
    // Recursively try to solve the rest of the grid
    if (SolveRecursive(patterns, index + 1)) {
      return true;  // Success!
    }
    
    // If we get here, this word didn't lead to a solution.
    // Backtrack by removing the word from the grid.
    // We'll implement a RemoveWord method for the Grid class.
    grid_.RemoveWord(current.span);
  }
  
  // If we tried all candidates and none worked, this is a dead end
  return false;
}
```

This algorithm:
1. Takes a collection of patterns and the current index to process
2. Checks if we've filled all patterns (base case)
3. Skips patterns that are already filled
4. Finds candidate words for the current pattern
5. Tries each candidate word:
   - Places the word in the grid
   - Recursively tries to solve the rest of the grid
   - If successful, returns true
   - If not, backtracks by removing the word
6. Returns false if no candidates lead to a solution

#### Adding RemoveWord to the Grid Class

To support backtracking, we need to add a `RemoveWord` method to our Grid class:

```cpp
void Grid::RemoveWord(const Span& s) {
  Point p = s.point;
  
  for (int i = 0; i < s.len; i++) {
    // Check if this position is at an intersection
    bool is_intersection = false;
    
    // Scan all spans to find intersections
    for (const Span& other : spans) {
      if (&other != &s) {  // Skip the current span
        Point intersection;
        if (SpansIntersect(s, other, intersection)) {
          if ((s.vert && intersection.row == p.row) ||
              (!s.vert && intersection.col == p.col)) {
            is_intersection = true;
            break;
          }
        }
      }
    }
    
    // Only remove non-intersection cells
    if (!is_intersection) {
      lines[p.row][p.col] = '-';  // Reset to empty
    }
    
    // Move to next position
    if (s.vert) {
      p.row++;
    } else {
      p.col++;
    }
  }
}
```

This method:
1. Resets cells in the span to empty ('-')
2. Preserves cells at intersections with other spans
3. This allows backtracking without removing letters that are part of other words

#### Adding Debug Output

To help understand the solving process, let's add some debug output:

```cpp
bool Solver::SolveRecursive(const Patterns& patterns, size_t index) {
  // ... existing code ...
  
  cout << "Solving pattern " << index << ": " << current.pattern << endl;
  
  // ... find candidates ...
  
  cout << "Found " << candidates.size() << " candidates" << endl;
  
  for (const string& word : candidates) {
    cout << "Trying word: " << word << endl;
    
    // ... place word and continue solving ...
    
    cout << "Backtracking from word: " << word << endl;
    grid_.RemoveWord(current.span);
  }
  
  cout << "No solution found for pattern " << index << endl;
  return false;
}
```

This helps visualize the solving process, showing which patterns are being solved and which words are being tried.

#### Putting It All Together

Now let's combine all these components into a complete implementation:

```cpp
#include <assert.h>
#include <algorithm>
#include <fstream>
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

// ... Point, Span, Pattern, Library, and Grid classes from previous chapters ...

// Add RemoveWord method to Grid class
void Grid::RemoveWord(const Span& s) {
  Point p = s.point;
  
  for (int i = 0; i < s.len; i++) {
    // Check if this position is at an intersection
    bool is_intersection = false;
    
    // Scan all spans to find intersections
    for (const Span& other : spans) {
      if (&other != &s) {  // Skip the current span
        Point intersection;
        if (SpansIntersect(s, other, intersection)) {
          if ((s.vert && intersection.row == p.row) ||
              (!s.vert && intersection.col == p.col)) {
            is_intersection = true;
            break;
          }
        }
      }
    }
    
    // Only remove non-intersection cells
    if (!is_intersection) {
      lines[p.row][p.col] = '-';  // Reset to empty
    }
    
    // Move to next position
    if (s.vert) {
      p.row++;
    } else {
      p.col++;
    }
  }
}

class Solver {
public:
  Solver(Grid& g, Library& l) : grid_(g), lib_(l) {}
  
  bool Solve() {
    // Make sure spans are calculated
    if (grid_.spans.empty()) {
      grid_.FillSpans();
    }
    
    // Get patterns sorted by constraint
    Patterns patterns = grid_.GetSortedPatterns();
    
    cout << "Starting to solve with " << patterns.size() << " patterns" << endl;
    
    // Start the recursive solving process
    return SolveRecursive(patterns, 0);
  }
  
private:
  bool SolveRecursive(const Patterns& patterns, size_t index) {
    // Base case: we've filled all patterns
    if (index >= patterns.size()) {
      return true;  // Success!
    }
    
    // Get the current pattern to fill
    const Pattern& current = patterns[index];
    
    cout << "Solving pattern " << index << ": " << current.pattern << endl;
    
    // If the pattern is already filled, move to the next one
    if (current.IsFilled()) {
      cout << "Pattern already filled, moving to next" << endl;
      return SolveRecursive(patterns, index + 1);
    }
    
    // Find candidate words for this pattern
    vector<string> candidates = FindCandidateWords(current);
    
    cout << "Found " << candidates.size() << " candidates" << endl;
    
    // Try each candidate
    for (const string& word : candidates) {
      cout << "Trying word: " << word << endl;
      
      // Place the word in the grid
      grid_.PlaceWord(current.span, word);
      
      // Recursively try to solve the rest of the grid
      if (SolveRecursive(patterns, index + 1)) {
        return true;  // Success!
      }
      
      cout << "Backtracking from word: " << word << endl;
      // If we get here, this word didn't lead to a solution.
      // Backtrack by removing the word from the grid.
      grid_.RemoveWord(current.span);
    }
    
    cout << "No solution found for pattern " << index << endl;
    // If we tried all candidates and none worked, this is a dead end
    return false;
  }
  
  vector<string> FindCandidateWords(const Pattern& pattern) {
    vector<string> candidates;
    
    // Find all words in the library that match this pattern
    auto matches = lib_.FindMatchingWords(pattern.pattern);
    
    for (const Word* word : matches) {
      // Verify that the word fits the pattern
      if (grid_.CanPlaceWord(pattern.span, word->word)) {
        candidates.push_back(word->word);
      }
    }
    
    return candidates;
  }
  
  Grid& grid_;
  Library& lib_;
};

int main() {
  // Load a library of words
  Library lib;
  lib.ReadFromFile("top_12000.txt");
  
  // Create and load a grid
  Grid grid("Crossword Puzzle");
  grid.LoadFromFile("test.txt");
  
  // Print the initial grid
  cout << "Initial grid:" << endl;
  grid.Print();
  
  // Create a solver and solve the grid
  Solver solver(grid, lib);
  bool success = solver.Solve();
  
  // Print the result
  cout << endl << "Solution " << (success ? "found" : "not found") << ":" << endl;
  grid.Print();
  
  return 0;
}
```

#### Understanding the Backtracking Algorithm

The core of our solver is a backtracking algorithm, which is a form of depth-first search:

1. We start with the most constrained pattern
2. We find all words that could fit this pattern
3. We try each word:
   - Place the word in the grid
   - Recursively try to solve the rest of the grid
   - If successful, we're done
   - If not, we remove the word and try the next one
4. If no words work, we backtrack to the previous pattern and try a different word

This approach systematically explores all possible combinations of words until it finds a valid solution or exhausts all possibilities.

#### Optimizing the Solver

Our basic solver works, but there are several optimizations we could make:

1. **Forward Checking**: When we place a word, immediately check if all intersecting patterns still have valid candidates.

2. **Variable Ordering**: Dynamically reorder patterns as we go, always choosing the most constrained one next.

3. **Value Ordering**: Sort candidate words by how likely they are to lead to a solution (e.g., by word frequency).

4. **Memoization**: Remember patterns we've already tried to avoid redundant work.

Let's implement a simple forward checking optimization:

```cpp
bool Solver::SolveRecursive(const Patterns& patterns, size_t index) {
  // ... existing code ...
  
  for (const string& word : candidates) {
    // Place the word in the grid
    grid_.PlaceWord(current.span, word);
    
    // Forward checking: verify that all intersecting patterns still have candidates
    bool valid = true;
    for (size_t i = index + 1; i < patterns.size(); i++) {
      const Pattern& next = patterns[i];
      string updated_pattern = grid_.GetSpanContent(next.span);
      
      // Skip already filled patterns
      if (next.IsFilled()) continue;
      
      // Check if this pattern still has candidate words
      auto next_matches = lib_.FindMatchingWords(updated_pattern);
      if (next_matches.empty()) {
        valid = false;
        break;
      }
    }
    
    if (valid) {
      // Recursively try to solve the rest of the grid
      if (SolveRecursive(patterns, index + 1)) {
        return true;  // Success!
      }
    }
    
    // Backtrack
    grid_.RemoveWord(current.span);
  }
  
  // ... existing code ...
}
```

This optimization checks if placing a word would create any patterns that can't be filled, allowing us to backtrack earlier.

#### Adding Metrics and Statistics

To better understand the solving process, let's add some metrics:

```cpp
class Solver {
public:
  // ... existing code ...
  
  // Add statistics tracking
  int GetBacktrackCount() const { return backtrack_count_; }
  int GetWordPlacementCount() const { return word_placement_count_; }
  
private:
  // ... existing code ...
  
  // Statistics
  int backtrack_count_ = 0;
  int word_placement_count_ = 0;
};

bool Solver::SolveRecursive(const Patterns& patterns, size_t index) {
  // ... existing code ...
  
  for (const string& word : candidates) {
    word_placement_count_++;
    // ... place word ...
    
    // ... backtrack ...
    backtrack_count_++;
  }
  
  // ... existing code ...
}
```

These metrics help us understand how efficient our solver is and where it's spending most of its time.

#### Conclusion

In this chapter, we've implemented a Solver class that brings together all the components we've built so far to automatically fill a crossword grid with valid words. The key features include:

1. **Pattern-Based Approach**: We identify patterns in the grid and fill them based on constraint level.

2. **Backtracking Algorithm**: We systematically try different word combinations, backtracking when necessary.

3. **Intersection Handling**: We ensure that words placed in the grid are consistent at intersections.

4. **Optimization Techniques**: We've implemented forward checking to improve efficiency.

Our solver demonstrates the power of combining data structures, algorithms, and object-oriented design to solve a complex problem. While there are many potential optimizations and enhancements, this implementation provides a solid foundation for crossword puzzle solving.

#### Practice Exercises

1. Implement dynamic pattern reordering to always choose the most constrained pattern next.
2. Add a time limit to the solver to prevent it from running too long on difficult puzzles.
3. Implement a heuristic to sort candidate words by frequency or some other measure of "goodness."
4. Add support for themed crosswords, where certain words must be included in the solution.
5. Create a visualization that shows the solving process step by step, highlighting pattern fills and backtracks.

### 17. Write Words to the Grid
[https://youtu.be/fFqyXMxfMVE](https://youtu.be/fFqyXMxfMVE)
### 17. Write Words to the Grid

In this chapter, we'll focus on enhancing our Grid class with robust methods to write words to the grid and manage the state of the grid during the solving process. This is a critical part of our crossword puzzle solver that ensures words are correctly placed and can be efficiently updated as the solver runs.

#### The Importance of Grid Updates

While we've already implemented basic word placement functionality in previous chapters, we need to refine and expand it to handle the complexities of:

1. Placing words while respecting existing letters
2. Tracking which cells are part of which words
3. Supporting efficient backtracking during solving
4. Handling word intersections correctly

#### Enhancing the Grid Class

Let's start by enhancing our Grid class with improved methods for word manipulation:

```cpp
struct Grid {
  // ... existing code from previous chapters ...
  
  // New methods for word manipulation
  bool PlaceWord(const Span& s, const string& word);
  bool RemoveWord(const Span& s);
  bool IsWordPlaceable(const Span& s, const string& word) const;
  
  // Helper method to get a reference to a cell
  char& CellAt(const Point& p) {
    assert(in_bounds(p));
    return lines[p.row][p.col];
  }
  
  // New data structures to track word placements
  vector<pair<Span, string>> placed_words;
};
```

We've added methods for placing, removing, and checking words, as well as a data structure to track which words have been placed.

#### Implementing an Improved PlaceWord Method

Let's implement a more robust `PlaceWord` method that returns whether the placement was successful and keeps track of placed words:

```cpp
bool Grid::PlaceWord(const Span& s, const string& word) {
  // Validate inputs
  if (word.length() != s.len) {
    return false;  // Word length doesn't match span length
  }
  
  // Check if the word fits the current grid state
  if (!IsWordPlaceable(s, word)) {
    return false;  // Word doesn't fit
  }
  
  // Place the word
  Point p = s.point;
  for (size_t i = 0; i < word.length(); i++) {
    CellAt(p) = word[i];
    
    // Move to next position
    if (s.vert) {
      p.row++;
    } else {
      p.col++;
    }
  }
  
  // Track this word placement
  placed_words.push_back(make_pair(s, word));
  
  return true;
}
```

This method:
1. Validates that the word length matches the span length
2. Checks if the word is compatible with existing letters
3. Places the word letter by letter
4. Tracks the placement in our `placed_words` list
5. Returns whether the placement was successful

#### Implementing IsWordPlaceable

The `IsWordPlaceable` method checks if a word can be placed in a span without contradicting existing letters:

```cpp
bool Grid::IsWordPlaceable(const Span& s, const string& word) const {
  if (word.length() != s.len) {
    return false;  // Word length doesn't match span length
  }
  
  string current = GetSpanContent(s);
  
  for (size_t i = 0; i < current.length(); i++) {
    char existing = current[i];
    if (existing != '-' && existing != word[i]) {
      return false;  // Conflict with existing letter
    }
  }
  
  return true;
}
```

This method:
1. Validates the word length
2. Gets the current content of the span
3. Checks if the word conflicts with any existing letters

#### Implementing an Improved RemoveWord Method

Now let's implement an improved `RemoveWord` method that correctly handles intersections and updates our tracking:

```cpp
bool Grid::RemoveWord(const Span& s) {
  // Find this span in our placed_words list
  auto it = find_if(placed_words.begin(), placed_words.end(),
    [&s](const pair<Span, string>& entry) {
      const Span& placed_span = entry.first;
      return placed_span.point.row == s.point.row &&
             placed_span.point.col == s.point.col &&
             placed_span.len == s.len &&
             placed_span.vert == s.vert;
    });
  
  // If we didn't find it, nothing to remove
  if (it == placed_words.end()) {
    return false;
  }
  
  // Get the word that was placed
  string word = it->second;
  
  // Remove from our tracking
  placed_words.erase(it);
  
  // Build a set of points that are part of intersections
  unordered_set<Point, PointHash> intersection_points;
  
  // Helper to hash Points
  struct PointHash {
    size_t operator()(const Point& p) const {
      return p.row * 10000 + p.col;
    }
  };
  
  struct PointEqual {
    bool operator()(const Point& a, const Point& b) const {
      return a.row == b.row && a.col == b.col;
    }
  };
  
  // Find all intersection points
  for (const auto& entry : placed_words) {
    const Span& other_span = entry.first;
    
    // Skip if same orientation
    if (other_span.vert == s.vert) {
      continue;
    }
    
    // Check for intersection
    Point intersection;
    if (SpansIntersect(s, other_span, intersection)) {
      intersection_points.insert(intersection);
    }
  }
  
  // Remove the word, preserving intersections
  Point p = s.point;
  for (size_t i = 0; i < s.len; i++) {
    // Check if this point is part of an intersection
    if (intersection_points.find(p) == intersection_points.end()) {
      // Not an intersection, clear the cell
      CellAt(p) = '-';
    }
    
    // Move to next position
    if (s.vert) {
      p.row++;
    } else {
      p.col++;
    }
  }
  
  return true;
}
```

This method:
1. Finds the span in our `placed_words` list
2. Builds a set of all points that are part of intersections with other placed words
3. Removes the word, preserving intersection points
4. Updates our tracking

Note that we need a custom hash function for Point objects to use them in an unordered_set.

#### Adding a PointHash Structure

Let's formally define the PointHash structure:

```cpp
struct PointHash {
  size_t operator()(const Point& p) const {
    return p.row * 10000 + p.col;  // Simple hash function
  }
};

struct PointEqual {
  bool operator()(const Point& a, const Point& b) const {
    return a.row == b.row && a.col == b.col;
  }
};
```

These helper structures allow us to use Point objects in unordered containers like unordered_set and unordered_map.

#### Tracking Word Placements

The `placed_words` vector gives us useful information about the current state of the grid. Let's add methods to utilize this:

```cpp
struct Grid {
  // ... existing code ...
  
  // Get all currently placed words
  vector<pair<Span, string>> GetPlacedWords() const {
    return placed_words;
  }
  
  // Check if a span already has a word placed
  bool IsSpanFilled(const Span& s) const {
    for (const auto& entry : placed_words) {
      const Span& placed_span = entry.first;
      if (placed_span.point.row == s.point.row &&
          placed_span.point.col == s.point.col &&
          placed_span.len == s.len &&
          placed_span.vert == s.vert) {
        return true;
      }
    }
    return false;
  }
  
  // Get the last placed word
  pair<Span, string> GetLastPlacedWord() const {
    assert(!placed_words.empty());
    return placed_words.back();
  }
  
  // Clear all placed words and reset the grid
  void ClearAllWords() {
    placed_words.clear();
    
    // Reset all cells to empty
    for (size_t r = 0; r < lines.size(); r++) {
      for (size_t c = 0; c < lines[r].size(); c++) {
        if (lines[r][c] != '.') {  // Don't clear blocks
          lines[r][c] = '-';
        }
      }
    }
  }
};
```

These methods provide useful functionality for managing word placements.

#### Testing Word Placement

Let's create a test function to demonstrate our word placement functionality:

```cpp
void TestWordPlacement(Grid& grid) {
  cout << "Initial grid:" << endl;
  grid.Print();
  
  // Find some spans
  if (grid.spans.empty()) {
    grid.FillSpans();
  }
  
  if (grid.spans.size() < 2) {
    cout << "Not enough spans for testing" << endl;
    return;
  }
  
  // Try to place a word
  const Span& span1 = grid.spans[0];
  string word1 = "TEST";
  
  if (span1.len != word1.length()) {
    cout << "Span length doesn't match word length" << endl;
    return;
  }
  
  cout << "Placing word '" << word1 << "' at " << span1 << endl;
  bool success = grid.PlaceWord(span1, word1);
  
  cout << "Placement " << (success ? "successful" : "failed") << endl;
  grid.Print();
  
  // Try to place another word that intersects
  const Span& span2 = grid.spans[1];
  
  // Find a word that fits and intersects properly
  string word2;
  for (char c = 'A'; c <= 'Z'; c++) {
    word2 = string(span2.len, c);  // Fill with the same letter
    
    Point intersection;
    if (grid.SpansIntersect(span1, span2, intersection)) {
      // Calculate position within each span
      int pos1 = span1.vert ? 
                  intersection.row - span1.point.row : 
                  intersection.col - span1.point.col;
      
      int pos2 = span2.vert ? 
                  intersection.row - span2.point.row : 
                  intersection.col - span2.point.col;
      
      // Make sure the intersection letter matches
      word2[pos2] = word1[pos1];
      break;
    }
  }
  
  cout << "Placing word '" << word2 << "' at " << span2 << endl;
  success = grid.PlaceWord(span2, word2);
  
  cout << "Placement " << (success ? "successful" : "failed") << endl;
  grid.Print();
  
  // Remove the first word
  cout << "Removing word at " << span1 << endl;
  success = grid.RemoveWord(span1);
  
  cout << "Removal " << (success ? "successful" : "failed") << endl;
  grid.Print();
}
```

This test function:
1. Places a word in the first span
2. Places a word in the second span, ensuring it's compatible at the intersection
3. Removes the first word, demonstrating how intersections are preserved

#### Integrating with the Solver

Our improved word placement methods integrate well with the Solver class from Chapter 16:

```cpp
bool Solver::SolveRecursive(const Patterns& patterns, size_t index) {
  // Base case: we've filled all patterns
  if (index >= patterns.size()) {
    return true;  // Success!
  }
  
  // Get the current pattern to fill
  const Pattern& current = patterns[index];
  
  // If the pattern is already filled (span has a word), move to the next one
  if (grid_.IsSpanFilled(current.span)) {
    return SolveRecursive(patterns, index + 1);
  }
  
  // Find candidate words for this pattern
  vector<string> candidates = FindCandidateWords(current);
  
  // Try each candidate
  for (const string& word : candidates) {
    // Place the word in the grid
    bool success = grid_.PlaceWord(current.span, word);
    
    if (success) {
      // Recursively try to solve the rest of the grid
      if (SolveRecursive(patterns, index + 1)) {
        return true;  // Success!
      }
      
      // If we get here, this word didn't lead to a solution.
      // Backtrack by removing the word from the grid.
      grid_.RemoveWord(current.span);
    }
  }
  
  // If we tried all candidates and none worked, this is a dead end
  return false;
}
```

The Solver can now use our improved methods to place and remove words during the solving process.

#### Visualizing Word Placements

To better understand the state of the grid, let's add a method to visualize word placements:

```cpp
void Grid::PrintWithWordHighlights() const {
  // Create a grid of cell highlights
  vector<vector<char>> highlight(lines.size(), vector<char>(lines[0].size(), ' '));
  
  // Mark each placed word with a unique label
  for (size_t i = 0; i < placed_words.size(); i++) {
    const auto& entry = placed_words[i];
    const Span& s = entry.first;
    
    // Use letters A-Z, then recycle
    char label = 'A' + (i % 26);
    
    Point p = s.point;
    for (int j = 0; j < s.len; j++) {
      highlight[p.row][p.col] = label;
      
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
  }
  
  // Print the grid with highlights
  for (size_t r = 0; r < lines.size(); r++) {
    // Print the grid line
    cout << lines[r] << "   ";
    
    // Print the highlight line
    for (size_t c = 0; c < lines[r].size(); c++) {
      cout << highlight[r][c];
    }
    
    cout << endl;
  }
  
  // Print a legend
  cout << endl << "Words placed:" << endl;
  for (size_t i = 0; i < placed_words.size(); i++) {
    char label = 'A' + (i % 26);
    cout << "  " << label << ": " << placed_words[i].second 
         << " at " << placed_words[i].first << endl;
  }
}
```

This method:
1. Creates a grid of highlights using letters to identify different words
2. Prints the grid with these highlights
3. Provides a legend mapping highlights to words

#### Putting It All Together

Now let's combine all these enhancements into our Grid class:

```cpp
#include <assert.h>
#include <algorithm>
#include <fstream>
#include <iostream>
#include <string>
#include <unordered_map>
#include <unordered_set>
#include <vector>

using namespace std;

// ... Point and Span structures from previous chapters ...

// Add PointHash for unordered containers
struct PointHash {
  size_t operator()(const Point& p) const {
    return p.row * 10000 + p.col;
  }
};

struct PointEqual {
  bool operator()(const Point& a, const Point& b) const {
    return a.row == b.row && a.col == b.col;
  }
};

// ... Pattern structure from previous chapters ...

struct Grid {
  // ... existing methods from previous chapters ...
  
  // Helper method to get a reference to a cell
  char& CellAt(const Point& p) {
    assert(in_bounds(p));
    return lines[p.row][p.col];
  }
  
  // Check if a word can be placed in a span
  bool IsWordPlaceable(const Span& s, const string& word) const {
    if (word.length() != s.len) {
      return false;  // Word length doesn't match span length
    }
    
    string current = GetSpanContent(s);
    
    for (size_t i = 0; i < current.length(); i++) {
      char existing = current[i];
      if (existing != '-' && existing != word[i]) {
        return false;  // Conflict with existing letter
      }
    }
    
    return true;
  }
  
  // Place a word in the grid
  bool PlaceWord(const Span& s, const string& word) {
    // Validate inputs
    if (word.length() != s.len) {
      return false;  // Word length doesn't match span length
    }
    
    // Check if the word fits the current grid state
    if (!IsWordPlaceable(s, word)) {
      return false;  // Word doesn't fit
    }
    
    // Place the word
    Point p = s.point;
    for (size_t i = 0; i < word.length(); i++) {
      CellAt(p) = word[i];
      
      // Move to next position
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
    
    // Track this word placement
    placed_words.push_back(make_pair(s, word));
    
    return true;
  }
  
  // Remove a word from the grid
  bool RemoveWord(const Span& s) {
    // Find this span in our placed_words list
    auto it = find_if(placed_words.begin(), placed_words.end(),
      [&s](const pair<Span, string>& entry) {
        const Span& placed_span = entry.first;
        return placed_span.point.row == s.point.row &&
               placed_span.point.col == s.point.col &&
               placed_span.len == s.len &&
               placed_span.vert == s.vert;
      });
    
    // If we didn't find it, nothing to remove
    if (it == placed_words.end()) {
      return false;
    }
    
    // Get the word that was placed
    string word = it->second;
    
    // Remove from our tracking
    placed_words.erase(it);
    
    // Build a set of points that are part of intersections
    unordered_set<Point, PointHash, PointEqual> intersection_points;
    
    // Find all intersection points
    for (const auto& entry : placed_words) {
      const Span& other_span = entry.first;
      
      // Skip if same orientation
      if (other_span.vert == s.vert) {
        continue;
      }
      
      // Check for intersection
      Point intersection;
      if (SpansIntersect(s, other_span, intersection)) {
        intersection_points.insert(intersection);
      }
    }
    
    // Remove the word, preserving intersections
    Point p = s.point;
    for (size_t i = 0; i < s.len; i++) {
      // Check if this point is part of an intersection
      if (intersection_points.find(p) == intersection_points.end()) {
        // Not an intersection, clear the cell
        CellAt(p) = '-';
      }
      
      // Move to next position
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
    
    return true;
  }
  
  // Get all currently placed words
  vector<pair<Span, string>> GetPlacedWords() const {
    return placed_words;
  }
  
  // Check if a span already has a word placed
  bool IsSpanFilled(const Span& s) const {
    for (const auto& entry : placed_words) {
      const Span& placed_span = entry.first;
      if (placed_span.point.row == s.point.row &&
          placed_span.point.col == s.point.col &&
          placed_span.len == s.len &&
          placed_span.vert == s.vert) {
        return true;
      }
    }
    return false;
  }
  
  // Get the last placed word
  pair<Span, string> GetLastPlacedWord() const {
    assert(!placed_words.empty());
    return placed_words.back();
  }
  
  // Clear all placed words and reset the grid
  void ClearAllWords() {
    placed_words.clear();
    
    // Reset all cells to empty
    for (size_t r = 0; r < lines.size(); r++) {
      for (size_t c = 0; c < lines[r].size(); c++) {
        if (lines[r][c] != '.') {  // Don't clear blocks
          lines[r][c] = '-';
        }
      }
    }
  }
  
  // Print the grid with word highlights
  void PrintWithWordHighlights() const {
    // Create a grid of cell highlights
    vector<vector<char>> highlight(lines.size(), vector<char>(lines[0].size(), ' '));
    
    // Mark each placed word with a unique label
    for (size_t i = 0; i < placed_words.size(); i++) {
      const auto& entry = placed_words[i];
      const Span& s = entry.first;
      
      // Use letters A-Z, then recycle
      char label = 'A' + (i % 26);
      
      Point p = s.point;
      for (int j = 0; j < s.len; j++) {
        highlight[p.row][p.col] = label;
        
        if (s.vert) {
          p.row++;
        } else {
          p.col++;
        }
      }
    }
    
    // Print the grid with highlights
    for (size_t r = 0; r < lines.size(); r++) {
      // Print the grid line
      cout << lines[r] << "   ";
      
      // Print the highlight line
      for (size_t c = 0; c < lines[r].size(); c++) {
        cout << highlight[r][c];
      }
      
      cout << endl;
    }
    
    // Print a legend
    cout << endl << "Words placed:" << endl;
    for (size_t i = 0; i < placed_words.size(); i++) {
      char label = 'A' + (i % 26);
      cout << "  " << label << ": " << placed_words[i].second 
           << " at " << placed_words[i].first << endl;
    }
  }
  
  // ... existing members ...
  vector<pair<Span, string>> placed_words;  // Track placed words
};

// Test function to demonstrate word placement
void TestWordPlacement(Grid& grid) {
  // ... implementation from earlier ...
}

int main() {
  // Load a grid
  Grid grid("Crossword Puzzle");
  grid.LoadFromFile("test.txt");
  
  // Test word placement
  TestWordPlacement(grid);
  
  // Print with highlights
  grid.PrintWithWordHighlights();
  
  return 0;
}
```

#### Conclusion

In this chapter, we've significantly enhanced our Grid class with robust methods for placing and removing words:

1. **Improved Word Placement**: We implemented a more robust `PlaceWord` method that checks compatibility and tracks placements.

2. **Intelligent Word Removal**: We created a `RemoveWord` method that preserves intersections with other words.

3. **Word Placement Tracking**: We added a `placed_words` list to keep track of all words placed in the grid.

4. **Visualization**: We implemented a method to visualize word placements with highlights.

These enhancements provide a solid foundation for our crossword puzzle solver, allowing it to efficiently place and remove words during the solving process while maintaining grid consistency. In the next chapter, "Preventing Duplicates," we'll build on this foundation to ensure that our solver doesn't place the same word multiple times in the grid.

#### Practice Exercises

1. Enhance the `PlaceWord` method to return information about why a word couldn't be placed (e.g., conflicts with existing letters).
2. Implement a method to check if two spans overlap (not just intersect) and handle this case in word placement.
3. Add functionality to undo/redo word placements with a history stack.
4. Create a method to save the current grid state to a file, including information about placed words.
5. Implement a method to find all possible word placements for a given span based on the current grid state and a word library.

### 18. Preventing Duplicates
[https://youtu.be/AIjy3TcH924](https://youtu.be/AIjy3TcH924)
### 18. Preventing Duplicates

In this chapter, we'll tackle an important aspect of crossword puzzle construction: preventing duplicate words from appearing in the same puzzle. This is a common rule in professional crossword puzzles and will improve the quality of our generated solutions.

#### The Duplicate Word Problem

In our current implementation, there's nothing preventing the same word from being used multiple times in the grid. For example, the word "CAT" could potentially appear in both a horizontal and a vertical span. This is generally considered poor form in crossword puzzle design.

To address this, we need to:
1. Track which words have already been placed in the grid
2. Prevent the placement of words that are already used
3. Update our solver to consider this constraint

#### Enhancing the Grid Class

Let's start by enhancing our Grid class to track and prevent duplicate words:

```cpp
struct Grid {
  // ... existing code from previous chapters ...
  
  // New data structure to track used words
  unordered_set<string> used_words;
  
  // Check if a word is already used in the grid
  bool IsWordUsed(const string& word) const {
    return used_words.find(word) != used_words.end();
  }
  
  // Enhanced PlaceWord that prevents duplicates
  bool PlaceWord(const Span& s, const string& word, bool allow_duplicates = false) {
    // Check for duplicates
    if (!allow_duplicates && IsWordUsed(word)) {
      return false;  // Word is already used elsewhere
    }
    
    // Existing validation
    if (word.length() != s.len) {
      return false;  // Word length doesn't match span length
    }
    
    // Check if the word fits the current grid state
    if (!IsWordPlaceable(s, word)) {
      return false;  // Word doesn't fit
    }
    
    // Place the word
    Point p = s.point;
    for (size_t i = 0; i < word.length(); i++) {
      CellAt(p) = word[i];
      
      // Move to next position
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
    
    // Track this word placement
    placed_words.push_back(make_pair(s, word));
    used_words.insert(word);
    
    return true;
  }
  
  // Enhanced RemoveWord that updates used_words
  bool RemoveWord(const Span& s) {
    // Find this span in our placed_words list
    auto it = find_if(placed_words.begin(), placed_words.end(),
      [&s](const pair<Span, string>& entry) {
        const Span& placed_span = entry.first;
        return placed_span.point.row == s.point.row &&
               placed_span.point.col == s.point.col &&
               placed_span.len == s.len &&
               placed_span.vert == s.vert;
      });
    
    // If we didn't find it, nothing to remove
    if (it == placed_words.end()) {
      return false;
    }
    
    // Get the word that was placed
    string word = it->second;
    
    // Remove from our tracking
    placed_words.erase(it);
    
    // Check if the word appears elsewhere before removing from used_words
    bool word_used_elsewhere = false;
    for (const auto& entry : placed_words) {
      if (entry.second == word) {
        word_used_elsewhere = true;
        break;
      }
    }
    
    if (!word_used_elsewhere) {
      used_words.erase(word);
    }
    
    // Rest of the removal logic (preserving intersections)
    // ... existing code from Chapter 17 ...
    
    return true;
  }
  
  // Reset word usage tracking
  void ClearAllWords() {
    placed_words.clear();
    used_words.clear();
    
    // Reset all cells to empty
    for (size_t r = 0; r < lines.size(); r++) {
      for (size_t c = 0; c < lines[r].size(); c++) {
        if (lines[r][c] != '.') {  // Don't clear blocks
          lines[r][c] = '-';
        }
      }
    }
  }
};
```

The key enhancements are:
1. A new `used_words` set to track words that have been placed
2. An `IsWordUsed` method to check if a word is already in use
3. An enhanced `PlaceWord` method that checks for duplicates
4. An enhanced `RemoveWord` method that updates the `used_words` set
5. An optional `allow_duplicates` parameter that can be used to override the duplicate check

#### Word Frequency and Duplicate Prevention

In crossword construction, not all duplicates are equally problematic. Common short words like "THE" or "AND" might be more acceptable to duplicate than longer, more distinctive words. Let's add some nuance to our duplicate prevention:

```cpp
struct Grid {
  // ... existing code ...
  
  // Enhanced duplicate prevention with word length consideration
  bool ShouldAllowDuplicate(const string& word) const {
    // Never allow duplicates of words longer than 3 characters
    if (word.length() > 3) {
      return false;
    }
    
    // For 3-letter words, check how many times it's already used
    if (word.length() == 3) {
      int usage_count = 0;
      for (const auto& entry : placed_words) {
        if (entry.second == word) {
          usage_count++;
        }
      }
      
      // Allow at most one duplicate for 3-letter words
      return usage_count < 1;
    }
    
    // For 2-letter words, be even more permissive
    if (word.length() == 2) {
      int usage_count = 0;
      for (const auto& entry : placed_words) {
        if (entry.second == word) {
          usage_count++;
        }
      }
      
      // Allow at most two duplicates for 2-letter words
      return usage_count < 2;
    }
    
    // Default - don't allow duplicates
    return false;
  }
  
  // Further enhanced PlaceWord
  bool PlaceWord(const Span& s, const string& word, bool ignore_duplicate_rules = false) {
    // Check for duplicates
    if (!ignore_duplicate_rules && IsWordUsed(word)) {
      // Apply more nuanced rules
      if (!ShouldAllowDuplicate(word)) {
        return false;  // Reject this duplicate
      }
    }
    
    // Rest of the placement logic
    // ... existing code ...
  }
};
```

This more nuanced approach allows for limited duplication of short, common words while preventing duplication of longer, more distinctive words.

#### Implementing Duplicate Prevention in the Solver

Now let's update our Solver class to work with the enhanced Grid:

```cpp
class Solver {
public:
  // ... existing code ...
  
  // Add options for duplicate prevention
  void SetAllowDuplicates(bool allow) {
    allow_duplicates_ = allow;
  }
  
private:
  // ... existing code ...
  
  bool SolveRecursive(const Patterns& patterns, size_t index) {
    // ... existing code ...
    
    for (const string& word : candidates) {
      // Place the word in the grid, respecting duplicate prevention
      bool success = grid_.PlaceWord(current.span, word, allow_duplicates_);
      
      if (success) {
        // ... rest of solving logic ...
      }
    }
    
    // ... existing code ...
  }
  
  // Configuration options
  bool allow_duplicates_ = false;
};
```

This update allows the solver to respect the duplicate prevention rules, with an option to override them if needed.

#### Finding Candidate Words with Duplicate Prevention

We also need to update the `FindCandidateWords` method to filter out words that are already used:

```cpp
vector<string> Solver::FindCandidateWords(const Pattern& pattern) {
  vector<string> candidates;
  
  // Find all words in the library that match this pattern
  auto matches = lib_.FindMatchingWords(pattern.pattern);
  
  for (const Word* word : matches) {
    // Check for duplicates if required
    if (!allow_duplicates_ && grid_.IsWordUsed(word->word)) {
      // Apply nuanced rules
      if (!grid_.ShouldAllowDuplicate(word->word)) {
        continue;  // Skip this duplicate
      }
    }
    
    // Verify that the word fits the pattern
    if (grid_.IsWordPlaceable(pattern.span, word->word)) {
      candidates.push_back(word->word);
    }
  }
  
  return candidates;
}
```

This ensures that duplicate words are filtered out before they're even considered for placement.

#### Word Quality and Scoring

Another way to improve our crossword solutions is to prefer more common or "better" words. Let's add a simple scoring system:

```cpp
struct Word {
  // ... existing code ...
  
  // Add a quality score (higher is better)
  int quality = 1;
};

// Enhanced candidate finding with word scoring
vector<string> Solver::FindCandidateWords(const Pattern& pattern) {
  vector<pair<string, int>> scored_candidates;
  
  // Find all words in the library that match this pattern
  auto matches = lib_.FindMatchingWords(pattern.pattern);
  
  for (const Word* word : matches) {
    // Check for duplicates
    // ... existing duplicate checking ...
    
    // Verify that the word fits the pattern
    if (grid_.IsWordPlaceable(pattern.span, word->word)) {
      scored_candidates.push_back(make_pair(word->word, word->quality));
    }
  }
  
  // Sort by quality (higher first)
  sort(scored_candidates.begin(), scored_candidates.end(),
       [](const pair<string, int>& a, const pair<string, int>& b) {
         return a.second > b.second;
       });
  
  // Extract just the words
  vector<string> candidates;
  for (const auto& pair : scored_candidates) {
    candidates.push_back(pair.first);
  }
  
  return candidates;
}
```

This modification sorts candidate words by quality, attempting to use better words first.

#### Tracking and Analyzing Duplicate Prevention

To understand how duplicate prevention affects our solving process, let's add some tracking:

```cpp
class Solver {
public:
  // ... existing code ...
  
  // Statistics about duplicate prevention
  struct DuplicateStats {
    int total_attempts = 0;
    int duplicates_prevented = 0;
    int duplicates_allowed = 0;
    
    void Print() const {
      cout << "Duplicate prevention statistics:" << endl;
      cout << "  Total word placement attempts: " << total_attempts << endl;
      cout << "  Duplicates prevented: " << duplicates_prevented << endl;
      cout << "  Duplicates allowed: " << duplicates_allowed << endl;
    }
  };
  
  // Get the current duplicate stats
  const DuplicateStats& GetDuplicateStats() const {
    return dup_stats_;
  }
  
private:
  // ... existing code ...
  
  bool SolveRecursive(const Patterns& patterns, size_t index) {
    // ... existing code ...
    
    for (const string& word : candidates) {
      dup_stats_.total_attempts++;
      
      // Check for duplicates before placement
      bool is_duplicate = grid_.IsWordUsed(word);
      bool should_place = true;
      
      if (is_duplicate) {
        if (allow_duplicates_ || grid_.ShouldAllowDuplicate(word)) {
          dup_stats_.duplicates_allowed++;
        } else {
          dup_stats_.duplicates_prevented++;
          should_place = false;
        }
      }
      
      if (should_place) {
        bool success = grid_.PlaceWord(current.span, word, allow_duplicates_);
        
        if (success) {
          // ... rest of solving logic ...
        }
      }
    }
    
    // ... existing code ...
  }
  
  // Statistics tracking
  DuplicateStats dup_stats_;
};
```

This tracking allows us to see how many duplicates are being prevented and how many are being allowed based on our rules.

#### Testing Duplicate Prevention

Let's create a test function to demonstrate our duplicate prevention:

```cpp
void TestDuplicatePrevention(Grid& grid, Library& lib) {
  // Clear the grid
  grid.ClearAllWords();
  
  // Fill spans if needed
  if (grid.spans.empty()) {
    grid.FillSpans();
  }
  
  cout << "Initial grid:" << endl;
  grid.Print();
  
  // Find some spans
  if (grid.spans.size() < 2) {
    cout << "Not enough spans for testing" << endl;
    return;
  }
  
  // Find a word from the library
  string test_word;
  for (int i = 0; i < 1000; i++) {  // Try up to 1000 words
    string word = lib.GetWord(i);
    
    // Find a span with matching length
    for (const Span& s : grid.spans) {
      if (s.len == word.length() && grid.IsWordPlaceable(s, word)) {
        test_word = word;
        break;
      }
    }
    
    if (!test_word.empty()) break;
  }
  
  if (test_word.empty()) {
    cout << "Couldn't find a suitable test word" << endl;
    return;
  }
  
  // Find spans where this word could be placed
  vector<Span> matching_spans;
  for (const Span& s : grid.spans) {
    if (s.len == test_word.length() && grid.IsWordPlaceable(s, test_word)) {
      matching_spans.push_back(s);
    }
  }
  
  if (matching_spans.size() < 2) {
    cout << "Not enough matching spans for testing" << endl;
    return;
  }
  
  // Try placing the word twice
  cout << "Placing word '" << test_word << "' at " << matching_spans[0] << endl;
  bool success1 = grid.PlaceWord(matching_spans[0], test_word);
  cout << "First placement " << (success1 ? "successful" : "failed") << endl;
  
  cout << "Trying to place the same word at " << matching_spans[1] << endl;
  bool success2 = grid.PlaceWord(matching_spans[1], test_word);
  cout << "Second placement " << (success2 ? "successful" : "failed") << endl;
  
  grid.Print();
  
  // Try with override
  if (!success2) {
    cout << "Trying again with duplicate override:" << endl;
    bool success3 = grid.PlaceWord(matching_spans[1], test_word, true);
    cout << "Placement with override " << (success3 ? "successful" : "failed") << endl;
    grid.Print();
  }
}
```

This test:
1. Finds a suitable word from the library
2. Attempts to place it in two different spans
3. Demonstrates how duplicate prevention blocks the second placement
4. Shows how the override flag can be used to bypass the restriction

#### Putting It All Together

Now let's combine all these enhancements into our program:

```cpp
#include <assert.h>
#include <algorithm>
#include <fstream>
#include <iostream>
#include <string>
#include <unordered_map>
#include <unordered_set>
#include <vector>

using namespace std;

// ... Point, Span, Pattern structures from previous chapters ...

// Enhanced Word structure with quality score
struct Word {
  Word() {}
  Word(string s, int q = 1) : word(s), quality(q) {}
  int len() const { return word.length(); }
  
  string word;
  int quality;  // Higher is better
};

// ... Library class from previous chapters ...

// Enhanced Grid with duplicate prevention
struct Grid {
  // ... existing code from previous chapters ...
  
  // New data structure to track used words
  unordered_set<string> used_words;
  
  // Check if a word is already used in the grid
  bool IsWordUsed(const string& word) const {
    return used_words.find(word) != used_words.end();
  }
  
  // Enhanced duplicate prevention with word length consideration
  bool ShouldAllowDuplicate(const string& word) const {
    // Never allow duplicates of words longer than 3 characters
    if (word.length() > 3) {
      return false;
    }
    
    // For 3-letter words, check how many times it's already used
    if (word.length() == 3) {
      int usage_count = 0;
      for (const auto& entry : placed_words) {
        if (entry.second == word) {
          usage_count++;
        }
      }
      
      // Allow at most one duplicate for 3-letter words
      return usage_count < 1;
    }
    
    // For 2-letter words, be even more permissive
    if (word.length() == 2) {
      int usage_count = 0;
      for (const auto& entry : placed_words) {
        if (entry.second == word) {
          usage_count++;
        }
      }
      
      // Allow at most two duplicates for 2-letter words
      return usage_count < 2;
    }
    
    // Default - don't allow duplicates
    return false;
  }
  
  // Enhanced PlaceWord that prevents duplicates
  bool PlaceWord(const Span& s, const string& word, bool ignore_duplicate_rules = false) {
    // Check for duplicates
    if (!ignore_duplicate_rules && IsWordUsed(word)) {
      // Apply more nuanced rules
      if (!ShouldAllowDuplicate(word)) {
        return false;  // Reject this duplicate
      }
    }
    
    // Existing validation
    if (word.length() != s.len) {
      return false;  // Word length doesn't match span length
    }
    
    // Check if the word fits the current grid state
    if (!IsWordPlaceable(s, word)) {
      return false;  // Word doesn't fit
    }
    
    // Place the word
    Point p = s.point;
    for (size_t i = 0; i < word.length(); i++) {
      CellAt(p) = word[i];
      
      // Move to next position
      if (s.vert) {
        p.row++;
      } else {
        p.col++;
      }
    }
    
    // Track this word placement
    placed_words.push_back(make_pair(s, word));
    used_words.insert(word);
    
    return true;
  }
  
  // Enhanced RemoveWord that updates used_words
  bool RemoveWord(const Span& s) {
    // ... find and remove the word (existing code) ...
    
    // Check if the word appears elsewhere before removing from used_words
    bool word_used_elsewhere = false;
    for (const auto& entry : placed_words) {
      if (entry.second == word) {
        word_used_elsewhere = true;
        break;
      }
    }
    
    if (!word_used_elsewhere) {
      used_words.erase(word);
    }
    
    // ... rest of the removal logic ...
  }
  
  // Reset word usage tracking
  void ClearAllWords() {
    placed_words.clear();
    used_words.clear();
    
    // Reset all cells to empty
    for (size_t r = 0; r < lines.size(); r++) {
      for (size_t c = 0; c < lines[r].size(); c++) {
        if (lines[r][c] != '.') {  // Don't clear blocks
          lines[r][c] = '-';
        }
      }
    }
  }
};

// Enhanced Solver with duplicate prevention
class Solver {
public:
  Solver(Grid& g, Library& l) : grid_(g), lib_(l), allow_duplicates_(false) {}
  
  // Add options for duplicate prevention
  void SetAllowDuplicates(bool allow) {
    allow_duplicates_ = allow;
  }
  
  bool Solve() {
    // Make sure spans are calculated
    if (grid_.spans.empty()) {
      grid_.FillSpans();
    }
    
    // Get patterns sorted by constraint
    Patterns patterns = grid_.GetSortedPatterns();
    
    cout << "Starting to solve with " << patterns.size() << " patterns" << endl;
    
    // Reset statistics
    dup_stats_ = DuplicateStats();
    
    // Start the recursive solving process
    bool result = SolveRecursive(patterns, 0);
    
    // Print stats
    dup_stats_.Print();
    
    return result;
  }
  
  // Statistics about duplicate prevention
  struct DuplicateStats {
    int total_attempts = 0;
    int duplicates_prevented = 0;
    int duplicates_allowed = 0;
    
    void Print() const {
      cout << "Duplicate prevention statistics:" << endl;
      cout << "  Total word placement attempts: " << total_attempts << endl;
      cout << "  Duplicates prevented: " << duplicates_prevented << endl;
      cout << "  Duplicates allowed: " << duplicates_allowed << endl;
    }
  };
  
  // Get the current duplicate stats
  const DuplicateStats& GetDuplicateStats() const {
    return dup_stats_;
  }
  
private:
  bool SolveRecursive(const Patterns& patterns, size_t index) {
    // Base case: we've filled all patterns
    if (index >= patterns.size()) {
      return true;  // Success!
    }
    
    // Get the current pattern to fill
    const Pattern& current = patterns[index];
    
    cout << "Solving pattern " << index << ": " << current.pattern << endl;
    
    // If the pattern is already filled, move to the next one
    if (current.IsFilled()) {
      cout << "Pattern already filled, moving to next" << endl;
      return SolveRecursive(patterns, index + 1);
    }
    
    // Find candidate words for this pattern
    vector<string> candidates = FindCandidateWords(current);
    
    cout << "Found " << candidates.size() << " candidates" << endl;
    
    // Try each candidate
    for (const string& word : candidates) {
      dup_stats_.total_attempts++;
      
      // Check for duplicates before placement
      bool is_duplicate = grid_.IsWordUsed(word);
      bool should_place = true;
      
      if (is_duplicate) {
        if (allow_duplicates_ || grid_.ShouldAllowDuplicate(word)) {
          dup_stats_.duplicates_allowed++;
        } else {
          dup_stats_.duplicates_prevented++;
          should_place = false;
        }
      }
      
      if (should_place) {
        cout << "Trying word: " << word << endl;
        
        // Place the word in the grid
        bool success = grid_.PlaceWord(current.span, word, allow_duplicates_);
        
        if (success) {
          // Recursively try to solve the rest of the grid
          if (SolveRecursive(patterns, index + 1)) {
            return true;  // Success!
          }
          
          cout << "Backtracking from word: " << word << endl;
          // If we get here, this word didn't lead to a solution.
          // Backtrack by removing the word from the grid.
          grid_.RemoveWord(current.span);
        }
      }
    }
    
    cout << "No solution found for pattern " << index << endl;
    // If we tried all candidates and none worked, this is a dead end
    return false;
  }
  
  vector<string> FindCandidateWords(const Pattern& pattern) {
    vector<pair<string, int>> scored_candidates;
    
    // Find all words in the library that match this pattern
    auto matches = lib_.FindMatchingWords(pattern.pattern);
    
    for (const Word* word : matches) {
      // Check for duplicates
      if (!allow_duplicates_ && grid_.IsWordUsed(word->word)) {
        // Apply nuanced rules
        if (!grid_.ShouldAllowDuplicate(word->word)) {
          continue;  // Skip this duplicate
        }
      }
      
      // Verify that the word fits the pattern
      if (grid_.IsWordPlaceable(pattern.span, word->word)) {
        scored_candidates.push_back(make_pair(word->word, word->quality));
      }
    }
    
    // Sort by quality (higher first)
    sort(scored_candidates.begin(), scored_candidates.end(),
         [](const pair<string, int>& a, const pair<string, int>& b) {
           return a.second > b.second;
         });
    
    // Extract just the words
    vector<string> candidates;
    for (const auto& pair : scored_candidates) {
      candidates.push_back(pair.first);
    }
    
    return candidates;
  }
  
  Grid& grid_;
  Library& lib_;
  bool allow_duplicates_;
  DuplicateStats dup_stats_;
};

// Test function for duplicate prevention
void TestDuplicatePrevention(Grid& grid, Library& lib) {
  // ... implementation from earlier ...
}

int main() {
  // Load a library of words
  Library lib;
  lib.ReadFromFile("top_12000.txt");
  
  // Create and load a grid
  Grid grid("Crossword Puzzle");
  grid.LoadFromFile("test.txt");
  
  // Test duplicate prevention
  TestDuplicatePrevention(grid, lib);
  
  // Create a solver with duplicate prevention
  Solver solver(grid, lib);
  solver.SetAllowDuplicates(false);  // Prevent duplicates (default)
  
  // Solve the grid
  grid.ClearAllWords();
  cout << "\nSolving with duplicate prevention:" << endl;
  bool success = solver.Solve();
  
  // Print the result
  cout << endl << "Solution " << (success ? "found" : "not found") << ":" << endl;
  grid.Print();
  
  // Try again without duplicate prevention if the first attempt failed
  if (!success) {
    grid.ClearAllWords();
    solver.SetAllowDuplicates(true);
    cout << "\nSolving without duplicate prevention:" << endl;
    success = solver.Solve();
    
    cout << endl << "Solution " << (success ? "found" : "not found") << ":" << endl;
    grid.Print();
  }
  
  return 0;
}
```

#### Conclusion

In this chapter, we've enhanced our crossword puzzle solver to prevent duplicate words from appearing in the same puzzle:

1. **Duplicate Tracking**: We added the ability to track which words have been placed in the grid.

2. **Nuanced Rules**: We implemented more sophisticated rules that allow limited duplication of short, common words.

3. **Word Quality**: We added a quality score to words to prefer better words in our solutions.

4. **Statistics Tracking**: We added the ability to track and analyze how duplicate prevention affects our solving process.

These enhancements improve the quality of our crossword puzzle solutions, making them more aligned with professional crossword construction standards.

In the next chapters, we'll continue to refine our solver with additional optimizations and features, but the duplicate prevention capability we've implemented here is a significant step toward generating high-quality crossword puzzles.

#### Practice Exercises

1. Enhance the duplicate prevention system to consider word similarity, not just exact matches (e.g., plurals or different forms of the same root word).
2. Implement a system to assign quality scores to words based on their frequency in English text or another metric.
3. Add support for "theme words" that must be included in the puzzle, potentially overriding duplicate rules.
4. Create a visualization that highlights duplicate words in the grid.
5. Implement a more sophisticated placement strategy that tries to maximize the average quality of words in the puzzle.

### 19. Speeding up the library with partial character hash
### 19. Speeding up the library with partial character hash

In this chapter, we'll focus on optimizing our word lookup mechanism with a technique called "partial character hashing." This approach significantly improves the performance of our crossword solver, especially when dealing with patterns containing many wildcards or when working with larger word libraries.

#### The Performance Challenge

In our current implementation, we've already made significant optimizations using the pattern hash system from Chapter 12. However, this approach still has limitations:

1. **Exponential Pattern Growth**: For each word, we generate 2^n patterns (where n is the word length). This quickly becomes inefficient for longer words.

2. **Wildcard-Heavy Patterns**: Patterns with many wildcards (like "-----") match a large number of words, resulting in the need to scan through many candidates.

3. **Large Dictionaries**: As our dictionary grows, these inefficiencies become more pronounced.

Let's implement a more efficient approach using partial character hashing.

#### The Concept of Partial Character Hashing

The key insight behind partial character hashing is to create a data structure that enables us to quickly find words where specific positions contain specific characters. Instead of generating all possible patterns for each word, we'll index the words based on their characters and positions.

For example, with the word "DOG":
- Position 0 contains 'D'
- Position 1 contains 'O'
- Position 2 contains 'G'

We'll create an index that allows us to quickly find all words where position 0 contains 'D', or position 2 contains 'G', etc. When we encounter a pattern like "D--", we can find all words of length 3 where position 0 contains 'D'.

#### Implementing the Partial Character Hash

Let's start by defining a new structure to manage our partial character hash:

```cpp
class PartialCharacterHash {
public:
  PartialCharacterHash() {}
  
  // Add a word to the hash
  void AddWord(Word* word) {
    const string& str = word->word;
    int len = str.length();
    
    // Store the word in the length-based index
    length_index_[len].push_back(word);
    
    // Store word in character-position indices
    for (int i = 0; i < len; i++) {
      char c = str[i];
      char_pos_index_[make_pair(i, c)].push_back(word);
    }
  }
  
  // Find words matching a pattern
  Words FindMatches(const string& pattern) const {
    Words result;
    
    // First, check if we have an exact pattern match
    auto it = pattern_index_.find(pattern);
    if (it != pattern_index_.end()) {
      return it->second;
    }
    
    // If not, use the partial character hash
    int len = pattern.length();
    
    // Get all words of the right length
    auto len_it = length_index_.find(len);
    if (len_it == length_index_.end()) {
      return result;  // No words of this length
    }
    
    // Find the most restrictive position (one with a specified character)
    int best_pos = -1;
    char best_char = 0;
    int best_count = INT_MAX;
    
    for (int i = 0; i < len; i++) {
      if (pattern[i] != '-') {
        auto count_it = char_pos_counts_.find(make_pair(i, pattern[i]));
        int count = (count_it != char_pos_counts_.end()) ? count_it->second : 0;
        
        if (count < best_count) {
          best_pos = i;
          best_char = pattern[i];
          best_count = count;
        }
      }
    }
    
    // If we found a restrictive position, use it to filter
    if (best_pos >= 0) {
      auto char_pos_it = char_pos_index_.find(make_pair(best_pos, best_char));
      if (char_pos_it != char_pos_index_.end()) {
        // Check each candidate word against the full pattern
        for (Word* word : char_pos_it->second) {
          if (MatchesPattern(word->word, pattern)) {
            result.push_back(word);
          }
        }
      }
    } else {
      // No specified characters, check all words of the right length
      for (Word* word : len_it->second) {
        if (MatchesPattern(word->word, pattern)) {
          result.push_back(word);
        }
      }
    }
    
    // Cache this result for future lookups
    pattern_index_[pattern] = result;
    
    return result;
  }
  
  // Build counts of character-position pairs
  void BuildCounts() {
    for (const auto& entry : char_pos_index_) {
      char_pos_counts_[entry.first] = entry.second.size();
    }
  }
  
private:
  // Check if a word matches a pattern
  bool MatchesPattern(const string& word, const string& pattern) const {
    if (word.length() != pattern.length()) {
      return false;
    }
    
    for (size_t i = 0; i < pattern.length(); i++) {
      if (pattern[i] != '-' && pattern[i] != word[i]) {
        return false;
      }
    }
    
    return true;
  }
  
  // Length-based index
  unordered_map<int, Words> length_index_;
  
  // Character-position index
  unordered_map<pair<int, char>, Words, PairHash> char_pos_index_;
  
  // Character-position counts for determining most restrictive positions
  unordered_map<pair<int, char>, int, PairHash> char_pos_counts_;
  
  // Cache for previously computed pattern matches
  mutable unordered_map<string, Words> pattern_index_;
  
  // Helper for hashing pairs
  struct PairHash {
    size_t operator()(const pair<int, char>& p) const {
      return p.first * 256 + p.second;
    }
  };
};
```

This implementation provides several key optimizations:
1. **Length-Based Filtering**: We quickly filter by word length
2. **Restrictive Position Selection**: We choose the most restrictive character position to minimize candidates
3. **Result Caching**: We cache results for previously seen patterns
4. **Incremental Filtering**: We filter first by the most restrictive character, then check the full pattern

#### Integrating with the Library Class

Now let's integrate our partial character hash with the Library class:

```cpp
class Library {
public:
  Library() {}
  ~Library() {
    for (Word* w : words_) {
      delete w;
    }
  }
  
  // Find words matching a pattern
  Words FindMatchingWords(const string& pattern) const {
    // Use the new partial character hash for lookups
    return partial_hash_.FindMatches(pattern);
  }
  
  // Read words from a file
  void ReadFromFile(string filename) {
    ifstream f;
    f.open(filename);
    while (f.is_open() && !f.eof()) {
      string line;
      getline(f, line);
      if (!line.empty()) {
        line = ToUpper(line);
        int len = line.length();
        if (line[len - 1] == '\r') {
          line = line.substr(0, len - 1);
        }
        
        Word* w = new Word(line);
        words_.push_back(w);
        
        // Add to the partial character hash
        partial_hash_.AddWord(w);
        
        // Also add to the traditional pattern hash for comparison
        CreatePatternHash(w);
      }
    }
    
    f.close();
    
    // Build the character-position counts
    partial_hash_.BuildCounts();
    
    cout << "Read " << words_.size() << " words from file '" << filename << "'" << endl;
  }
  
  // ... other existing methods ...
  
  // Benchmark the performance of different lookup methods
  void BenchmarkLookups() const {
    vector<string> test_patterns = {
      "THE", "C-T", "--G", "-----", "A-----", "------", "-------"
    };
    
    cout << "Benchmarking pattern lookups:" << endl;
    
    for (const string& pattern : test_patterns) {
      // Time the traditional pattern hash
      auto start1 = chrono::high_resolution_clock::now();
      
      auto it = word_map_.find(pattern);
      size_t count1 = (it != word_map_.end()) ? it->second.size() : 0;
      
      auto end1 = chrono::high_resolution_clock::now();
      auto duration1 = chrono::duration_cast<chrono::microseconds>(end1 - start1);
      
      // Time the partial character hash
      auto start2 = chrono::high_resolution_clock::now();
      
      Words matches = partial_hash_.FindMatches(pattern);
      size_t count2 = matches.size();
      
      auto end2 = chrono::high_resolution_clock::now();
      auto duration2 = chrono::duration_cast<chrono::microseconds>(end2 - start2);
      
      cout << "Pattern '" << pattern << "':" << endl;
      cout << "  Traditional hash: " << count1 << " words in " << duration1.count() << " μs" << endl;
      cout << "  Partial char hash: " << count2 << " words in " << duration2.count() << " μs" << endl;
      cout << "  Speedup: " << (duration1.count() > 0 ? (float)duration1.count() / duration2.count() : 0) << "x" << endl;
    }
  }
  
private:
  Words words_;                // All words
  WordMap word_map_;           // Traditional pattern hash
  PartialCharacterHash partial_hash_;  // New partial character hash
  vector<int> counts_;
};
```

The key changes:
1. We've added a `partial_hash_` member to the Library class
2. We populate this hash when reading words from a file
3. We've updated `FindMatchingWords` to use the partial character hash
4. We've added a benchmarking method to compare the two approaches

#### Optimizing the Pattern Matching Algorithm

Let's refine our pattern matching algorithm to be even more efficient:

```cpp
Words PartialCharacterHash::FindMatches(const string& pattern) const {
  Words result;
  int len = pattern.length();
  
  // First check the cache
  auto cache_it = pattern_index_.find(pattern);
  if (cache_it != pattern_index_.end()) {
    return cache_it->second;
  }
  
  // Get words of the right length
  auto len_it = length_index_.find(len);
  if (len_it == length_index_.end()) {
    return result;  // No words of this length
  }
  
  // Count the number of specified (non-wildcard) characters
  int specified_count = 0;
  for (char c : pattern) {
    if (c != '-') {
      specified_count++;
    }
  }
  
  // If all wildcards, return all words of this length
  if (specified_count == 0) {
    return len_it->second;
  }
  
  // If only one character is specified, use the character-position index directly
  if (specified_count == 1) {
    int pos = -1;
    for (int i = 0; i < len; i++) {
      if (pattern[i] != '-') {
        pos = i;
        break;
      }
    }
    
    auto char_pos_it = char_pos_index_.find(make_pair(pos, pattern[pos]));
    if (char_pos_it != char_pos_index_.end()) {
      return char_pos_it->second;
    }
    return result;
  }
  
  // For patterns with multiple specified characters, use a more complex approach
  
  // Find the most restrictive character position
  int best_pos = -1;
  char best_char = 0;
  int best_count = INT_MAX;
  
  for (int i = 0; i < len; i++) {
    if (pattern[i] != '-') {
      auto count_it = char_pos_counts_.find(make_pair(i, pattern[i]));
      int count = (count_it != char_pos_counts_.end()) ? count_it->second : 0;
      
      if (count < best_count && count > 0) {
        best_pos = i;
        best_char = pattern[i];
        best_count = count;
      }
    }
  }
  
  // If we found a restrictive position, use it as a starting filter
  if (best_pos >= 0) {
    auto char_pos_it = char_pos_index_.find(make_pair(best_pos, best_char));
    if (char_pos_it != char_pos_index_.end()) {
      // Check each candidate against the full pattern
      for (Word* word : char_pos_it->second) {
        bool match = true;
        
        for (int i = 0; i < len; i++) {
          if (pattern[i] != '-' && pattern[i] != word->word[i]) {
            match = false;
            break;
          }
        }
        
        if (match) {
          result.push_back(word);
        }
      }
    }
  }
  
  // Cache the result
  pattern_index_[pattern] = result;
  
  return result;
}
```

This refined algorithm:
1. Checks the cache first
2. Handles all-wildcard patterns efficiently
3. Handles single-character patterns directly
4. Uses the most restrictive character position for multi-character patterns
5. Caches the results for future use

#### BitSet Implementation for Even Faster Matching

For an even more efficient implementation, we can use bitsets to represent which characters appear at each position:

```cpp
class BitsetCharHash {
public:
  BitsetCharHash() {}
  
  // Add a word to the hash
  void AddWord(Word* word) {
    const string& str = word->word;
    int len = str.length();
    
    // Store word in length index
    length_index_[len].push_back(word);
    
    // Create a vector of bitsets for this word
    vector<bitset<26>> char_masks(len);
    
    // Set bits for each character position
    for (int i = 0; i < len; i++) {
      char c = str[i];
      if (c >= 'A' && c <= 'Z') {
        int bit_pos = c - 'A';
        char_masks[i].set(bit_pos);
      }
    }
    
    // Store the word and its bitsets
    word_bitsets_[word] = char_masks;
  }
  
  // Find words that match a pattern
  Words FindMatches(const string& pattern) const {
    Words result;
    int len = pattern.length();
    
    // Check cache first
    auto cache_it = pattern_cache_.find(pattern);
    if (cache_it != pattern_cache_.end()) {
      return cache_it->second;
    }
    
    // Get words of the right length
    auto len_it = length_index_.find(len);
    if (len_it == length_index_.end()) {
      return result;  // No words of this length
    }
    
    // Create a pattern mask
    vector<bitset<26>> pattern_masks(len);
    vector<bool> is_wildcard(len, false);
    
    for (int i = 0; i < len; i++) {
      char c = pattern[i];
      if (c == '-') {
        // Wildcard - accept any character
        pattern_masks[i].set();  // Set all bits
        is_wildcard[i] = true;
      } else if (c >= 'A' && c <= 'Z') {
        // Specific character
        int bit_pos = c - 'A';
        pattern_masks[i].set(bit_pos);
      }
    }
    
    // Check each word of the right length
    for (Word* word : len_it->second) {
      const auto& word_masks = word_bitsets_.at(word);
      bool match = true;
      
      for (int i = 0; i < len; i++) {
        if (!is_wildcard[i]) {
          // Check if the word has the required character at this position
          if ((word_masks[i] & pattern_masks[i]).none()) {
            match = false;
            break;
          }
        }
      }
      
      if (match) {
        result.push_back(word);
      }
    }
    
    // Cache the result
    pattern_cache_[pattern] = result;
    
    return result;
  }
  
private:
  // Length-based index
  unordered_map<int, Words> length_index_;
  
  // Word to bitset mapping
  unordered_map<Word*, vector<bitset<26>>> word_bitsets_;
  
  // Pattern cache
  mutable unordered_map<string, Words> pattern_cache_;
};
```

This bitset approach provides even more efficiency:
1. It represents character possibilities as bitsets, allowing for fast bitwise operations
2. It efficiently handles wildcards by setting all bits
3. It can quickly check if a word satisfies a pattern by using bitwise AND operations

#### Performance Analysis and Comparison

Let's analyze the performance of our different approaches:

```cpp
void PerformanceAnalysis(const Library& lib) {
  vector<string> test_patterns = {
    "THE",     // Exact word
    "T--",     // One character specified
    "--E",     // One character specified at the end
    "----",    // All wildcards (short)
    "------",  // All wildcards (medium)
    "--------" // All wildcards (long)
  };
  
  cout << "Performance Analysis:" << endl;
  cout << "=====================" << endl;
  
  for (const string& pattern : test_patterns) {
    cout << "Pattern: '" << pattern << "'" << endl;
    
    // Measure the traditional pattern hash
    auto start1 = chrono::high_resolution_clock::now();
    for (int i = 0; i < 1000; i++) {
      lib.FindMatchingWordsTraditional(pattern);
    }
    auto end1 = chrono::high_resolution_clock::now();
    auto duration1 = chrono::duration_cast<chrono::milliseconds>(end1 - start1);
    
    // Measure the partial character hash
    auto start2 = chrono::high_resolution_clock::now();
    for (int i = 0; i < 1000; i++) {
      lib.FindMatchingWordsPartial(pattern);
    }
    auto end2 = chrono::high_resolution_clock::now();
    auto duration2 = chrono::duration_cast<chrono::milliseconds>(end2 - start2);
    
    // Measure the bitset hash
    auto start3 = chrono::high_resolution_clock::now();
    for (int i = 0; i < 1000; i++) {
      lib.FindMatchingWordsBitset(pattern);
    }
    auto end3 = chrono::high_resolution_clock::now();
    auto duration3 = chrono::duration_cast<chrono::milliseconds>(end3 - start3);
    
    cout << "  Traditional: " << duration1.count() << " ms" << endl;
    cout << "  Partial Char: " << duration2.count() << " ms" << endl;
    cout << "  Bitset:       " << duration3.count() << " ms" << endl;
    cout << endl;
  }
}
```

The results will depend on the specific patterns and dictionary, but we generally expect:
1. **Traditional Hash**: Fast for exact matches, slow for patterns with many wildcards
2. **Partial Character Hash**: Good balance for most patterns
3. **Bitset Hash**: Best for patterns with specific characters at known positions

#### Memory-Performance Tradeoffs

Our optimizations come with memory costs. Let's analyze the space complexity:

```cpp
void AnalyzeMemoryUsage(const Library& lib) {
  size_t traditional_size = lib.EstimateTraditionalHashSize();
  size_t partial_size = lib.EstimatePartialHashSize();
  size_t bitset_size = lib.EstimateBitsetHashSize();
  
  cout << "Memory Usage Analysis:" << endl;
  cout << "======================" << endl;
  cout << "  Traditional Hash: " << traditional_size / (1024 * 1024) << " MB" << endl;
  cout << "  Partial Char Hash: " << partial_size / (1024 * 1024) << " MB" << endl;
  cout << "  Bitset Hash:       " << bitset_size / (1024 * 1024) << " MB" << endl;
}
```

The memory usage will vary, but we typically expect:
1. **Traditional Hash**: Higher memory usage due to storing all pattern variations
2. **Partial Character Hash**: Moderate memory usage
3. **Bitset Hash**: Lower memory usage for the core structure, but potentially higher when caching many patterns

#### Combining Approaches for Optimal Performance

For the best performance, we can use a hybrid approach:

```cpp
Words Library::FindMatchingWords(const string& pattern) const {
  // Check if this is an exact pattern (no wildcards)
  bool has_wildcard = false;
  for (char c : pattern) {
    if (c == '-') {
      has_wildcard = true;
      break;
    }
  }
  
  if (!has_wildcard) {
    // For exact patterns, use the traditional hash
    auto it = word_map_.find(pattern);
    if (it != word_map_.end()) {
      return it->second;
    }
    return Words();
  }
  
  // For wildcard patterns, use the partial character hash
  return partial_hash_.FindMatches(pattern);
}
```

This hybrid approach:
1. Uses the traditional hash for exact patterns (very fast lookups)
2. Uses the partial character hash for wildcard patterns (more efficient)

#### Putting It All Together

Let's integrate these optimizations into our Library class:

```cpp
class Library {
public:
  Library() {}
  ~Library() {
    for (Word* w : words_) {
      delete w;
    }
  }
  
  // Find words matching a pattern using the optimal approach
  Words FindMatchingWords(const string& pattern) const {
    // Check if this is an exact pattern (no wildcards)
    bool has_wildcard = false;
    for (char c : pattern) {
      if (c == '-') {
        has_wildcard = true;
        break;
      }
    }
    
    if (!has_wildcard) {
      // For exact patterns, use the traditional hash
      auto it = word_map_.find(pattern);
      if (it != word_map_.end()) {
        return it->second;
      }
      return Words();
    }
    
    // For wildcard patterns, use the best approach based on pattern
    if (pattern.length() <= 3) {
      // For short patterns, the traditional hash might be fast enough
      auto it = word_map_.find(pattern);
      if (it != word_map_.end()) {
        return it->second;
      }
    }
    
    // For longer or more complex patterns, use the partial character hash
    return partial_hash_.FindMatches(pattern);
  }
  
  // ... other methods ...
  
  // Various lookup methods for comparison
  Words FindMatchingWordsTraditional(const string& pattern) const {
    auto it = word_map_.find(pattern);
    if (it != word_map_.end()) {
      return it->second;
    }
    return Words();
  }
  
  Words FindMatchingWordsPartial(const string& pattern) const {
    return partial_hash_.FindMatches(pattern);
  }
  
  Words FindMatchingWordsBitset(const string& pattern) const {
    return bitset_hash_.FindMatches(pattern);
  }
  
private:
  Words words_;
  WordMap word_map_;
  PartialCharacterHash partial_hash_;
  BitsetCharHash bitset_hash_;
  vector<int> counts_;
};
```

With these optimizations, our Library class now offers significantly faster pattern matching, especially for the types of patterns commonly encountered in crossword solving.

#### Impact on the Solver

The improved pattern matching performance directly benefits our crossword solver:

```cpp
vector<string> Solver::FindCandidateWords(const Pattern& pattern) {
  vector<string> candidates;
  
  // Use our optimized matching function
  auto matches = lib_.FindMatchingWords(pattern.pattern);
  
  // Time the matching
  auto start = chrono::high_resolution_clock::now();
  
  // Process matches
  for (const Word* word : matches) {
    // Apply other constraints (no duplicates, etc.)
    if (!allow_duplicates_ && grid_.IsWordUsed(word->word) && 
        !grid_.ShouldAllowDuplicate(word->word)) {
      continue;
    }
    
    // Verify the word fits in the grid
    if (grid_.IsWordPlaceable(pattern.span, word->word)) {
      candidates.push_back(word->word);
    }
  }
  
  auto end = chrono::high_resolution_clock::now();
  auto duration = chrono::duration_cast<chrono::microseconds>(end - start);
  
  // Debug output
  if (debug_level_ > 1) {
    cout << "Found " << candidates.size() << " candidates for pattern " 
         << pattern.pattern << " in " << duration.count() << " μs" << endl;
  }
  
  return candidates;
}
```

This improved lookup speed enables our solver to handle larger puzzles and dictionaries efficiently.

#### Conclusion

In this chapter, we've significantly optimized our word lookup mechanism using partial character hashing. The key improvements include:

1. **Faster Pattern Matching**: We can now find words matching wildcard patterns much more efficiently.

2. **Scalability**: Our approach scales better with larger dictionaries and more complex patterns.

3. **Memory Efficiency**: We've optimized memory usage while maintaining fast lookups.

4. **Hybrid Approach**: We've combined different strategies for optimal performance in various scenarios.

These optimizations make our crossword solver faster and more capable of handling professional-grade puzzles and dictionaries. In the next chapters, we'll explore further enhancements such as multi-threading and scoring algorithms to create even better crossword puzzles.

#### Practice Exercises

1. Enhance the pattern matching to support character classes (e.g., vowels, consonants).
2. Implement a performance test that compares the different hashing approaches on various pattern types.
3. Add a memory-efficient version of the partial character hash for very large dictionaries.
4. Create a visualization that shows how different pattern types benefit from different hashing approaches.
5. Extend the bitset implementation to support fuzzy matching (allowing a certain number of mismatches).

### 20. Multi-threading: not as hard as you think!
### 20. Multi-threading: not as hard as you think!

In this chapter, we'll enhance our crossword puzzle solver with multi-threading capabilities. This will allow us to leverage modern multi-core processors to explore multiple solution paths simultaneously, significantly improving the speed of our solver when working with complex grids.

#### Why Multi-threading?

Solving crossword puzzles is a computationally intensive task, especially when dealing with complex grids and large dictionaries. Our solver uses a backtracking algorithm, which:

1. Tries a word in a specific position
2. Recursively attempts to fill the rest of the grid
3. Backtracks when it reaches a dead end

This process naturally leads to many independent solution paths that can be explored in parallel. By using multiple threads, we can explore several different word choices simultaneously, potentially finding a solution much faster.

#### Understanding Threads

A thread is a single sequence of execution within a program. Modern operating systems and processors support running multiple threads concurrently:

- On multi-core processors, threads can run truly in parallel
- Even on single-core processors, the operating system can rapidly switch between threads

In C++, the standard library provides thread support via the `<thread>` header since C++11. Additional synchronization mechanisms are available in `<mutex>` and `<condition_variable>`.

#### Basic Thread Creation in C++

Let's start with a simple example of creating threads:

```cpp
#include <iostream>
#include <thread>
#include <vector>

using namespace std;

// Function that will run in a separate thread
void ThreadFunction(int id) {
  cout << "Thread " << id << " running" << endl;
  
  // Simulate some work
  for (int i = 0; i < 1000000; i++) {
    // Do some calculations
    double result = sqrt(i * 3.14159);
  }
  
  cout << "Thread " << id << " finished" << endl;
}

int main() {
  const int num_threads = 4;
  vector<thread> threads;
  
  cout << "Main thread: Creating " << num_threads << " threads" << endl;
  
  // Create threads
  for (int i = 0; i < num_threads; i++) {
    threads.push_back(thread(ThreadFunction, i));
  }
  
  cout << "Main thread: Waiting for threads to finish" << endl;
  
  // Wait for all threads to finish
  for (auto& t : threads) {
    t.join();
  }
  
  cout << "Main thread: All threads have finished" << endl;
  
  return 0;
}
```

This program:
1. Creates 4 threads that run the `ThreadFunction`
2. Each thread performs some work independently
3. The main thread waits for all threads to finish using `join()`

#### Designing a Multi-threaded Solver

Now let's apply multi-threading to our crossword solver. We'll modify our `Solver` class to explore multiple paths in parallel:

```cpp
class Solver {
public:
  // ... existing code ...
  
  // New multi-threaded solve method
  bool SolveMultiThreaded(int num_threads = 4) {
    // Make sure spans are calculated
    if (grid_.spans.empty()) {
      grid_.FillSpans();
    }
    
    // Get patterns sorted by constraint
    Patterns patterns = grid_.GetSortedPatterns();
    
    cout << "Starting to solve with " << patterns.size() << " patterns" << endl;
    cout << "Using " << num_threads << " threads" << endl;
    
    // Reset statistics
    dup_stats_ = DuplicateStats();
    found_solution_ = false;
    
    // Get initial pattern
    if (patterns.empty()) {
      return true;  // Empty grid, trivial solution
    }
    
    const Pattern& first_pattern = patterns[0];
    
    // Find candidate words for the first pattern
    vector<string> candidates = FindCandidateWords(first_pattern);
    
    cout << "Found " << candidates.size() << " candidates for first pattern" << endl;
    
    // If no candidates, fail immediately
    if (candidates.empty()) {
      return false;
    }
    
    // Create a grid for each thread
    vector<Grid> thread_grids;
    for (int i = 0; i < num_threads; i++) {
      thread_grids.push_back(grid_);  // Copy the initial grid
    }
    
    // Create a mutex for thread synchronization
    mutex solution_mutex;
    
    // Create threads
    vector<thread> threads;
    int words_per_thread = (candidates.size() + num_threads - 1) / num_threads;
    
    for (int t = 0; t < num_threads; t++) {
      int start_idx = t * words_per_thread;
      int end_idx = min((t + 1) * words_per_thread, (int)candidates.size());
      
      // Skip if no words for this thread
      if (start_idx >= candidates.size()) {
        continue;
      }
      
      threads.push_back(thread(&Solver::SolveThreadFunction, this, 
                               ref(thread_grids[t]), ref(patterns), 
                               start_idx, end_idx, candidates, 
                               ref(solution_mutex), t));
    }
    
    // Wait for threads to finish
    for (auto& t : threads) {
      t.join();
    }
    
    // Check if a solution was found
    if (found_solution_) {
      // Copy the solution grid to the main grid
      grid_ = solution_grid_;
    }
    
    return found_solution_;
  }
  
private:
  // Function that runs in each thread
  void SolveThreadFunction(Grid& grid, const Patterns& patterns, 
                          int start_idx, int end_idx, 
                          const vector<string>& candidates,
                          mutex& solution_mutex, int thread_id) {
    cout << "Thread " << thread_id << " exploring candidates " 
         << start_idx << " to " << (end_idx - 1) << endl;
    
    for (int i = start_idx; i < end_idx; i++) {
      // Check if a solution has already been found
      if (found_solution_) {
        return;
      }
      
      const string& word = candidates[i];
      
      cout << "Thread " << thread_id << " trying word: " << word << endl;
      
      // Place the word in the thread's grid
      bool success = grid.PlaceWord(patterns[0].span, word, allow_duplicates_);
      
      if (success) {
        // Recursively try to solve the rest of the grid
        if (SolveRecursiveInThread(grid, patterns, 1, thread_id)) {
          // Found a solution, update the shared state
          lock_guard<mutex> lock(solution_mutex);
          
          if (!found_solution_) {
            found_solution_ = true;
            solution_grid_ = grid;
            
            cout << "Thread " << thread_id << " found a solution!" << endl;
          }
          
          return;
        }
        
        // If we get here, this word didn't lead to a solution
        grid.RemoveWord(patterns[0].span);
      }
    }
    
    cout << "Thread " << thread_id << " finished without finding a solution" << endl;
  }
  
  // Recursive solving function used by each thread
  bool SolveRecursiveInThread(Grid& grid, const Patterns& patterns, 
                             size_t index, int thread_id) {
    // Check if a solution has already been found
    if (found_solution_) {
      return false;
    }
    
    // Base case: we've filled all patterns
    if (index >= patterns.size()) {
      return true;  // Success!
    }
    
    // Get the current pattern to fill
    const Pattern& current = patterns[index];
    
    // If the pattern is already filled, move to the next one
    if (grid.IsSpanFilled(current.span)) {
      return SolveRecursiveInThread(grid, patterns, index + 1, thread_id);
    }
    
    // Find candidate words for this pattern
    vector<string> candidates = FindCandidateWords(current);
    
    // Try each candidate
    for (const string& word : candidates) {
      // Check if a solution has already been found
      if (found_solution_) {
        return false;
      }
      
      // Check for duplicates before placement
      bool is_duplicate = grid.IsWordUsed(word);
      bool should_place = true;
      
      if (is_duplicate) {
        if (allow_duplicates_ || grid.ShouldAllowDuplicate(word)) {
          // Allow this duplicate
        } else {
          should_place = false;
        }
      }
      
      if (should_place) {
        // Place the word in the grid
        bool success = grid.PlaceWord(current.span, word, allow_duplicates_);
        
        if (success) {
          // Recursively try to solve the rest of the grid
          if (SolveRecursiveInThread(grid, patterns, index + 1, thread_id)) {
            return true;  // Success!
          }
          
          // If we get here, this word didn't lead to a solution
          grid.RemoveWord(current.span);
        }
      }
    }
    
    // If we tried all candidates and none worked, this is a dead end
    return false;
  }
  
  // ... existing members ...
  
  // New members for multi-threading
  atomic<bool> found_solution_{false};  // Shared flag indicating if a solution was found
  Grid solution_grid_;  // Grid to store the solution
};
```

This implementation:
1. Divides the candidates for the first pattern among multiple threads
2. Each thread explores its assigned candidates independently
3. When a thread finds a solution, it updates a shared flag and solution grid
4. Threads check this flag regularly and stop if a solution has been found

#### Thread Synchronization

When multiple threads access shared data, we need to ensure proper synchronization:

```cpp
#include <mutex>
#include <atomic>

// ... inside the Solver class ...

private:
  // Atomic flag indicating if a solution was found
  atomic<bool> found_solution_{false};
  
  // Mutex for thread synchronization
  mutex solution_mutex_;
  
  // Grid to store the solution
  Grid solution_grid_;
```

We use:
- `atomic<bool>` for the `found_solution_` flag, which can be safely accessed by multiple threads
- `mutex` for protecting access to the `solution_grid_` when a solution is found

#### Load Balancing

Our initial implementation divides the work evenly among threads, but this may not be optimal. Some solution paths may be explored much faster than others. Let's implement a more dynamic work distribution:

```cpp
class WorkQueue {
public:
  WorkQueue() : done_(false) {}
  
  void AddWork(const string& word, const Pattern& pattern) {
    lock_guard<mutex> lock(queue_mutex_);
    work_items_.push_back(make_pair(word, pattern));
  }
  
  bool GetWork(string& word, Pattern& pattern) {
    lock_guard<mutex> lock(queue_mutex_);
    if (work_items_.empty()) {
      return false;
    }
    
    auto work = work_items_.back();
    work_items_.pop_back();
    
    word = work.first;
    pattern = work.second;
    
    return true;
  }
  
  void SetDone() {
    lock_guard<mutex> lock(queue_mutex_);
    done_ = true;
  }
  
  bool IsDone() {
    lock_guard<mutex> lock(queue_mutex_);
    return done_ && work_items_.empty();
  }
  
private:
  vector<pair<string, Pattern>> work_items_;
  mutex queue_mutex_;
  bool done_;
};

// Update the Solver class to use the work queue
class Solver {
public:
  // ... existing code ...
  
  bool SolveMultiThreadedDynamic(int num_threads = 4) {
    // ... initialization code ...
    
    // Create a work queue
    WorkQueue work_queue;
    
    // Add initial work items (first pattern candidates)
    for (const string& word : candidates) {
      work_queue.AddWork(word, first_pattern);
    }
    
    // Create threads
    vector<thread> threads;
    
    for (int t = 0; t < num_threads; t++) {
      threads.push_back(thread(&Solver::WorkerThreadFunction, this, 
                               t, ref(work_queue), ref(solution_mutex_)));
    }
    
    // Wait for threads to finish
    for (auto& t : threads) {
      t.join();
    }
    
    // ... finalization code ...
  }
  
private:
  void WorkerThreadFunction(int thread_id, WorkQueue& work_queue, mutex& solution_mutex) {
    // Create a local grid for this thread
    Grid grid = grid_;  // Copy the initial grid
    
    while (!work_queue.IsDone() && !found_solution_) {
      string word;
      Pattern pattern;
      
      // Get work from the queue
      if (!work_queue.GetWork(word, pattern)) {
        // No work available, but queue is not done
        this_thread::sleep_for(chrono::milliseconds(10));
        continue;
      }
      
      // Process this work item
      // ... (similar to the previous implementation)
      
      // Add new work items if needed
      // ... (add candidate words for the next pattern)
    }
  }
  
  // ... existing members ...
};
```

This dynamic approach:
1. Uses a shared work queue instead of static assignment
2. Threads get work items as they become available
3. As threads explore deeper in the solution space, they add new work items
4. This ensures threads are consistently busy and adapts to varying solution path complexities

#### Thread Pool Implementation

For even more flexibility, we can implement a thread pool:

```cpp
class ThreadPool {
public:
  ThreadPool(size_t num_threads) : stop_(false) {
    for (size_t i = 0; i < num_threads; ++i) {
      workers_.emplace_back([this] {
        while (true) {
          function<void()> task;
          
          {
            unique_lock<mutex> lock(queue_mutex_);
            condition_.wait(lock, [this] { 
              return stop_ || !tasks_.empty(); 
            });
            
            if (stop_ && tasks_.empty()) {
              return;
            }
            
            task = move(tasks_.front());
            tasks_.pop();
          }
          
          task();
        }
      });
    }
  }
  
  template<class F>
  void Enqueue(F&& f) {
    {
      unique_lock<mutex> lock(queue_mutex_);
      tasks_.emplace(forward<F>(f));
    }
    condition_.notify_one();
  }
  
  ~ThreadPool() {
    {
      unique_lock<mutex> lock(queue_mutex_);
      stop_ = true;
    }
    condition_.notify_all();
    for (thread& worker : workers_) {
      worker.join();
    }
  }
  
private:
  vector<thread> workers_;
  queue<function<void()>> tasks_;
  
  mutex queue_mutex_;
  condition_variable condition_;
  bool stop_;
};

// Integrate the thread pool with our Solver
class Solver {
public:
  // ... existing code ...
  
  bool SolveWithThreadPool(int num_threads = 4) {
    // ... initialization code ...
    
    // Create a thread pool
    ThreadPool pool(num_threads);
    
    // Create a counter to track active tasks
    atomic<int> active_tasks(0);
    mutex counter_mutex;
    condition_variable counter_cv;
    
    // Enqueue the initial tasks
    for (const string& word : candidates) {
      active_tasks++;
      pool.Enqueue([this, word, &patterns, &active_tasks, 
                    &counter_mutex, &counter_cv]() {
        // Create a local grid for this task
        Grid local_grid = grid_;
        
        // Try this word
        bool success = local_grid.PlaceWord(patterns[0].span, word, allow_duplicates_);
        
        if (success) {
          // Recursively try to solve the rest of the grid
          if (SolveRecursiveWithThreadPool(local_grid, patterns, 1, 
                                          active_tasks, counter_mutex, counter_cv)) {
            // Found a solution, update the shared state
            lock_guard<mutex> lock(solution_mutex_);
            
            if (!found_solution_) {
              found_solution_ = true;
              solution_grid_ = local_grid;
            }
          }
        }
        
        // Decrement the active task counter
        {
          lock_guard<mutex> lock(counter_mutex);
          active_tasks--;
        }
        counter_cv.notify_all();
      });
    }
    
    // Wait for all tasks to complete
    {
      unique_lock<mutex> lock(counter_mutex);
      counter_cv.wait(lock, [&active_tasks] { 
        return active_tasks == 0; 
      });
    }
    
    // ... finalization code ...
  }
  
private:
  bool SolveRecursiveWithThreadPool(Grid& grid, const Patterns& patterns, 
                                    size_t index,
                                    atomic<int>& active_tasks,
                                    mutex& counter_mutex,
                                    condition_variable& counter_cv) {
    // ... similar to previous recursive functions ...
  }
  
  // ... existing members ...
};
```

The thread pool implementation:
1. Creates a fixed number of worker threads
2. Maintains a queue of tasks (functions to execute)
3. Workers continuously pull tasks from the queue
4. This allows for more fine-grained task distribution

#### Performance Analysis

Let's analyze the performance of our multi-threaded solver:

```cpp
void PerformanceAnalysis(const string& grid_file, const string& dict_file) {
  // Load library and grid
  Library lib;
  lib.ReadFromFile(dict_file);
  
  Grid grid("Performance Test");
  grid.LoadFromFile(grid_file);
  
  // Create solvers
  Solver single_threaded(grid, lib);
  Solver multi_threaded(grid, lib);
  Solver dynamic_threaded(grid, lib);
  Solver pool_threaded(grid, lib);
  
  // Set options
  single_threaded.SetAllowDuplicates(false);
  multi_threaded.SetAllowDuplicates(false);
  dynamic_threaded.SetAllowDuplicates(false);
  pool_threaded.SetAllowDuplicates(false);
  
  // Measure single-threaded performance
  auto start1 = chrono::high_resolution_clock::now();
  bool success1 = single_threaded.Solve();
  auto end1 = chrono::high_resolution_clock::now();
  auto duration1 = chrono::duration_cast<chrono::milliseconds>(end1 - start1);
  
  // Reset the grid
  grid.ClearAllWords();
  
  // Measure multi-threaded performance
  auto start2 = chrono::high_resolution_clock::now();
  bool success2 = multi_threaded.SolveMultiThreaded(4);
  auto end2 = chrono::high_resolution_clock::now();
  auto duration2 = chrono::duration_cast<chrono::milliseconds>(end2 - start2);
  
  // Reset the grid
  grid.ClearAllWords();
  
  // Measure dynamic multi-threaded performance
  auto start3 = chrono::high_resolution_clock::now();
  bool success3 = dynamic_threaded.SolveMultiThreadedDynamic(4);
  auto end3 = chrono::high_resolution_clock::now();
  auto duration3 = chrono::duration_cast<chrono::milliseconds>(end3 - start3);
  
  // Reset the grid
  grid.ClearAllWords();
  
  // Measure thread pool performance
  auto start4 = chrono::high_resolution_clock::now();
  bool success4 = pool_threaded.SolveWithThreadPool(4);
  auto end4 = chrono::high_resolution_clock::now();
  auto duration4 = chrono::duration_cast<chrono::milliseconds>(end4 - start4);
  
  // Print results
  cout << "Performance Analysis:" << endl;
  cout << "====================" << endl;
  cout << "Single-threaded: " << duration1.count() << " ms (success: " << success1 << ")" << endl;
  cout << "Multi-threaded: " << duration2.count() << " ms (success: " << success2 << ")" << endl;
  cout << "Dynamic threading: " << duration3.count() << " ms (success: " << success3 << ")" << endl;
  cout << "Thread pool: " << duration4.count() << " ms (success: " << success4 << ")" << endl;
  
  // Calculate speedup
  double speedup2 = (double)duration1.count() / duration2.count();
  double speedup3 = (double)duration1.count() / duration3.count();
  double speedup4 = (double)duration1.count() / duration4.count();
  
  cout << "Speedup (multi-threaded): " << speedup2 << "x" << endl;
  cout << "Speedup (dynamic): " << speedup3 << "x" << endl;
  cout << "Speedup (thread pool): " << speedup4 << "x" << endl;
}
```

The results will vary depending on:
1. The complexity of the grid
2. The size of the dictionary
3. The number of cores in your CPU
4. The threading implementation used

In general, we expect significant speedups on modern multi-core processors.

#### Challenges and Considerations

Multi-threading introduces some challenges:

1. **Thread Safety**: We need to ensure proper synchronization of shared data
2. **Load Balancing**: Work should be evenly distributed among threads
3. **Overhead**: Creating and managing threads has overhead
4. **Debugging**: Multi-threaded code can be more difficult to debug

In our implementation, we've addressed these challenges through:
- Careful synchronization using mutexes and atomic variables
- Dynamic work distribution to balance load
- Thread pool to minimize thread creation overhead
- Clear logging to aid in debugging

#### Putting It All Together

Let's combine all our multi-threading implementations:

```cpp
#include <atomic>
#include <chrono>
#include <condition_variable>
#include <functional>
#include <iostream>
#include <mutex>
#include <queue>
#include <thread>
#include <vector>

// ... existing Library and Grid classes ...

// Thread pool implementation
class ThreadPool {
public:
  ThreadPool(size_t num_threads);
  ~ThreadPool();
  
  template<class F>
  void Enqueue(F&& f);
  
private:
  vector<thread> workers_;
  queue<function<void()>> tasks_;
  
  mutex queue_mutex_;
  condition_variable condition_;
  bool stop_;
};

// Work queue for dynamic threading
class WorkQueue {
public:
  WorkQueue();
  
  void AddWork(const string& word, const Pattern& pattern);
  bool GetWork(string& word, Pattern& pattern);
  void SetDone();
  bool IsDone();
  
private:
  vector<pair<string, Pattern>> work_items_;
  mutex queue_mutex_;
  bool done_;
};

// Enhanced Solver with multi-threading
class Solver {
public:
  Solver(Grid& g, Library& l);
  
  // Single-threaded solve
  bool Solve();
  
  // Multi-threaded solve with static work distribution
  bool SolveMultiThreaded(int num_threads = 4);
  
  // Multi-threaded solve with dynamic work distribution
  bool SolveMultiThreadedDynamic(int num_threads = 4);
  
  // Multi-threaded solve with thread pool
  bool SolveWithThreadPool(int num_threads = 4);
  
  // ... existing methods ...
  
private:
  // Thread functions
  void SolveThreadFunction(Grid& grid, const Patterns& patterns, 
                          int start_idx, int end_idx, 
                          const vector<string>& candidates,
                          mutex& solution_mutex, int thread_id);
                          
  void WorkerThreadFunction(int thread_id, WorkQueue& work_queue, mutex& solution_mutex);
  
  // Recursive solving functions
  bool SolveRecursive(const Patterns& patterns, size_t index);
  bool SolveRecursiveInThread(Grid& grid, const Patterns& patterns, size_t index, int thread_id);
  
  // ... existing members ...
  
  // Threading members
  atomic<bool> found_solution_{false};
  mutex solution_mutex_;
  Grid solution_grid_;
};

// Performance analysis function
void PerformanceAnalysis(const string& grid_file, const string& dict_file);

int main() {
  // Load library and grid
  Library lib;
  lib.ReadFromFile("top_12000.txt");
  
  Grid grid("Crossword Puzzle");
  grid.LoadFromFile("test.txt");
  
  // Create solver
  Solver solver(grid, lib);
  
  // Try multi-threaded solve
  cout << "Solving with multi-threading..." << endl;
  
  auto start = chrono::high_resolution_clock::now();
  bool success = solver.SolveMultiThreaded(4);
  auto end = chrono::high_resolution_clock::now();
  
  auto duration = chrono::duration_cast<chrono::milliseconds>(end - start);
  
  cout << "Solved in " << duration.count() << " ms" << endl;
  cout << "Solution " << (success ? "found" : "not found") << endl;
  
  grid.Print();
  
  // Run performance analysis
  cout << "\nRunning performance analysis..." << endl;
  PerformanceAnalysis("test.txt", "top_12000.txt");
  
  return 0;
}
```

#### Conclusion

In this chapter, we've enhanced our crossword puzzle solver with multi-threading capabilities:

1. **Basic Multi-threading**: We implemented a simple approach that divides work among threads
2. **Dynamic Work Distribution**: We added a more flexible system using a work queue
3. **Thread Pool**: We created a reusable thread pool for efficient task execution
4. **Performance Analysis**: We compared different threading approaches

By leveraging the power of modern multi-core processors, our solver can now explore multiple solution paths simultaneously, potentially finding solutions much faster, especially for complex puzzles.

The techniques we've learned in this chapter are not only applicable to crossword solving but can be applied to many other computationally intensive tasks that can be parallelized.

#### Practice Exercises

1. Add a configuration option to automatically select the optimal number of threads based on CPU cores.
2. Implement a work-stealing mechanism to further improve load balancing between threads.
3. Add progress reporting to show how much of the solution space has been explored.
4. Create a visualization that shows the solution paths being explored by different threads.
5. Extend the multi-threading to other parts of the solver, such as pattern matching.

### 21. Adding points to the library word and scoring
### 21. Adding points to the library word and scoring

In this chapter, we'll enhance our crossword puzzle solver by implementing a sophisticated word scoring system. This will allow our solver to prioritize high-quality words, producing crossword puzzles that are more enjoyable and natural for solvers.

#### Why Word Scoring Matters

So far, our crossword solver has focused on finding *any* valid solution. However, not all valid solutions are equally good from a puzzle constructor's perspective. A high-quality crossword puzzle should:

1. Use common, recognizable words that solvers are likely to know
2. Avoid obscure abbreviations, foreign terms, or archaic words
3. Include a good mix of common and interesting vocabulary
4. Minimize the use of "crosswordese" (words that appear frequently in crosswords but rarely in everyday language)

By implementing a scoring system, we can guide our solver toward solutions that meet these criteria.

#### Designing the Scoring System

Let's start by enhancing our `Word` structure to include a score:

```cpp
struct Word {
  Word() {}
  Word(string s, int q = 1) : word(s), quality(q) {}
  int len() const { return word.length(); }
  
  string word;
  int quality;  // Higher is better
};
```

The `quality` field is an integer value where higher numbers represent better words. This simple approach allows us to rank words while keeping our data structure clean.

#### Scoring Algorithms

We'll implement several scoring algorithms that contribute to a word's overall quality:

1. **Frequency-Based Scoring**: Words that appear more frequently in English text get higher scores
2. **Length-Based Adjustment**: Adjustments based on word length (favoring medium-length words)
3. **Character Variety**: Words with a good mix of different letters (especially vowels and consonants)
4. **Scrabble Score**: Using letter values from Scrabble as a component of scoring

Let's implement these algorithms:

```cpp
class WordScorer {
public:
  // Calculate a composite quality score for a word
  static int ScoreWord(const string& word) {
    int freq_score = FrequencyScore(word);
    int length_score = LengthScore(word);
    int variety_score = CharacterVarietyScore(word);
    int scrabble_score = ScrabbleScore(word);
    
    // Combine scores with appropriate weights
    int composite_score = (freq_score * 5) + 
                          (length_score * 2) + 
                          (variety_score * 1) + 
                          (scrabble_score * 1);
    
    // Ensure a minimum score of 1
    return max(1, composite_score);
  }
  
private:
  // Score based on word frequency (higher for more common words)
  static int FrequencyScore(const string& word) {
    // Simplified approach that classifies words into tiers
    // In a real implementation, this would use actual frequency data
    static const unordered_set<string> tier1 = {"THE", "AND", "FOR", "THAT", "WITH"};
    static const unordered_set<string> tier2 = {"ABOUT", "WOULD", "THERE", "THEIR", "WHICH"};
    
    if (tier1.find(word) != tier1.end()) return 10;
    if (tier2.find(word) != tier2.end()) return 8;
    
    // Default score based on length (shorter words tend to be more common)
    return max(1, 10 - word.length());
  }
  
  // Score based on word length (favoring medium-length words)
  static int LengthScore(const string& word) {
    int len = word.length();
    
    // Penalize very short words
    if (len <= 3) return 1;
    
    // Favor medium-length words (5-8 letters)
    if (len >= 5 && len <= 8) return 5;
    
    // Slightly penalize longer words
    if (len > 10) return 2;
    
    // Default
    return 3;
  }
  
  // Score based on character variety
  static int CharacterVarietyScore(const string& word) {
    // Count unique letters
    unordered_set<char> unique_chars;
    for (char c : word) {
      unique_chars.insert(c);
    }
    
    // Count vowels
    int vowel_count = 0;
    for (char c : word) {
      if (c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U') {
        vowel_count++;
      }
    }
    
    // Calculate vowel ratio (should be around 40% for English)
    double vowel_ratio = (double)vowel_count / word.length();
    int vowel_score = (vowel_ratio >= 0.3 && vowel_ratio <= 0.5) ? 3 : 1;
    
    // Score based on unique characters and vowel ratio
    return min(5, (int)unique_chars.size() / 2) + vowel_score;
  }
  
  // Score based on Scrabble letter values
  static int ScrabbleScore(const string& word) {
    static const unordered_map<char, int> letter_values = {
      {'A', 1}, {'B', 3}, {'C', 3}, {'D', 2}, {'E', 1},
      {'F', 4}, {'G', 2}, {'H', 4}, {'I', 1}, {'J', 8},
      {'K', 5}, {'L', 1}, {'M', 3}, {'N', 1}, {'O', 1},
      {'P', 3}, {'Q', 10}, {'R', 1}, {'S', 1}, {'T', 1},
      {'U', 1}, {'V', 4}, {'W', 4}, {'X', 8}, {'Y', 4},
      {'Z', 10}
    };
    
    int score = 0;
    for (char c : word) {
      score += letter_values.at(c);
    }
    
    // Normalize score (1-10 scale)
    return min(10, 1 + score / 3);
  }
};
```

This `WordScorer` class provides a flexible way to evaluate word quality based on multiple criteria. We can adjust the weights of different factors to fine-tune our scoring.

#### Loading Word Frequencies from a File

In a real-world implementation, we would load word frequencies from a data file. Let's implement this capability:

```cpp
class FrequencyLoader {
public:
  // Load word frequencies from a file
  static unordered_map<string, int> LoadFrequencies(const string& filename) {
    unordered_map<string, int> frequencies;
    
    ifstream file(filename);
    if (!file.is_open()) {
      cerr << "Error: Could not open frequency file: " << filename << endl;
      return frequencies;
    }
    
    string line;
    while (getline(file, line)) {
      istringstream iss(line);
      string word;
      int freq;
      
      if (iss >> word >> freq) {
        // Convert to uppercase for consistency
        for (char& c : word) {
          c = toupper(c);
        }
        
        frequencies[word] = freq;
      }
    }
    
    file.close();
    cout << "Loaded " << frequencies.size() << " word frequencies from " << filename << endl;
    
    return frequencies;
  }
};
```

This function loads word frequencies from a tab-separated file with word-frequency pairs.

#### Integrating Word Scoring with the Library

Now, let's enhance our `Library` class to use these scoring mechanisms:

```cpp
class Library {
public:
  Library() {}
  ~Library() {
    for (Word* w : words_) {
      delete w;
    }
  }
  
  // Read words from a file with scoring
  void ReadFromFile(const string& filename, const string& freq_file = "") {
    // Load word frequencies if available
    unordered_map<string, int> frequencies;
    if (!freq_file.empty()) {
      frequencies = FrequencyLoader::LoadFrequencies(freq_file);
    }
    
    // Open word list file
    ifstream f(filename);
    if (!f.is_open()) {
      cerr << "Error: Could not open word file: " << filename << endl;
      return;
    }
    
    // Read words
    while (!f.eof()) {
      string line;
      getline(f, line);
      
      if (!line.empty()) {
        line = ToUpper(line);
        if (line[line.length() - 1] == '\r') {
          line = line.substr(0, line.length() - 1);
        }
        
        // Calculate word quality
        int quality;
        if (!frequencies.empty() && frequencies.find(line) != frequencies.end()) {
          // Use loaded frequency if available
          quality = min(10, 1 + (int)log10(frequencies[line]));
        } else {
          // Otherwise use our scoring algorithm
          quality = WordScorer::ScoreWord(line);
        }
        
        // Create word with quality score
        Word* w = new Word(line, quality);
        words_.push_back(w);
        
        // Add to indices
        word_map_[line].push_back(w);
        CreatePatternHash(w);
      }
    }
    
    f.close();
    
    cout << "Read " << words_.size() << " words from file '" << filename << "'" << endl;
    
    // Compute word statistics with quality distribution
    ComputeStats();
  }
  
  // Enhanced statistics with quality distribution
  void ComputeStats() {
    // ... existing counts code ...
    
    // Compute quality distribution
    quality_counts_.resize(11, 0);  // Quality scores 0-10
    
    for (const Word* w : words_) {
      int q = min(10, w->quality);
      quality_counts_[q]++;
    }
  }
  
  void PrintStats() const {
    // ... existing stats output ...
    
    // Print quality distribution
    cout << "Word quality distribution:" << endl;
    for (int i = 1; i <= 10; i++) {
      cout << "  Quality " << i << ": " << quality_counts_[i] << " words" << endl;
    }
  }
  
  // Get a sample of words with different quality scores
  void PrintWordSamples() const {
    cout << "Word quality samples:" << endl;
    
    // Create buckets for each quality level
    vector<vector<const Word*>> quality_buckets(11);
    for (const Word* w : words_) {
      int q = min(10, w->quality);
      quality_buckets[q].push_back(w);
    }
    
    // Print samples from each quality level
    for (int q = 10; q >= 1; q--) {
      const auto& bucket = quality_buckets[q];
      if (!bucket.empty()) {
        cout << "  Quality " << q << " words: ";
        
        // Print up to 5 examples
        for (int i = 0; i < min(5, (int)bucket.size()); i++) {
          cout << bucket[i]->word << " ";
        }
        cout << endl;
      }
    }
  }
  
  // ... existing methods ...
  
private:
  // ... existing members ...
  vector<int> quality_counts_;  // Distribution of quality scores
};
```

With these enhancements, our Library now assigns and tracks quality scores for all words.

#### Enhancing the Solver with Word Quality

Now let's modify our Solver to prioritize high-quality words:

```cpp
class Solver {
public:
  // ... existing methods ...
  
  // Set quality preference (higher values favor higher quality words)
  void SetQualityPreference(double pref) {
    quality_preference_ = pref;
  }
  
  // Enhanced candidate finding with quality-based sorting
  vector<string> FindCandidateWords(const Pattern& pattern) {
    vector<pair<string, double>> scored_candidates;
    
    // Find all words matching the pattern
    Words matches = lib_.FindMatchingWords(pattern.pattern);
    
    for (const Word* word : matches) {
      // Apply existing filters (duplicates, etc.)
      if (!allow_duplicates_ && grid_.IsWordUsed(word->word) && 
          !grid_.ShouldAllowDuplicate(word->word)) {
        continue;
      }
      
      // Verify the word fits in the grid
      if (grid_.IsWordPlaceable(pattern.span, word->word)) {
        // Calculate a score that combines quality and constraint satisfaction
        double score = CalculateCandidateScore(word, pattern);
        scored_candidates.push_back(make_pair(word->word, score));
      }
    }
    
    // Sort by score (higher first)
    sort(scored_candidates.begin(), scored_candidates.end(),
         [](const pair<string, double>& a, const pair<string, double>& b) {
           return a.second > b.second;
         });
    
    // Extract just the words
    vector<string> candidates;
    for (const auto& pair : scored_candidates) {
      candidates.push_back(pair.first);
    }
    
    return candidates;
  }
  
private:
  // Calculate a score for a candidate word
  double CalculateCandidateScore(const Word* word, const Pattern& pattern) {
    // Base score is the word's quality
    double score = word->quality;
    
    // Adjust based on how constrained the pattern is
    int filled_positions = 0;
    for (char c : pattern.pattern) {
      if (c != '-') filled_positions++;
    }
    
    // Words that satisfy more constraints get a bonus
    double constraint_bonus = filled_positions * 2.0;
    
    // Apply quality preference factor
    return (score * quality_preference_) + constraint_bonus;
  }
  
  // ... existing members ...
  double quality_preference_ = 1.0;  // How much to prioritize word quality
};
```

This enhancement:
1. Adds a quality preference setting to control how much we prioritize word quality
2. Modifies candidate selection to favor higher quality words
3. Uses a scoring system that balances quality and constraint satisfaction

#### Grid Quality Scoring

We can also score entire grid solutions based on the quality of the words used:

```cpp
class GridScorer {
public:
  // Calculate the overall quality of a grid solution
  static double ScoreGrid(const Grid& grid, const Library& lib) {
    double total_score = 0;
    double min_word_score = 10;
    double avg_word_score = 0;
    
    // Get all words placed in the grid
    vector<pair<Span, string>> words = grid.GetPlacedWords();
    
    if (words.empty()) {
      return 0;  // Empty grid
    }
    
    // Calculate scores for each word
    for (const auto& entry : words) {
      const string& word = entry.second;
      
      // Get word quality (either from library or recalculate)
      double word_score = lib.GetWordQuality(word);
      
      // Update statistics
      total_score += word_score;
      min_word_score = min(min_word_score, word_score);
    }
    
    avg_word_score = total_score / words.size();
    
    // Final score combines average and minimum word quality
    // This penalizes grids with even a single poor word
    return (avg_word_score * 0.7) + (min_word_score * 0.3);
  }
};
```

We can integrate this scoring into our solver to keep track of the best solutions:

```cpp
class Solver {
public:
  // ... existing methods ...
  
  // Solve and return the best solution based on quality
  Grid SolveBest(int max_solutions = 10) {
    // Reset best solution tracking
    best_solutions_.clear();
    best_scores_.clear();
    
    // Make sure spans are calculated
    if (grid_.spans.empty()) {
      grid_.FillSpans();
    }
    
    // Get patterns sorted by constraint
    Patterns patterns = grid_.GetSortedPatterns();
    
    cout << "Looking for " << max_solutions << " best solutions..." << endl;
    
    // Start recursive solving
    SolveRecursiveBest(patterns, 0, max_solutions);
    
    // Return the best solution if found
    if (!best_solutions_.empty()) {
      cout << "Found " << best_solutions_.size() << " solutions" << endl;
      
      // Print quality scores
      cout << "Solution qualities:" << endl;
      for (int i = 0; i < best_solutions_.size(); i++) {
        cout << "  Solution " << (i + 1) << ": " << best_scores_[i] << endl;
      }
      
      // Return the best solution (highest score)
      return best_solutions_[0];
    } else {
      cout << "No solutions found" << endl;
      return grid_;  // Return the original grid
    }
  }
  
private:
  // Recursive solving that tracks the best solutions
  bool SolveRecursiveBest(const Patterns& patterns, size_t index, int max_solutions) {
    // Base case: we've filled all patterns
    if (index >= patterns.size()) {
      // Found a complete solution - score it
      double score = GridScorer::ScoreGrid(grid_, lib_);
      
      // Add to our list of best solutions
      AddSolution(grid_, score, max_solutions);
      
      // Continue searching for more solutions
      return false;
    }
    
    // ... rest of recursive solving logic ...
  }
  
  // Add a solution to our list of best solutions
  void AddSolution(const Grid& grid, double score, int max_solutions) {
    // Find where this solution ranks
    int insert_pos = best_scores_.size();
    for (int i = 0; i < best_scores_.size(); i++) {
      if (score > best_scores_[i]) {
        insert_pos = i;
        break;
      }
    }
    
    // Insert the solution at the appropriate position
    if (insert_pos < max_solutions) {
      best_solutions_.insert(best_solutions_.begin() + insert_pos, grid);
      best_scores_.insert(best_scores_.begin() + insert_pos, score);
      
      // Trim excess solutions
      if (best_solutions_.size() > max_solutions) {
        best_solutions_.pop_back();
        best_scores_.pop_back();
      }
    }
  }
  
  // ... existing members ...
  
  // Best solution tracking
  vector<Grid> best_solutions_;
  vector<double> best_scores_;
};
```

This enhancement:
1. Tracks multiple solutions based on their quality
2. Returns the highest quality solution
3. Allows exploring more of the solution space to find better puzzles

#### Word Visualization with Quality Indicators

To better understand our word quality system, let's add a visualization method:

```cpp
void Grid::PrintWithQuality(const Library& lib) const {
  // Create grid for quality visualization
  vector<vector<char>> quality_markers(lines.size(), vector<char>(lines[0].size(), ' '));
  
  // Assign quality markers to cells based on words
  for (const auto& entry : placed_words) {
    const Span& span = entry.first;
    const string& word = entry.second;
    
    // Get word quality
    int quality = lib.GetWordQuality(word);
    
    // Convert quality to a character (higher quality = brighter color)
    char marker;
    if (quality >= 8) marker = '+';      // High quality
    else if (quality >= 5) marker = '*';  // Medium quality
    else marker = '-';                    // Low quality
    
    // Mark all cells in this word
    Point p = span.point;
    for (int i = 0; i < span.len; i++) {
      quality_markers[p.row][p.col] = marker;
      if (span.vert) p.row++;
      else p.col++;
    }
  }
  
  // Print the grid with quality markers
  cout << "Grid with quality indicators:" << endl;
  cout << "  '+' = high quality, '*' = medium quality, '-' = low quality" << endl << endl;
  
  for (size_t r = 0; r < lines.size(); r++) {
    // Print the grid line
    cout << lines[r] << "   ";
    
    // Print the quality markers
    for (size_t c = 0; c < lines[r].size(); c++) {
      cout << quality_markers[r][c];
    }
    
    cout << endl;
  }
}
```

This visualization makes it easy to identify areas of the grid with lower quality words that might need improvement.

#### Putting It All Together

Let's combine all these enhancements into our program:

```cpp
#include <algorithm>
#include <cmath>
#include <fstream>
#include <iomanip>
#include <iostream>
#include <sstream>
#include <string>
#include <unordered_map>
#include <unordered_set>
#include <vector>

// ... existing Point, Span, Pattern classes ...

// Enhanced Word with quality
struct Word {
  Word() {}
  Word(string s, int q = 1) : word(s), quality(q) {}
  int len() const { return word.length(); }
  
  string word;
  int quality;  // Higher is better
};

// Word scoring
class WordScorer {
public:
  static int ScoreWord(const string& word);
  
private:
  static int FrequencyScore(const string& word);
  static int LengthScore(const string& word);
  static int CharacterVarietyScore(const string& word);
  static int ScrabbleScore(const string& word);
};

// Frequency loading
class FrequencyLoader {
public:
  static unordered_map<string, int> LoadFrequencies(const string& filename);
};

// Enhanced Library with word quality
class Library {
public:
  // ... existing methods ...
  
  void ReadFromFile(const string& filename, const string& freq_file = "");
  void ComputeStats();
  void PrintStats() const;
  void PrintWordSamples() const;
  int GetWordQuality(const string& word) const;
  
private:
  // ... existing members ...
  vector<int> quality_counts_;
};

// Grid scoring
class GridScorer {
public:
  static double ScoreGrid(const Grid& grid, const Library& lib);
};

// Enhanced Solver with quality preference
class Solver {
public:
  // ... existing methods ...
  
  void SetQualityPreference(double pref);
  Grid SolveBest(int max_solutions = 10);
  
private:
  // ... existing methods ...
  
  bool SolveRecursiveBest(const Patterns& patterns, size_t index, int max_solutions);
  void AddSolution(const Grid& grid, double score, int max_solutions);
  double CalculateCandidateScore(const Word* word, const Pattern& pattern);
  
  double quality_preference_ = 1.0;
  vector<Grid> best_solutions_;
  vector<double> best_scores_;
};

// Enhanced Grid with quality visualization
class Grid {
public:
  // ... existing methods ...
  
  void PrintWithQuality(const Library& lib) const;
};

int main() {
  // Load library with word frequencies
  Library lib;
  lib.ReadFromFile("top_12000.txt", "word_frequencies.txt");
  
  // Print some statistics
  lib.PrintStats();
  lib.PrintWordSamples();
  
  // Load grid
  Grid grid("Crossword Puzzle");
  grid.LoadFromFile("test.txt");
  
  // Create solver with quality preference
  Solver solver(grid, lib);
  solver.SetQualityPreference(2.0);  // Strongly prefer high-quality words
  
  // Find the best solution
  Grid solution = solver.SolveBest(5);
  
  // Print the solution with quality indicators
  solution.PrintWithQuality(lib);
  
  return 0;
}
```

#### Sample Word Frequency File Format

Here's an example of what the word frequency file might look like:
```
the 23135851162
of 13151942776
and 12997637966
to 12136980858
a 9081174698
in 8469404971
for 5933321709
is 4705743816
on 3750423199
that 3400031103
...
```

#### Conclusion

In this chapter, we've significantly enhanced our crossword puzzle solver with word quality scoring:

1. **Word Quality Measures**: We've implemented algorithms to evaluate word quality based on frequency, length, character variety, and Scrabble score.

2. **Quality-Based Selection**: Our solver now prioritizes higher quality words when exploring solution paths.

3. **Grid Quality Scoring**: We can evaluate entire grid solutions based on the quality of the words used.

4. **Multiple Solution Tracking**: We can find and compare multiple solutions to identify the highest quality puzzles.

5. **Quality Visualization**: We've added tools to visualize word quality within the grid.

These enhancements transform our solver from a tool that merely finds valid solutions to one that creates high-quality crossword puzzles with natural, recognizable vocabulary. This is a crucial step toward generating puzzles that would be enjoyable for human solvers.

#### Practice Exercises

1. Implement a more sophisticated frequency-based scoring system using a comprehensive word frequency database.

2. Add a thematic scoring component that gives bonus points to words related to a specific theme.

3. Create a user interface that allows adjusting quality preferences interactively.

4. Implement a system to score word intersections, favoring natural letter combinations at crossing points.

5. Create a visualization that shows how the solver's word choices change when quality preferences are adjusted.

### 22. Ordered map to save the best N solutions
### 22. Ordered map to save the best N solutions

In this chapter, we'll enhance our crossword puzzle solver to efficiently track and manage multiple high-quality solutions. We'll implement an ordered data structure to automatically maintain a collection of the best N solutions found during the solving process, allowing us to present users with multiple high-quality options.

#### Why Track Multiple Solutions?

So far, our solver has focused on finding a single solution, or in Chapter 21, tracking a fixed number of best solutions. However, there are compelling reasons to maintain a dynamic collection of the best solutions:

1. **Quality vs. Diversity**: The highest-scoring solution may not always be the most desirable; having multiple options allows for subjective selection.
2. **Themed Puzzles**: Different solutions may include different theme words or patterns.
3. **Editorial Flexibility**: Puzzle editors often prefer having options to choose from.
4. **Performance Optimization**: We can keep exploring the solution space even after finding acceptable solutions.

#### Understanding Ordered Maps

The C++ Standard Library provides `std::map` and `std::set`, which maintain their elements in a sorted order. For our purpose, we'll use a `map` to associate solution grids with their quality scores:

```cpp
#include <map>
using SolutionMap = map<double, Grid, greater<double>>;
```

This creates a map where:
- The key is the solution quality score (double)
- The value is the Grid representing that solution
- The ordering is from highest to lowest score (using `greater<double>`)

The `map` container automatically keeps elements sorted by key, making it perfect for tracking our best solutions.

#### Implementing a Solution Tracker

Let's implement a class to manage our collection of best solutions:

```cpp
class SolutionTracker {
public:
  SolutionTracker(size_t max_solutions = 10) 
    : max_solutions_(max_solutions) {}
  
  // Add a solution to the tracker
  bool AddSolution(const Grid& grid, double score) {
    // If we haven't reached capacity yet, add the solution
    if (solutions_.size() < max_solutions_) {
      solutions_[score] = grid;
      return true;
    }
    
    // Otherwise, check if this solution is better than our worst one
    auto last = --solutions_.end();
    if (score > last->first) {
      // Remove the worst solution
      solutions_.erase(last);
      
      // Add the new, better solution
      solutions_[score] = grid;
      return true;
    }
    
    return false;  // Solution wasn't good enough
  }
  
  // Check if a score would qualify for inclusion
  bool WouldQualify(double score) const {
    if (solutions_.size() < max_solutions_) {
      return true;  // We have room for more solutions
    }
    
    // Check against our worst solution
    auto last = --solutions_.end();
    return score > last->first;
  }
  
  // Get the best N solutions
  vector<pair<double, Grid>> GetBestSolutions(size_t n = 0) const {
    if (n == 0 || n > solutions_.size()) {
      n = solutions_.size();
    }
    
    vector<pair<double, Grid>> result;
    auto it = solutions_.begin();
    
    for (size_t i = 0; i < n && it != solutions_.end(); ++i, ++it) {
      result.push_back(*it);
    }
    
    return result;
  }
  
  // Get the number of solutions currently tracked
  size_t Size() const {
    return solutions_.size();
  }
  
  // Check if we have any solutions
  bool Empty() const {
    return solutions_.empty();
  }
  
  // Get the lowest score that would qualify
  double GetQualificationThreshold() const {
    if (solutions_.size() < max_solutions_) {
      return std::numeric_limits<double>::lowest();  // Any score qualifies
    }
    
    auto last = --solutions_.end();
    return last->first;
  }
  
private:
  SolutionMap solutions_;  // Map of score to grid
  size_t max_solutions_;   // Maximum number of solutions to track
};
```

This `SolutionTracker` class:
1. Maintains an ordered map of solutions by score
2. Automatically keeps only the best N solutions
3. Provides methods to check if a solution would qualify
4. Offers ways to retrieve the best solutions

#### Integrating with the Solver

Now, let's integrate our `SolutionTracker` with the `Solver` class:

```cpp
class Solver {
public:
  // ... existing methods ...
  
  // Solve and find the best N solutions
  vector<pair<double, Grid>> SolveBestN(size_t max_solutions = 10, 
                                       double min_quality = 0.0,
                                       int max_time_seconds = 0) {
    // Initialize solution tracker
    solution_tracker_ = SolutionTracker(max_solutions);
    
    // Make sure spans are calculated
    if (grid_.spans.empty()) {
      grid_.FillSpans();
    }
    
    // Get patterns sorted by constraint
    Patterns patterns = grid_.GetSortedPatterns();
    
    cout << "Looking for up to " << max_solutions << " best solutions..." << endl;
    cout << "Minimum quality threshold: " << min_quality << endl;
    
    // Track start time for time limit
    auto start_time = chrono::high_resolution_clock::now();
    bool time_limit_reached = false;
    
    // Start the recursive solving process
    SolveRecursiveBestN(patterns, 0, min_quality, start_time, max_time_seconds, time_limit_reached);
    
    if (time_limit_reached) {
      cout << "Time limit reached. Stopping search." << endl;
    }
    
    // Get the best solutions
    auto solutions = solution_tracker_.GetBestSolutions();
    
    cout << "Found " << solutions.size() << " solutions" << endl;
    return solutions;
  }
  
private:
  // ... existing methods ...
  
  // Recursive solving function that maintains best N solutions
  bool SolveRecursiveBestN(const Patterns& patterns, size_t index, 
                          double min_quality,
                          const chrono::high_resolution_clock::time_point& start_time,
                          int max_time_seconds,
                          bool& time_limit_reached) {
    // Check time limit if specified
    if (max_time_seconds > 0) {
      auto current_time = chrono::high_resolution_clock::now();
      auto elapsed = chrono::duration_cast<chrono::seconds>(current_time - start_time);
      
      if (elapsed.count() >= max_time_seconds) {
        time_limit_reached = true;
        return false;
      }
    }
    
    // Base case: we've filled all patterns
    if (index >= patterns.size()) {
      // Found a complete solution - score it
      double score = GridScorer::ScoreGrid(grid_, lib_);
      
      // Only consider solutions that meet the minimum quality
      if (score >= min_quality) {
        // Add to our solution tracker
        solution_tracker_.AddSolution(grid_, score);
        
        cout << "Found solution with score: " << score 
             << " (current threshold: " << solution_tracker_.GetQualificationThreshold() << ")" << endl;
      }
      
      // Continue searching for more solutions
      return false;
    }
    
    // Get the current pattern to fill
    const Pattern& current = patterns[index];
    
    // If the pattern is already filled, move to the next one
    if (grid_.IsSpanFilled(current.span)) {
      return SolveRecursiveBestN(patterns, index + 1, min_quality, 
                                start_time, max_time_seconds, time_limit_reached);
    }
    
    // Find candidate words for this pattern
    vector<string> candidates = FindCandidateWords(current);
    
    // Try each candidate
    for (const string& word : candidates) {
      // If time limit reached, stop exploring
      if (time_limit_reached) {
        return false;
      }
      
      // Check for duplicates and other constraints
      // ... (existing duplicate checking logic) ...
      
      // Place the word in the grid
      bool success = grid_.PlaceWord(current.span, word, allow_duplicates_);
      
      if (success) {
        // Quick check if a full solution with this partial solution could qualify
        // This is an optimization to prune unproductive branches
        if (index > patterns.size() / 2) {  // Only estimate for significantly filled grids
          double partial_score = GridScorer::EstimatePartialGridScore(grid_, lib_);
          double qualification_threshold = solution_tracker_.GetQualificationThreshold();
          
          // If we have a full set of solutions and this partial solution
          // doesn't look promising, skip it
          if (solution_tracker_.Size() >= solution_tracker_.GetMaxSolutions() &&
              partial_score < qualification_threshold * 0.9) {  // 10% margin for error
            grid_.RemoveWord(current.span);
            continue;
          }
        }
        
        // Recursively try to solve the rest of the grid
        SolveRecursiveBestN(patterns, index + 1, min_quality, 
                           start_time, max_time_seconds, time_limit_reached);
        
        // Backtrack
        grid_.RemoveWord(current.span);
      }
    }
    
    // If we tried all candidates and none worked, this is a dead end
    return false;
  }
  
  // ... existing members ...
  
  SolutionTracker solution_tracker_;  // Tracks the best N solutions
};
```

This implementation:
1. Uses our `SolutionTracker` to maintain the best N solutions
2. Adds support for a minimum quality threshold
3. Implements a time limit to stop searching after a set duration
4. Includes a branch pruning optimization based on partial grid scoring

#### Enhanced Grid Scoring

To support our optimization that estimates scores for partially filled grids, let's enhance our `GridScorer`:

```cpp
class GridScorer {
public:
  // ... existing methods ...
  
  // Estimate the potential score of a partially filled grid
  static double EstimatePartialGridScore(const Grid& grid, const Library& lib) {
    // Get placed words and their scores
    vector<pair<Span, string>> placed_words = grid.GetPlacedWords();
    double total_score = 0;
    double total_weight = 0;
    
    for (const auto& entry : placed_words) {
      const string& word = entry.second;
      double word_score = lib.GetWordQuality(word);
      total_score += word_score;
      total_weight += 1.0;
    }
    
    // Get unfilled spans
    vector<Span> unfilled_spans = grid.GetUnfilledSpans();
    
    // Estimate quality for unfilled spans (optimistically)
    for (const Span& span : unfilled_spans) {
      // Assume a moderately high quality for unfilled spans
      // This is optimistic but includes a discount for uncertainty
      total_score += 7.0;  // Assuming 10 is max quality
      total_weight += 1.0;
    }
    
    // Calculate weighted average
    return total_weight > 0 ? total_score / total_weight : 0;
  }
};
```

This method estimates the potential final score of a partially filled grid by:
1. Calculating the score of words already placed
2. Making an optimistic but reasonable estimate for unfilled spans
3. Computing a weighted average

#### Visualizing Multiple Solutions

Let's add a method to display multiple solutions side by side:

```cpp
void DisplayMultipleSolutions(const vector<pair<double, Grid>>& solutions,
                             const Library& lib,
                             int max_to_display = 3) {
  if (solutions.empty()) {
    cout << "No solutions to display." << endl;
    return;
  }
  
  int display_count = min(max_to_display, (int)solutions.size());
  
  cout << "Displaying top " << display_count << " solutions:" << endl << endl;
  
  // Display solution grids side by side
  vector<vector<string>> grid_lines(display_count);
  
  for (int i = 0; i < display_count; i++) {
    double score = solutions[i].first;
    const Grid& grid = solutions[i].second;
    
    // Get the grid lines
    grid_lines[i] = grid.GetLines();
    
    // Add header with score
    grid_lines[i].insert(grid_lines[i].begin(), 
                        "Solution " + to_string(i+1) + " (Score: " + 
                        to_string(score) + ")");
    grid_lines[i].insert(grid_lines[i].begin() + 1, string(grid_lines[i][0].length(), '-'));
  }
  
  // Find the maximum number of lines across all grids
  size_t max_lines = 0;
  for (const auto& lines : grid_lines) {
    max_lines = max(max_lines, lines.size());
  }
  
  // Display grids side by side
  for (size_t line_idx = 0; line_idx < max_lines; line_idx++) {
    for (int grid_idx = 0; grid_idx < display_count; grid_idx++) {
      // Get the current grid's lines
      const auto& lines = grid_lines[grid_idx];
      
      // Display the current line or spaces if this grid doesn't have this line
      if (line_idx < lines.size()) {
        cout << lines[line_idx];
      } else {
        cout << string(lines[0].length(), ' ');
      }
      
      // Add spacing between grids
      cout << "   ";
    }
    cout << endl;
  }
  
  cout << endl;
  
  // Display statistics for each solution
  for (int i = 0; i < display_count; i++) {
    double score = solutions[i].first;
    const Grid& grid = solutions[i].second;
    
    cout << "Solution " << (i+1) << " details:" << endl;
    cout << "  Score: " << score << endl;
    
    // Get word statistics
    map<int, int> quality_counts;  // Map of quality level to count
    auto placed_words = grid.GetPlacedWords();
    
    for (const auto& entry : placed_words) {
      const string& word = entry.second;
      int quality = lib.GetWordQuality(word);
      quality_counts[quality]++;
    }
    
    // Print quality distribution
    cout << "  Word quality distribution:" << endl;
    for (auto it = quality_counts.rbegin(); it != quality_counts.rend(); ++it) {
      cout << "    Quality " << it->first << ": " << it->second << " words" << endl;
    }
    
    cout << endl;
  }
}
```

This function creates a side-by-side visualization of multiple solutions along with their scores and word quality statistics.

#### Adding Solution Diversity

One challenge with maintaining only the highest-scoring solutions is that they might be very similar to each other. Let's add a method to ensure diversity among our solutions:

```cpp
class SolutionTracker {
public:
  // ... existing methods ...
  
  // Set diversity preference (higher values encourage more diverse solutions)
  void SetDiversityPreference(double preference) {
    diversity_preference_ = preference;
  }
  
  // Add a solution with diversity consideration
  bool AddSolutionWithDiversity(const Grid& grid, double score) {
    // If we have room, add normally
    if (solutions_.size() < max_solutions_) {
      solutions_[score] = grid;
      return true;
    }
    
    // Calculate similarity to existing solutions
    double max_similarity = CalculateMaxSimilarity(grid);
    
    // Adjust score based on diversity
    double adjusted_score = score - (max_similarity * diversity_preference_);
    
    // Check if this would qualify based on adjusted score
    auto last = --solutions_.end();
    if (adjusted_score > last->first) {
      // Remove the worst solution
      solutions_.erase(last);
      
      // Add the new solution with its original score
      // (we adjust for diversity during selection, but store the true score)
      solutions_[score] = grid;
      return true;
    }
    
    return false;
  }
  
private:
  // Calculate maximum similarity to any existing solution
  double CalculateMaxSimilarity(const Grid& grid) const {
    if (solutions_.empty()) {
      return 0.0;
    }
    
    double max_similarity = 0.0;
    
    // Get words from the new grid
    vector<string> new_words;
    for (const auto& entry : grid.GetPlacedWords()) {
      new_words.push_back(entry.second);
    }
    
    // Compare with each existing solution
    for (const auto& entry : solutions_) {
      const Grid& existing_grid = entry.second;
      
      // Get words from the existing grid
      vector<string> existing_words;
      for (const auto& word_entry : existing_grid.GetPlacedWords()) {
        existing_words.push_back(word_entry.second);
      }
      
      // Calculate Jaccard similarity (intersection over union)
      double similarity = CalculateJaccardSimilarity(new_words, existing_words);
      max_similarity = max(max_similarity, similarity);
    }
    
    return max_similarity;
  }
  
  // Calculate Jaccard similarity between two sets of words
  double CalculateJaccardSimilarity(const vector<string>& words1, 
                                  const vector<string>& words2) const {
    // Count words in the intersection
    int intersection_count = 0;
    
    for (const string& word : words1) {
      if (find(words2.begin(), words2.end(), word) != words2.end()) {
        intersection_count++;
      }
    }
    
    // Calculate union size (|A|+|B|-|A∩B|)
    int union_count = words1.size() + words2.size() - intersection_count;
    
    // Return Jaccard index
    return union_count > 0 ? (double)intersection_count / union_count : 0.0;
  }
  
  SolutionMap solutions_;
  size_t max_solutions_;
  double diversity_preference_ = 0.0;  // How much to prefer diverse solutions
};
```

This enhancement:
1. Calculates the similarity between solutions using the Jaccard index
2. Adjusts scores based on similarity to existing solutions
3. Promotes diversity in the solution set when the diversity preference is high

#### Saving and Loading Solutions

Let's add functionality to save our best solutions to a file and load them later:

```cpp
class SolutionManager {
public:
  // Save solutions to a file
  static bool SaveSolutions(const string& filename, 
                          const vector<pair<double, Grid>>& solutions) {
    ofstream file(filename);
    if (!file.is_open()) {
      cerr << "Error: Could not open file for writing: " << filename << endl;
      return false;
    }
    
    // Write the number of solutions
    file << solutions.size() << endl;
    
    // Write each solution
    for (const auto& entry : solutions) {
      double score = entry.first;
      const Grid& grid = entry.second;
      
      // Write the score
      file << score << endl;
      
      // Write the grid dimensions
      file << grid.rows() << " " << grid.cols() << endl;
      
      // Write the grid content
      for (int r = 0; r < grid.rows(); r++) {
        file << grid.GetLine(r) << endl;
      }
      
      // Write placed words
      auto placed_words = grid.GetPlacedWords();
      file << placed_words.size() << endl;
      
      for (const auto& word_entry : placed_words) {
        const Span& span = word_entry.first;
        const string& word = word_entry.second;
        
        // Write span details and word
        file << span.point.row << " " << span.point.col << " " 
             << span.len << " " << span.vert << " " << word << endl;
      }
    }
    
    file.close();
    cout << "Saved " << solutions.size() << " solutions to " << filename << endl;
    return true;
  }
  
  // Load solutions from a file
  static vector<pair<double, Grid>> LoadSolutions(const string& filename) {
    vector<pair<double, Grid>> solutions;
    
    ifstream file(filename);
    if (!file.is_open()) {
      cerr << "Error: Could not open file for reading: " << filename << endl;
      return solutions;
    }
    
    // Read the number of solutions
    int num_solutions;
    file >> num_solutions;
    
    // Read each solution
    for (int i = 0; i < num_solutions; i++) {
      double score;
      int rows, cols;
      
      // Read score and dimensions
      file >> score >> rows >> cols;
      file.ignore(); // Skip newline
      
      // Create a grid
      Grid grid("Loaded Solution");
      
      // Read grid content
      vector<string> lines;
      for (int r = 0; r < rows; r++) {
        string line;
        getline(file, line);
        lines.push_back(line);
      }
      
      grid.SetLines(lines);
      
      // Read placed words
      int num_words;
      file >> num_words;
      
      for (int w = 0; w < num_words; w++) {
        int row, col, len;
        bool vert;
        string word;
        
        file >> row >> col >> len >> vert >> word;
        
        // Add the word to the grid
        Span span(Point(row, col), len, vert);
        grid.PlaceWord(span, word);
      }
      
      // Add to solutions
      solutions.push_back(make_pair(score, grid));
    }
    
    file.close();
    cout << "Loaded " << solutions.size() << " solutions from " << filename << endl;
    return solutions;
  }
};
```

This `SolutionManager` class provides methods to:
1. Save a collection of solutions to a file, including their scores and word placements
2. Load solutions from a file, reconstructing the grids and score information

#### Putting It All Together

Let's combine all these enhancements into our program:

```cpp
int main() {
  // Load library
  Library lib;
  lib.ReadFromFile("top_12000.txt", "word_frequencies.txt");
  
  // Load grid
  Grid grid("Crossword Puzzle");
  grid.LoadFromFile("test.txt");
  
  // Create solver
  Solver solver(grid, lib);
  solver.SetQualityPreference(2.0);  // Prefer high-quality words
  
  // Set up solution tracker with diversity preference
  solver.SetDiversityPreference(0.3);  // Moderate diversity preference
  
  // Find the best solutions with time limit
  cout << "Searching for best solutions (max 30 seconds)..." << endl;
  auto solutions = solver.SolveBestN(5, 6.0, 30);  // Up to 5 solutions, min quality 6.0, 30 second time limit
  
  // Display the solutions
  DisplayMultipleSolutions(solutions, lib);
  
  // Save solutions
  SolutionManager::SaveSolutions("best_solutions.txt", solutions);
  
  // Load and display saved solutions
  auto loaded_solutions = SolutionManager::LoadSolutions("best_solutions.txt");
  cout << "Loaded solutions:" << endl;
  DisplayMultipleSolutions(loaded_solutions, lib);
  
  return 0;
}
```

#### Performance Considerations

The ordered map approach has several performance implications:

1. **Insertion Complexity**: Inserting into a `std::map` is O(log n), making it efficient even with many solutions.

2. **Dynamic Pruning**: As we collect good solutions, the qualification threshold rises, allowing us to prune more solution paths early.

3. **Memory Usage**: We only store the best N solutions, keeping memory usage reasonable.

4. **Diversity vs. Quality**: The diversity preference allows trading off between pure quality and solution variety.

#### Conclusion

In this chapter, we've significantly enhanced our crossword puzzle solver with the ability to efficiently track and manage multiple high-quality solutions:

1. **Ordered Map**: We've implemented a solution tracker using ordered maps to automatically maintain the best N solutions.

2. **Solution Diversity**: We've added mechanisms to promote diversity among our solutions, preventing near-duplicates.

3. **Optimization Techniques**: We've implemented early pruning of unproductive solution paths based on partial grid scoring.

4. **Time Management**: We've added support for time limits to prevent excessively long searches.

5. **Persistence**: We've created functionality to save and load solutions for later use.

These enhancements transform our solver into a comprehensive crossword construction tool that can generate multiple high-quality options, balancing word quality with solution diversity. This approach gives puzzle constructors and editors the flexibility to choose solutions that best meet their needs, whether for publication, education, or entertainment.

#### Practice Exercises

1. Implement a graphical user interface that allows browsing and editing the best solutions.

2. Create a system that automatically extracts potential clues for the words in each solution.

3. Enhance the diversity calculation to consider word semantics, not just exact matches.

4. Implement a solution rating system that allows users to provide feedback on solution quality.

5. Add support for puzzle themes by giving bonus points to solutions containing words related to a specific topic.

### 23. Finding islands
### 23. Finding islands

In this chapter, we'll enhance our crossword puzzle solver with the ability to detect and handle "islands" - isolated regions in the grid that aren't connected to the rest of the puzzle. Identifying islands is crucial for constructing high-quality crossword puzzles, as standard crosswords should consist of a single connected region with no isolated words or sections.

#### Understanding Islands in Crossword Puzzles

In the context of crossword puzzles, an "island" refers to a section of the grid that is completely separated from the rest by black squares (blocks). For example:

```
.WORD....
.O......
.R......
.D......
........
....DOG.
....O...
....G...
```

In this grid, "WORD" and "DOG" form two separate islands - they have no connecting white squares, meaning a solver would have to solve them independently.

Most published crossword puzzles avoid islands for several reasons:
1. They create disconnected solving experiences
2. They make the puzzle feel like multiple mini-puzzles
3. They reduce the satisfaction of making progress through connected words

#### Detecting Islands with Flood Fill

We'll use a classic algorithm called "flood fill" to detect islands. This algorithm works by:
1. Starting from a white cell (non-block)
2. Exploring all connected white cells
3. Marking all visited cells
4. Repeating from an unmarked white cell if any remain

Each time we need to start a new flood fill, we've found a separate island.

Let's implement island detection in our Grid class:

```cpp
class Grid {
public:
  // ... existing methods ...
  
  // Find all islands in the grid
  vector<vector<Point>> FindIslands() const {
    vector<vector<Point>> islands;
    
    // Create a visited flag grid
    vector<vector<bool>> visited(rows(), vector<bool>(cols(), false));
    
    // Mark all blocks as visited (we're only interested in non-block cells)
    for (int r = 0; r < rows(); r++) {
      for (int c = 0; c < cols(); c++) {
        if (is_block(Point(r, c))) {
          visited[r][c] = true;
        }
      }
    }
    
    // Find all islands using flood fill
    for (int r = 0; r < rows(); r++) {
      for (int c = 0; c < cols(); c++) {
        if (!visited[r][c]) {
          // Found an unvisited cell - start of a new island
          vector<Point> island;
          FloodFill(Point(r, c), visited, island);
          islands.push_back(island);
        }
      }
    }
    
    return islands;
  }
  
private:
  // Perform flood fill from a starting point
  void FloodFill(const Point& start, vector<vector<bool>>& visited, 
                vector<Point>& island) const {
    // Create a queue for BFS traversal
    queue<Point> q;
    q.push(start);
    visited[start.row][start.col] = true;
    island.push_back(start);
    
    // Define the four directions (up, right, down, left)
    const int dr[] = {-1, 0, 1, 0};
    const int dc[] = {0, 1, 0, -1};
    
    // BFS traversal
    while (!q.empty()) {
      Point current = q.front();
      q.pop();
      
      // Check all four adjacent cells
      for (int i = 0; i < 4; i++) {
        Point next(current.row + dr[i], current.col + dc[i]);
        
        // Check if the adjacent cell is valid and unvisited
        if (in_bounds(next) && !visited[next.row][next.col]) {
          visited[next.row][next.col] = true;
          island.push_back(next);
          q.push(next);
        }
      }
    }
  }
};
```

This implementation:
1. Creates a 2D grid of visited flags
2. Marks all blocks as already visited
3. Uses the flood fill algorithm to identify connected regions
4. Returns a list of islands, each represented as a collection of points

#### Visualizing Islands

Let's add a method to visualize the islands in a grid:

```cpp
void Grid::PrintWithIslands() const {
  // Find islands
  vector<vector<Point>> islands = FindIslands();
  
  // Create a grid for visualization
  vector<vector<char>> island_markers(rows(), vector<char>(cols(), ' '));
  
  // Assign a different marker for each island
  const string markers = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
  for (size_t i = 0; i < islands.size(); i++) {
    char marker = i < markers.length() ? markers[i] : '*';
    
    for (const Point& p : islands[i]) {
      island_markers[p.row][p.col] = marker;
    }
  }
  
  // Print the grid with island markers
  cout << "Grid with islands (" << islands.size() << " found):" << endl;
  
  for (int r = 0; r < rows(); r++) {
    // Print the original grid line
    cout << lines[r] << "   ";
    
    // Print the island markers
    for (int c = 0; c < cols(); c++) {
      cout << island_markers[r][c];
    }
    
    cout << endl;
  }
  
  // Print island statistics
  cout << endl << "Island statistics:" << endl;
  for (size_t i = 0; i < islands.size(); i++) {
    char marker = i < markers.length() ? markers[i] : '*';
    cout << "  Island " << marker << ": " << islands[i].size() << " cells" << endl;
  }
}
```

This method:
1. Identifies all islands in the grid
2. Assigns a unique letter marker to each island
3. Displays the grid with island markers
4. Provides statistics about each island's size

#### Island-Aware Grid Scoring

Now that we can detect islands, let's enhance our grid scoring to penalize puzzles with multiple islands:

```cpp
class GridScorer {
public:
  // ... existing methods ...
  
  // Score a grid, taking islands into account
  static double ScoreGridWithIslands(const Grid& grid, const Library& lib) {
    // Get base score from word quality
    double base_score = ScoreGrid(grid, lib);
    
    // Find islands
    vector<vector<Point>> islands = grid.FindIslands();
    
    // Apply island penalty
    double island_penalty = 0.0;
    if (islands.size() > 1) {
      // Severe penalty for multiple islands
      island_penalty = (islands.size() - 1) * 2.0;
    }
    
    return base_score - island_penalty;
  }
};
```

This approach:
1. Starts with the base score based on word quality
2. Applies a significant penalty for each additional island beyond the first

#### Island-Aware Solver

Let's update our Solver class to be aware of islands:

```cpp
class Solver {
public:
  // ... existing methods ...
  
  // Set whether to allow islands
  void SetAllowIslands(bool allow) {
    allow_islands_ = allow;
  }
  
  // Enhanced solution scoring taking islands into account
  double ScoreSolution(const Grid& grid) const {
    double score = GridScorer::ScoreGrid(grid, lib_);
    
    if (!allow_islands_) {
      // Find islands
      vector<vector<Point>> islands = grid.FindIslands();
      
      // Apply penalty for multiple islands
      if (islands.size() > 1) {
        score -= (islands.size() - 1) * 2.0;
      }
    }
    
    return score;
  }
  
private:
  // ... existing methods ...
  
  // Modified recursive solver that checks for islands
  bool SolveRecursiveWithIslandCheck(const Patterns& patterns, size_t index) {
    // Base case: we've filled all patterns
    if (index >= patterns.size()) {
      // Check for islands if required
      if (!allow_islands_) {
        vector<vector<Point>> islands = grid_.FindIslands();
        if (islands.size() > 1) {
          return false;  // Reject solutions with multiple islands
        }
      }
      
      return true;  // Valid solution
    }
    
    // ... rest of recursive solving logic ...
  }
  
  bool allow_islands_ = false;  // By default, don't allow islands
};
```

This enhancement:
1. Adds a configuration option to allow or disallow islands
2. Updates solution scoring to penalize islands when not allowed
3. Modifies the recursive solver to reject solutions with multiple islands

#### Early Detection of Potential Islands

Waiting until the grid is completely filled to check for islands can be inefficient. Let's implement a method to detect if a partially filled grid already has or will inevitably have islands:

```cpp
bool Grid::HasOrWillHaveIslands() const {
  // Create a grid that represents the connectivity potential
  // A cell is "connectable" if it's not a block
  vector<vector<bool>> connectable(rows(), vector<bool>(cols(), false));
  
  for (int r = 0; r < rows(); r++) {
    for (int c = 0; c < cols(); c++) {
      if (!is_block(Point(r, c))) {
        connectable[r][c] = true;
      }
    }
  }
  
  // Perform flood fill from the first connectable cell
  vector<vector<bool>> visited = connectable;  // Start with a copy
  bool found_first = false;
  Point start;
  
  // Find the first connectable cell
  for (int r = 0; r < rows() && !found_first; r++) {
    for (int c = 0; c < cols() && !found_first; c++) {
      if (connectable[r][c]) {
        start = Point(r, c);
        found_first = true;
      }
    }
  }
  
  if (!found_first) {
    return false;  // No connectable cells
  }
  
  // Perform flood fill
  vector<Point> dummy;  // We don't need to collect the points
  FloodFill(start, visited, dummy);
  
  // Check if there are unvisited connectable cells
  for (int r = 0; r < rows(); r++) {
    for (int c = 0; c < cols(); c++) {
      if (connectable[r][c] && !visited[r][c]) {
        return true;  // Found an unvisited connectable cell - there's an island
      }
    }
  }
  
  return false;  // No islands
}
```

This method:
1. Creates a grid of "connectable" cells (non-blocks)
2. Performs a flood fill from the first connectable cell
3. Checks if any connectable cells weren't visited during the flood fill
4. If unvisited connectable cells exist, the grid has or will have islands

#### Combining Island Detection with Recursive Solving

Now, let's integrate island detection into our recursive solver for early pruning:

```cpp
bool Solver::SolveRecursiveWithEarlyPruning(const Patterns& patterns, size_t index) {
  // Base case: we've filled all patterns
  if (index >= patterns.size()) {
    return true;  // Valid solution
  }
  
  // Early island detection (after placing a few words)
  if (!allow_islands_ && index > min(5, (int)patterns.size() / 3)) {
    if (grid_.HasOrWillHaveIslands()) {
      return false;  // This path will lead to islands
    }
  }
  
  // Get the current pattern to fill
  const Pattern& current = patterns[index];
  
  // ... rest of recursive solving logic ...
}
```

This modification checks for potential islands after placing a few words, allowing us to prune unproductive paths early in the solving process.

#### Island Bridging

Rather than simply rejecting solutions with islands, we might want to try to fix them by adding "bridges" - removing strategic black squares to connect isolated regions. Let's implement a method to suggest potential bridges:

```cpp
vector<Point> Grid::FindPotentialBridges() const {
  vector<Point> bridges;
  
  // Find islands
  vector<vector<Point>> islands = FindIslands();
  
  // If there's only one island or no islands, no bridges needed
  if (islands.size() <= 1) {
    return bridges;
  }
  
  // For each pair of islands, try to find the shortest possible bridge
  for (size_t i = 0; i < islands.size(); i++) {
    for (size_t j = i + 1; j < islands.size(); j++) {
      // Find the closest pair of cells between islands i and j
      Point best_bridge;
      int min_distance = INT_MAX;
      
      for (const Point& p1 : islands[i]) {
        for (const Point& p2 : islands[j]) {
          // Check if p1 and p2 are separated by exactly one block
          if (abs(p1.row - p2.row) + abs(p1.col - p2.col) == 2) {
            // Calculate the midpoint (potential bridge location)
            Point midpoint((p1.row + p2.row) / 2, (p1.col + p2.col) / 2);
            
            // Check if it's a block
            if (in_bounds(midpoint) && is_block(midpoint)) {
              // Calculate the "cost" of removing this block
              // (preference for bridges away from the edges)
              int edge_distance = min(midpoint.row, rows() - 1 - midpoint.row) + 
                                 min(midpoint.col, cols() - 1 - midpoint.col);
              
              if (edge_distance < min_distance) {
                min_distance = edge_distance;
                best_bridge = midpoint;
              }
            }
          }
        }
      }
      
      // If we found a potential bridge, add it to the list
      if (min_distance != INT_MAX) {
        bridges.push_back(best_bridge);
      }
    }
  }
  
  return bridges;
}
```

This method:
1. Identifies all islands in the grid
2. For each pair of islands, searches for cells that are separated by exactly one block
3. Prioritizes bridges that are away from grid edges
4. Returns a list of potential bridge locations (blocks that could be removed)

#### Implementing Automatic Island Fixing

Let's add a method to automatically fix islands by adding bridges:

```cpp
bool Grid::FixIslands() {
  // Find islands
  vector<vector<Point>> islands = FindIslands();
  
  // If there's only one island or no islands, nothing to fix
  if (islands.size() <= 1) {
    return false;  // No changes made
  }
  
  // Find potential bridges
  vector<Point> bridges = FindPotentialBridges();
  
  // If no bridges found, can't fix
  if (bridges.empty()) {
    return false;
  }
  
  // Apply bridges (remove blocks)
  for (const Point& bridge : bridges) {
    lines[bridge.row][bridge.col] = '-';  // Replace block with empty cell
  }
  
  // Check if we've fixed all islands
  islands = FindIslands();
  
  return islands.size() == 1;
}
```

This method:
1. Identifies islands in the grid
2. Finds potential bridges to connect them
3. Removes blocks to create bridges
4. Checks if the islands have been successfully connected

#### Putting It All Together

Now, let's integrate these island-handling capabilities into our main program:

```cpp
#include <iostream>
#include <queue>
#include <vector>
// ... other includes ...

// ... existing Point, Span, Pattern, Word, Library classes ...

// Enhanced Grid with island detection
class Grid {
public:
  // ... existing methods ...
  
  vector<vector<Point>> FindIslands() const;
  void PrintWithIslands() const;
  bool HasOrWillHaveIslands() const;
  vector<Point> FindPotentialBridges() const;
  bool FixIslands();
  
private:
  void FloodFill(const Point& start, vector<vector<bool>>& visited, 
                vector<Point>& island) const;
};

// Enhanced GridScorer with island awareness
class GridScorer {
public:
  // ... existing methods ...
  
  static double ScoreGridWithIslands(const Grid& grid, const Library& lib);
};

// Enhanced Solver with island handling
class Solver {
public:
  // ... existing methods ...
  
  void SetAllowIslands(bool allow);
  double ScoreSolution(const Grid& grid) const;
  
private:
  // ... existing methods ...
  
  bool SolveRecursiveWithIslandCheck(const Patterns& patterns, size_t index);
  bool SolveRecursiveWithEarlyPruning(const Patterns& patterns, size_t index);
  
  bool allow_islands_ = false;
};

int main() {
  // Load library
  Library lib;
  lib.ReadFromFile("top_12000.txt", "word_frequencies.txt");
  
  // Load grid
  Grid grid("Crossword Puzzle");
  grid.LoadFromFile("test.txt");
  
  // Display initial grid
  cout << "Initial grid:" << endl;
  grid.Print();
  
  // Check for islands
  cout << "Checking for islands..." << endl;
  grid.PrintWithIslands();
  
  // Try to fix islands
  cout << "Attempting to fix islands..." << endl;
  if (grid.FixIslands()) {
    cout << "Islands successfully fixed!" << endl;
    grid.PrintWithIslands();
  } else {
    cout << "Could not fix all islands automatically." << endl;
  }
  
  // Create solver
  Solver solver(grid, lib);
  solver.SetAllowIslands(false);  // Don't allow islands
  
  // Find the best solutions
  cout << "Finding the best solutions..." << endl;
  auto solutions = solver.SolveBestN(5, 6.0, 30);
  
  // Display the solutions
  DisplayMultipleSolutions(solutions, lib);
  
  return 0;
}
```

#### Performance Considerations

The island detection and handling features have several performance implications:

1. **Early Pruning**: By detecting potential islands early in the solving process, we can avoid exploring unproductive solution paths.

2. **Flood Fill Efficiency**: The flood fill algorithm is O(n) where n is the number of cells in the grid, making it very efficient.

3. **Bridge Finding**: The naive approach to finding bridges is O(n²) where n is the number of cells, but since the number of cells in an island is typically small, this remains practical.

#### Conclusion

In this chapter, we've enhanced our crossword puzzle solver with the ability to detect, visualize, and handle islands:

1. **Island Detection**: We've implemented efficient algorithms to identify isolated regions in the grid.

2. **Island Visualization**: We've added methods to visualize islands for easier understanding and debugging.

3. **Island-Aware Scoring**: We've enhanced our grid scoring to penalize puzzles with multiple islands.

4. **Early Pruning**: We've integrated island detection into our recursive solver for more efficient searching.

5. **Island Bridging**: We've implemented methods to automatically fix islands by adding bridges.

These enhancements ensure that our crossword puzzle solver produces high-quality puzzles that follow standard construction principles, with all words connected in a single cohesive puzzle. The ability to detect and fix islands also opens up possibilities for more creative grid designs while still maintaining connectivity.

#### Practice Exercises

1. Enhance the island bridging algorithm to consider the impact on potential word placements.

2. Implement a "relaxed connectivity" option that allows diagonal connections between cells.

3. Create a visual interface that allows users to manually add bridges between islands.

4. Implement an algorithm to identify the minimum number of bridges needed to connect all islands.

5. Add functionality to automatically adjust the grid size to eliminate islands while preserving existing word placements.

### 24. Partitions: finding, solving, and integrating
### 24. Partitions: finding, solving, and integrating

In this chapter, we'll tackle a powerful optimization technique for our crossword puzzle solver: partitioning. This approach identifies independent sections of the grid that can be solved separately and then combined, significantly improving performance for large or complex puzzles.

#### Understanding Partitions in Crossword Puzzles

A "partition" in a crossword puzzle is a section of the grid that can be filled independently of other sections. Unlike islands (which are completely disconnected), partitions may share boundaries but don't have intersecting words. For example:

```
.WORD....
.O......
.R.DOG...
.D.O.....
...G.....
.........
.........
.........
```

In this grid, "WORD" and "DOG" form two separate partitions - they share a boundary, but no words cross from one partition to the other.

Partitioning offers several advantages:
1. Each partition can be solved independently, reducing complexity
2. Smaller problems are exponentially faster to solve
3. Solutions from different partitions can be combined without conflicts

#### Detecting Partitions

To find partitions, we'll analyze how spans intersect with each other. Spans that interact (intersect directly or transitively) belong to the same partition.

Let's implement partition detection:

```cpp
class Grid {
public:
  // ... existing methods ...
  
  // Find all partitions in the grid
  vector<vector<Span>> FindPartitions() const {
    vector<vector<Span>> partitions;
    
    // Skip if no spans are defined
    if (spans.empty()) {
      return partitions;
    }
    
    // Create a graph where spans are nodes and intersections are edges
    vector<vector<size_t>> graph(spans.size());
    
    // Find all intersections between spans
    for (size_t i = 0; i < spans.size(); i++) {
      for (size_t j = i + 1; j < spans.size(); j++) {
        Point intersection;
        if (SpansIntersect(spans[i], spans[j], intersection)) {
          // Add edges in both directions
          graph[i].push_back(j);
          graph[j].push_back(i);
        }
      }
    }
    
    // Use BFS to find connected components (partitions)
    vector<bool> visited(spans.size(), false);
    
    for (size_t i = 0; i < spans.size(); i++) {
      if (!visited[i]) {
        // Start a new partition
        vector<Span> partition;
        queue<size_t> q;
        
        q.push(i);
        visited[i] = true;
        
        while (!q.empty()) {
          size_t current = q.front();
          q.pop();
          
          partition.push_back(spans[current]);
          
          // Add all unvisited neighbors
          for (size_t neighbor : graph[current]) {
            if (!visited[neighbor]) {
              q.push(neighbor);
              visited[neighbor] = true;
            }
          }
        }
        
        partitions.push_back(partition);
      }
    }
    
    return partitions;
  }
  
  // Visualize partitions
  void PrintWithPartitions() const {
    // Find partitions
    vector<vector<Span>> partitions = FindPartitions();
    
    // Create a grid for visualization
    vector<vector<char>> partition_markers(rows(), vector<char>(cols(), ' '));
    
    // Assign a different marker for each partition
    const string markers = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    
    for (size_t p = 0; p < partitions.size(); p++) {
      char marker = p < markers.length() ? markers[p] : '*';
      
      // Mark all cells in this partition's spans
      for (const Span& span : partitions[p]) {
        Point pos = span.point;
        
        for (int i = 0; i < span.len; i++) {
          partition_markers[pos.row][pos.col] = marker;
          
          // Move to next position
          if (span.vert) {
            pos.row++;
          } else {
            pos.col++;
          }
        }
      }
    }
    
    // Print the grid with partition markers
    cout << "Grid with partitions (" << partitions.size() << " found):" << endl;
    
    for (int r = 0; r < rows(); r++) {
      // Print the original grid line
      cout << lines[r] << "   ";
      
      // Print the partition markers
      for (int c = 0; c < cols(); c++) {
        cout << partition_markers[r][c];
      }
      
      cout << endl;
    }
    
    // Print partition statistics
    cout << endl << "Partition statistics:" << endl;
    for (size_t p = 0; p < partitions.size(); p++) {
      char marker = p < markers.length() ? markers[p] : '*';
      cout << "  Partition " << marker << ": " << partitions[p].size() << " spans" << endl;
    }
  }
};
```

This implementation:
1. Creates a graph where spans are nodes and intersections are edges
2. Uses breadth-first search to find connected components (partitions)
3. Returns a list of partitions, each containing a set of spans
4. Provides visualization to display the partitions

#### Partition-Aware Solver

Now let's enhance our Solver class to use partitioning:

```cpp
class PartitionSolver {
public:
  PartitionSolver(Grid& grid, Library& lib) 
    : grid_(grid), lib_(lib), solver_(grid, lib) {}
  
  // Solve using partitioning
  bool Solve() {
    // Find partitions
    vector<vector<Span>> partitions = grid_.FindPartitions();
    
    if (partitions.empty()) {
      cout << "No partitions found." << endl;
      return false;
    }
    
    cout << "Found " << partitions.size() << " partitions." << endl;
    
    // Create subgrids for each partition
    vector<Grid> subgrids;
    
    for (const auto& partition : partitions) {
      Grid subgrid = ExtractPartitionSubgrid(partition);
      subgrids.push_back(subgrid);
    }
    
    // Solve each subgrid
    vector<Grid> solved_subgrids;
    
    for (size_t i = 0; i < subgrids.size(); i++) {
      cout << "Solving partition " << (i + 1) << " of " << subgrids.size() << "..." << endl;
      
      // Create a solver for this subgrid
      Solver partition_solver(subgrids[i], lib_);
      partition_solver.SetQualityPreference(solver_.GetQualityPreference());
      partition_solver.SetAllowDuplicates(solver_.GetAllowDuplicates());
      
      // Solve the subgrid
      bool success = partition_solver.Solve();
      
      if (!success) {
        cout << "Failed to solve partition " << (i + 1) << endl;
        return false;
      }
      
      solved_subgrids.push_back(subgrids[i]);
    }
    
    // Combine the solved subgrids
    bool combined = CombineSolvedPartitions(solved_subgrids, partitions);
    
    if (!combined) {
      cout << "Failed to combine solved partitions." << endl;
      return false;
    }
    
    cout << "Successfully solved and combined all partitions." << endl;
    return true;
  }
  
private:
  // Extract a subgrid for a partition
  Grid ExtractPartitionSubgrid(const vector<Span>& partition) const {
    // Create a mask of cells in this partition
    vector<vector<bool>> mask(grid_.rows(), vector<bool>(grid_.cols(), false));
    
    // Mark all cells in the partition's spans
    for (const Span& span : partition) {
      Point pos = span.point;
      
      for (int i = 0; i < span.len; i++) {
        mask[pos.row][pos.col] = true;
        
        // Move to next position
        if (span.vert) {
          pos.row++;
        } else {
          pos.col++;
        }
      }
    }
    
    // Find the bounding box of the partition
    int min_row = grid_.rows();
    int min_col = grid_.cols();
    int max_row = 0;
    int max_col = 0;
    
    for (int r = 0; r < grid_.rows(); r++) {
      for (int c = 0; c < grid_.cols(); c++) {
        if (mask[r][c]) {
          min_row = min(min_row, r);
          min_col = min(min_col, c);
          max_row = max(max_row, r);
          max_col = max(max_col, c);
        }
      }
    }
    
    // Create a new grid for this partition
    Grid subgrid("Partition Subgrid");
    
    // Copy the relevant portion of the grid
    for (int r = min_row; r <= max_row; r++) {
      string line;
      
      for (int c = min_col; c <= max_col; c++) {
        if (mask[r][c]) {
          // This cell is part of the partition
          line.push_back(grid_.GetChar(Point(r, c)));
        } else {
          // This cell is not part of the partition - make it a block
          line.push_back('.');
        }
      }
      
      subgrid.AddLine(line);
    }
    
    // Calculate spans for the subgrid
    subgrid.FillSpans();
    
    return subgrid;
  }
  
  // Combine solved partitions back into the main grid
  bool CombineSolvedPartitions(const vector<Grid>& solved_subgrids, 
                              const vector<vector<Span>>& partitions) {
    // For each partition and its solved subgrid
    for (size_t p = 0; p < solved_subgrids.size(); p++) {
      const Grid& subgrid = solved_subgrids[p];
      const vector<Span>& partition = partitions[p];
      
      // Create a mapping from original spans to subgrid spans
      map<pair<int, int>, pair<int, int>> span_mapping;
      
      // Find bounding box of this partition
      // ... (similar to ExtractPartitionSubgrid) ...
      
      // Map each original span to its corresponding span in the subgrid
      // ... (calculate offset mapping) ...
      
      // Get placed words from the solved subgrid
      auto placed_words = subgrid.GetPlacedWords();
      
      // Place each word in the main grid
      for (const auto& entry : placed_words) {
        const Span& subgrid_span = entry.first;
        const string& word = entry.second;
        
        // Convert to the corresponding span in the main grid
        // ... (apply mapping) ...
        
        // Place the word in the main grid
        grid_.PlaceWord(main_grid_span, word);
      }
    }
    
    return true;
  }
  
  Grid& grid_;
  Library& lib_;
  Solver solver_;  // Reference solver for settings
};
```

This implementation:
1. Identifies partitions in the grid
2. Creates a subgrid for each partition
3. Solves each subgrid independently
4. Combines the solutions back into the main grid

#### Handling Partition Extraction and Combination

Let's enhance our implementation with more details for extracting and combining partitions:

```cpp
Grid ExtractPartitionSubgrid(const vector<Span>& partition) const {
  // Create a mask of cells in this partition
  vector<vector<bool>> mask(grid_.rows(), vector<bool>(grid_.cols(), false));
  
  // Mark all cells in the partition's spans
  for (const Span& span : partition) {
    Point pos = span.point;
    
    for (int i = 0; i < span.len; i++) {
      mask[pos.row][pos.col] = true;
      
      // Move to next position
      if (span.vert) {
        pos.row++;
      } else {
        pos.col++;
      }
    }
  }
  
  // Find the bounding box of the partition
  int min_row = grid_.rows();
  int min_col = grid_.cols();
  int max_row = 0;
  int max_col = 0;
  
  for (int r = 0; r < grid_.rows(); r++) {
    for (int c = 0; c < grid_.cols(); c++) {
      if (mask[r][c]) {
        min_row = min(min_row, r);
        min_col = min(min_col, c);
        max_row = max(max_row, r);
        max_col = max(max_col, c);
      }
    }
  }
  
  // Add a one-cell border around the partition if possible
  min_row = max(0, min_row - 1);
  min_col = max(0, min_col - 1);
  max_row = min(grid_.rows() - 1, max_row + 1);
  max_col = min(grid_.cols() - 1, max_col + 1);
  
  // Create a new grid for this partition
  Grid subgrid("Partition Subgrid");
  
  // Copy the relevant portion of the grid
  for (int r = min_row; r <= max_row; r++) {
    string line;
    
    for (int c = min_col; c <= max_col; c++) {
      if (mask[r][c]) {
        // This cell is part of the partition
        line.push_back(grid_.GetChar(Point(r, c)));
      } else {
        // This cell is not part of the partition - make it a block
        line.push_back('.');
      }
    }
    
    subgrid.AddLine(line);
  }
  
  // Calculate spans for the subgrid
  subgrid.FillSpans();
  
  // Store the offset for later reconstruction
  subgrid.SetOffsets(min_row, min_col);
  
  return subgrid;
}

bool CombineSolvedPartitions(const vector<Grid>& solved_subgrids, 
                            const vector<vector<Span>>& partitions) {
  // For each partition and its solved subgrid
  for (size_t p = 0; p < solved_subgrids.size(); p++) {
    const Grid& subgrid = solved_subgrids[p];
    
    // Get offsets from subgrid
    int row_offset = subgrid.GetRowOffset();
    int col_offset = subgrid.GetColOffset();
    
    // Get placed words from the solved subgrid
    auto placed_words = subgrid.GetPlacedWords();
    
    // Place each word in the main grid
    for (const auto& entry : placed_words) {
      const Span& subgrid_span = entry.first;
      const string& word = entry.second;
      
      // Convert to the corresponding span in the main grid
      Point main_grid_point(
        subgrid_span.point.row + row_offset,
        subgrid_span.point.col + col_offset
      );
      
      Span main_grid_span(main_grid_point, subgrid_span.len, subgrid_span.vert);
      
      // Place the word in the main grid
      bool success = grid_.PlaceWord(main_grid_span, word);
      
      if (!success) {
        cerr << "Failed to place word '" << word << "' in main grid." << endl;
        return false;
      }
    }
  }
  
  return true;
}
```

These enhanced methods handle the details of extracting subgrids with proper offsets and combining the solved subgrids back into the main grid.

#### Performance Analysis

Let's analyze the performance benefits of partitioning:

```cpp
void PerformanceAnalysis(const string& grid_file, const string& dict_file) {
  // Load library and grid
  Library lib;
  lib.ReadFromFile(dict_file);
  
  Grid grid("Performance Test");
  grid.LoadFromFile(grid_file);
  
  // Find partitions
  vector<vector<Span>> partitions = grid.FindPartitions();
  
  if (partitions.size() <= 1) {
    cout << "Grid has only one partition. No performance comparison possible." << endl;
    return;
  }
  
  cout << "Found " << partitions.size() << " partitions." << endl;
  
  // Regular solver
  Solver regular_solver(grid, lib);
  
  // Partition solver
  PartitionSolver partition_solver(grid, lib);
  
  // Measure regular solver performance
  cout << "Solving with regular solver..." << endl;
  auto start1 = chrono::high_resolution_clock::now();
  bool success1 = regular_solver.Solve();
  auto end1 = chrono::high_resolution_clock::now();
  
  auto duration1 = chrono::duration_cast<chrono::milliseconds>(end1 - start1);
  
  // Reset the grid
  grid.ClearAllWords();
  
  // Measure partition solver performance
  cout << "Solving with partition solver..." << endl;
  auto start2 = chrono::high_resolution_clock::now();
  bool success2 = partition_solver.Solve();
  auto end2 = chrono::high_resolution_clock::now();
  
  auto duration2 = chrono::duration_cast<chrono::milliseconds>(end2 - start2);
  
  // Print results
  cout << "Performance results:" << endl;
  cout << "  Regular solver: " << duration1.count() << " ms (" 
       << (success1 ? "success" : "failure") << ")" << endl;
  cout << "  Partition solver: " << duration2.count() << " ms (" 
       << (success2 ? "success" : "failure") << ")" << endl;
  
  if (success1 && success2) {
    double speedup = (double)duration1.count() / duration2.count();
    cout << "  Speedup: " << speedup << "x" << endl;
  }
}
```

The performance benefits of partitioning can be dramatic:
1. If a grid has P partitions of roughly equal size, the complexity can be reduced from O(n^P) to O(P * n).
2. Even with just 2-3 partitions, we might see order-of-magnitude speedups.
3. Some grids that would be practically unsolvable as a whole become easily solvable with partitioning.

#### Advanced Partition Analysis

For more sophisticated puzzles, we might want to analyze the characteristics of different partitions:

```cpp
void AnalyzePartitions(const Grid& grid) {
  // Find partitions
  vector<vector<Span>> partitions = grid.FindPartitions();
  
  cout << "Partition Analysis:" << endl;
  cout << "  Total partitions: " << partitions.size() << endl;
  
  if (partitions.empty()) {
    return;
  }
  
  // Analyze each partition
  for (size_t p = 0; p < partitions.size(); p++) {
    const vector<Span>& partition = partitions[p];
    
    cout << "  Partition " << (p + 1) << ":" << endl;
    cout << "    Spans: " << partition.size() << endl;
    
    // Count horizontal and vertical spans
    int horizontal = 0;
    int vertical = 0;
    
    for (const Span& span : partition) {
      if (span.vert) {
        vertical++;
      } else {
        horizontal++;
      }
    }
    
    cout << "    Horizontal spans: " << horizontal << endl;
    cout << "    Vertical spans: " << vertical << endl;
    
    // Analyze span lengths
    map<int, int> length_counts;
    
    for (const Span& span : partition) {
      length_counts[span.len]++;
    }
    
    cout << "    Span length distribution:" << endl;
    for (const auto& entry : length_counts) {
      cout << "      Length " << entry.first << ": " << entry.second << " spans" << endl;
    }
    
    // Calculate density (ratio of filled cells to total cells in bounding box)
    // ... (calculate partition bounding box and density) ...
    
    cout << endl;
  }
}
```

This analysis helps understand the characteristics of different partitions, which can guide solver optimizations.

#### Handling Overlapping Partitions

In some cases, we might have "soft partitions" that share some spans. These can be handled by solving partitions in sequence, preserving shared spans:

```cpp
bool SolveOverlappingPartitions(Grid& grid, Library& lib) {
  // Find all spans
  if (grid.spans.empty()) {
    grid.FillSpans();
  }
  
  // Create an adjacency graph of spans
  vector<vector<size_t>> graph(grid.spans.size());
  
  // Find all intersections between spans
  for (size_t i = 0; i < grid.spans.size(); i++) {
    for (size_t j = i + 1; j < grid.spans.size(); j++) {
      Point intersection;
      if (grid.SpansIntersect(grid.spans[i], grid.spans[j], intersection)) {
        // Add edges in both directions
        graph[i].push_back(j);
        graph[j].push_back(i);
      }
    }
  }
  
  // Calculate span "connectivity" (how many other spans it intersects)
  vector<int> connectivity(grid.spans.size());
  
  for (size_t i = 0; i < graph.size(); i++) {
    connectivity[i] = graph[i].size();
  }
  
  // Find cut points in the graph (spans that, when removed, create partitions)
  // ... (advanced graph algorithm) ...
  
  // Solve partitions in sequence, preserving shared spans
  // ... (sequential solving with constraints) ...
  
  return true;
}
```

This advanced approach can handle more complex grids with overlapping partitions.

#### Putting It All Together

Let's integrate partitioning into our main program:

```cpp
#include <chrono>
#include <iostream>
#include <map>
#include <queue>
#include <vector>
// ... other includes ...

// ... existing Point, Span, Pattern, Word, Library classes ...

// Enhanced Grid with partition detection
class Grid {
public:
  // ... existing methods ...
  
  vector<vector<Span>> FindPartitions() const;
  void PrintWithPartitions() const;
  void SetOffsets(int row_offset, int col_offset);
  int GetRowOffset() const;
  int GetColOffset() const;
  
private:
  // ... existing members ...
  
  int row_offset_ = 0;
  int col_offset_ = 0;
};

// Partition solver
class PartitionSolver {
public:
  PartitionSolver(Grid& grid, Library& lib);
  bool Solve();
  
private:
  Grid ExtractPartitionSubgrid(const vector<Span>& partition) const;
  bool CombineSolvedPartitions(const vector<Grid>& solved_subgrids, 
                              const vector<vector<Span>>& partitions);
  
  Grid& grid_;
  Library& lib_;
  Solver solver_;
};

int main() {
  // Load library
  Library lib;
  lib.ReadFromFile("top_12000.txt");
  
  // Load grid
  Grid grid("Crossword Puzzle");
  grid.LoadFromFile("test.txt");
  
  // Display initial grid
  cout << "Initial grid:" << endl;
  grid.Print();
  
  // Check for partitions
  cout << "Checking for partitions..." << endl;
  grid.PrintWithPartitions();
  
  // Analyze partitions
  AnalyzePartitions(grid);
  
  // Create solvers
  Solver regular_solver(grid, lib);
  PartitionSolver partition_solver(grid, lib);
  
  // Choose solver based on partition count
  vector<vector<Span>> partitions = grid.FindPartitions();
  
  if (partitions.size() > 1) {
    cout << "Using partition solver..." << endl;
    bool success = partition_solver.Solve();
    cout << "Solution " << (success ? "found" : "not found") << endl;
  } else {
    cout << "Using regular solver..." << endl;
    bool success = regular_solver.Solve();
    cout << "Solution " << (success ? "found" : "not found") << endl;
  }
  
  // Display the solution
  grid.Print();
  
  // Run performance analysis
  PerformanceAnalysis("test.txt", "top_12000.txt");
  
  return 0;
}
```

#### Conclusion

In this chapter, we've enhanced our crossword puzzle solver with partitioning capabilities:

1. **Partition Detection**: We've implemented algorithms to identify independent sections of the grid.

2. **Subgrid Extraction**: We've created methods to extract and solve partitions as separate puzzles.

3. **Solution Integration**: We've developed techniques to combine solutions from different partitions.

4. **Performance Analysis**: We've analyzed the significant speedups that partitioning can provide.

5. **Advanced Partition Handling**: We've explored techniques for analyzing and handling more complex partition scenarios.

Partitioning represents a powerful optimization that can make previously unsolvable puzzles solvable and dramatically improve performance for large grids. By breaking the problem into smaller, independent parts, we leverage the divide-and-conquer approach that is fundamental to many efficient algorithms.

#### Practice Exercises

1. Implement a visualization that shows the solving process for each partition in sequence.

2. Enhance the partitioning algorithm to identify "weak links" that could be broken to create more partitions.

3. Create a heuristic that decides whether to use partitioning based on grid characteristics.

4. Implement parallel solving of partitions using multiple threads.

5. Develop a hybrid approach that combines partitioning with other optimizations like word quality scoring and duplicate prevention.

### 25. More efficient incremental state change in recursion


### 26. Recursion limits based on cpu and tree size
### 27. Slot selection policy
### 28. Grid composition (designing "block" black squares)
### 29. Theme entry position permutations
### 30. Screening templates
