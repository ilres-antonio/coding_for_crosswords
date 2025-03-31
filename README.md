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


### 13. Points and Spans
[https://youtu.be/7uS0hrpERcY](https://youtu.be/7uS0hrpERcY)


### 14. Find Spans in the Grid
[https://youtu.be/_LlUZLRsxcU](https://youtu.be/_LlUZLRsxcU)


### 15. Get Strings from the Grid
[https://youtu.be/IyqaPP-I6UQ](https://youtu.be/IyqaPP-I6UQ)


### 16. Solver Class
[https://youtu.be/b05M5oPZGgc](https://youtu.be/b05M5oPZGgc)


### 17. Write Words to the Grid
[https://youtu.be/fFqyXMxfMVE](https://youtu.be/fFqyXMxfMVE)


### 18. Preventing Duplicates
[https://youtu.be/AIjy3TcH924](https://youtu.be/AIjy3TcH924)



