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
### 2a. Setup C++ for Windows
[https://youtu.be/Rov1Hm14ZoY](https://youtu.be/Rov1Hm14ZoY)
### 3. Add 1 plus 1!
[https://youtu.be/Wf5mfSYXdZg](https://youtu.be/Wf5mfSYXdZg)
### 4. Load a Grid (part 1)
[https://youtu.be/Gs7H9GOZjow](https://youtu.be/Gs7H9GOZjow)
### 5. Load a Grid (part 2)
[https://youtu.be/aMBiDC-Az-c](https://youtu.be/aMBiDC-Az-c)
```cpp=
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

        //for (int i = 0; i < grid.size(); i++) {

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
### 6. The Grid Object
[https://youtu.be/aJELHElkBTo](https://youtu.be/aJELHElkBTo)
```cpp=
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

};
```
### 7. Read the Grid from a File
[https://youtu.be/mibylIzx_sE](https://youtu.be/mibylIzx_sE)

```cpp=
int aa = 'A';
// single quote returns int, in these case 65
```

Carriage Return representation in some OS:

- Windows: `'\r\n'`
- Mac (OS 9-): `'\r'`
- Mac (OS 10+): `'\n'`
- Unix/Linux: `'\n'`

`ifstream f; // return n lines + one empty`

```cpp=
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>
#include <fstream>

using namespace std;

struct Grid
{

    Grid(string n)
    {
        name = n;
    }

    int rows() const { return lines.size(); }

    int cols() const
    {

        if (lines.empty())
        {
            return 0;
        }
        else
        {
            return lines[0].size();
        }
    }

    void LoadFromFile(string filename)
    {
        ifstream f;
        f.open(filename);
        while (!f.eof())
        {
            string line;
            getline(f, line);
            // cout << line << "   (" << line.length() << ")" << endl;
            if (!line.empty() && line[0] != '#')
            {
                lines.push_back(line);
            }
        }
        f.close();

        // lines.pop_back();
    }

    int Check() const
    {

        for (string s : lines)
        {
            assert(s.size() == cols());
        }
        return 0;
    }
    int Print() const
    {

        cout << "Grid : " << name << endl
             << endl;

        for (string s : lines)
        {
            cout << s << endl;
        }

        cout << endl
             << "Rows : " << rows() << endl;
        cout << "Columns : " << cols() << endl;

        return 0;
    }

    vector<string> lines;
    string name;
};

int main()
{
    Grid grid("MY GRID");

    grid.LoadFromFile("test.txt");
    grid.Check();
    grid.Print();
};

```
### 8. Read the Library from a File
[https://youtu.be/xxQWf-60hI8 ](https://youtu.be/xxQWf-60hI8 )

`struct` keyword declaration, everything inside is public.

`class` keyword declaration, everything inside is private.

```cpp=
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>
#include <fstream>

using namespace std;

class Library
{
public:
    void ComputeStats()
    {
        assert(counts.empty());
        // resize vector that don't grow in time
        // vector initialized to 0
        counts.resize(18);
        for (string s : words)
        {
            int len = s.length();
            if (len < 18)
            {
                counts[len]++;
            }
        }
    }

    void PrintStats() const
    {
        for (int i = 1; i < counts.size(); i++)
        {
            cout << counts[i] << " words of " << i << " character(s) " << endl;
        }
    }

    string GetWord(int i) const
    {
        assert(i >= 0 && i < words.size());
        return words[i];
    }

    void ReadFromFile(string filename)
    {
        ifstream f;
        f.open(filename);
        while (!f.eof())
        {
            string line;
            getline(f, line);
            // cout << line << "   (" << line.length() << ")" << endl;
            if (!line.empty())
            {
                int len = line.length();
                if (line[len - 1] == '\r')
                {
                    line = line.substr(0, len - 1);
                }
                words.push_back(line);
            }
        }

        cout << words[0] << endl;
        cout << words[0].length() << endl;
        for (char c : words[0])
        {
            int x = c;
            cout << c << " " << x << endl;
        }

        f.close();

        cout << "Read " << words.size() << " words from file '" << filename << "'" << endl;
    }

private:
    vector<string> words;
    vector<int> counts;
};

struct Grid
{

    Grid(string n)
    {
        name = n;
    }

    int rows() const { return lines.size(); }

    int cols() const
    {

        if (lines.empty())
        {
            return 0;
        }
        else
        {
            return lines[0].size();
        }
    }

    void LoadFromFile(string filename)
    {
        ifstream f;
        f.open(filename);
        while (!f.eof())
        {
            string line;
            getline(f, line);
            // cout << line << "   (" << line.length() << ")" << endl;
            if (!line.empty() && line[0] != '#')
            {
                lines.push_back(line);
            }
        }
        f.close();

        // lines.pop_back();
    }

    int Check() const
    {

        for (string s : lines)
        {
            assert(s.size() == cols());
        }
        return 0;
    }
    int Print() const
    {

        cout << "Grid : " << name << endl
             << endl;

        for (string s : lines)
        {
            cout << s << endl;
        }

        cout << endl
             << "Rows : " << rows() << endl;
        cout << "Columns : " << cols() << endl;

        return 0;
    }

    vector<string> lines;
    string name;
};

int main()
{

    Library lib;

    lib.ReadFromFile("top_12000.txt");

    cout << lib.GetWord(876) << endl;

    lib.ComputeStats();
    lib.PrintStats();

    // Grid grid("MY GRID");

    // grid.LoadFromFile("test.txt");
    // grid.Check();
    // grid.Print();
};
```

### 9. Search the Library
[https://youtu.be/s-0j5KZ92-E ](https://youtu.be/s-0j5KZ92-E )

```cpp=
#include <iostream>
#include <string>
#include <vector>
#include <assert.h>
#include <fstream>

using namespace std;

string ToUpper(string s)
{
    string s2;

    for (char c : s)
    {
        s2.push_back(toupper(c));
    }
    return s2;
};

struct Word
{
    Word(string s)
    {
        word = s;
    }
    string word;
};
typedef vector<Word> Words;

const int num_buckets = 1001;

int bucket(string s)
{
    assert(!s.empty());
    unsigned int i = 0;
    for (char c : s)
    {
        i = (i * 217) + c;
    }
    int b = i % num_buckets;

    assert(b >= 0 && b < num_buckets);
    return b;
};

class Library
{
public:
    Library()
    {
        shelves.resize(num_buckets);
    }

    bool IsWord(string s) const
    {
        cout << "bucket is " << bucket(s) << endl;
        for (Word w : shelves[bucket(s)])
        {
            if (s == w.word)
            {
                return true;
            }
        }
        return false;
    }

    void ComputeStats()
    {
        assert(counts.empty());
        // resize vector that don't grow in time
        // vector initialized to 0
        counts.resize(18);
        for (Word w : words)
        {
            int len = w.word.length();
            if (len < 18)
            {
                counts[len]++;
            }
        }
    }

    void PrintStats() const
    {
        for (int i = 1; i < counts.size(); i++)
        {
            cout << counts[i] << " words of " << i << " character(s) " << endl;
        }
    }

    string GetWord(int i) const
    {
        assert(i >= 0 && i < words.size());
        return words[i].word;
    }

    void ReadFromFile(string filename)
    {
        ifstream f;
        f.open(filename);
        while (!f.eof())
        {
            string line;
            getline(f, line);
            // cout << line << "   (" << line.length() << ")" << endl;
            if (!line.empty())
            {
                line = ToUpper(line);
                int len = line.length();
                if (line[len - 1] == '\r')
                {
                    line = line.substr(0, len - 1);
                }
                words.push_back(Word(line));
                shelves[bucket(line)].push_back(Word(line));
            }
        }

        // cout << words[0].word << endl;
        // cout << words[0].word.length() << endl;
        for (char c : words[0].word)
        {
            int x = c;
            // cout << c << " " << x << endl;
        }

        f.close();

        cout << "Read " << words.size() << " words from file '" << filename << "'" << endl;
    }

    void DebugBuckets() const
    {
        for (int i = 0; i < shelves.size(); i++)
        {
            cout << "[" << i << "] " << shelves[i].size() << endl;
        };
    }

private:
    Words words;
    vector<Words> shelves;
    vector<int> counts;
};

struct Grid
{

    Grid(string n)
    {
        name = n;
    }

    int rows() const { return lines.size(); }

    int cols() const
    {

        if (lines.empty())
        {
            return 0;
        }
        else
        {
            return lines[0].size();
        }
    }

    void LoadFromFile(string filename)
    {
        ifstream f;
        f.open(filename);
        while (!f.eof())
        {
            string line;
            getline(f, line);
            // cout << line << "   (" << line.length() << ")" << endl;
            if (!line.empty() && line[0] != '#')
            {
                lines.push_back(line);
            }
        }
        f.close();

        // lines.pop_back();
    }

    int Check() const
    {

        for (string s : lines)
        {
            assert(s.size() == cols());
        }
        return 0;
    }
    int Print() const
    {

        cout << "Grid : " << name << endl
             << endl;

        for (string s : lines)
        {
            cout << s << endl;
        }

        cout << endl
             << "Rows : " << rows() << endl;
        cout << "Columns : " << cols() << endl;

        return 0;
    }

    vector<string> lines;
    string name;
};

int main()
{

    Library lib;

    lib.ReadFromFile("top_12000.txt");

    // cout << lib.GetWord(876) << endl;

    // lib.ComputeStats();
    // lib.PrintStats();

    // cout << lib.IsWord("DOG") << endl;
    // cout << lib.IsWord("GOD") << endl;
    // cout << lib.IsWord("ASDFEW") << endl;
    // cout << lib.IsWord("THANKS") << endl;
    lib.DebugBuckets();

    // string s = "dog";
    // cout << s << endl;
    // cout << ToUpper(s) << endl;
    // cout << s << endl;

    // Grid grid("MY GRID");

    // grid.LoadFromFile("test.txt");
    // grid.Check();
    // grid.Print();
};
```

### 10. Search the Library, Fast!
[https://youtu.be/nSW4uXS3gJU ](https://youtu.be/nSW4uXS3gJU )

Standard method to initialize a `struct`:
```cpp=
struct Word
{
    Word(string s) : word(s) {}
    string word;
};
```

Add a trailing underscore to members of `private:` section. Ex. : words -> words_.

```cpp=
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
#include <assert.h>
#include <fstream>

using namespace std;

string ToUpper(string s)
{
    string s2;

    for (char c : s)
    {
        s2.push_back(toupper(c));
    }
    return s2;
};

struct Word
{
    Word() {}
    Word(string s) : word(s) {}
    string word;
};
typedef vector<Word> Words;
typedef unordered_map<string, Word> WordMap;

class Library
{
public:
    Library() {}
    bool IsWord(string s) const
    {
        // method 1
        auto it = word_map_.find(s);
        return it != word_map_.end();
        // method 2
        // return word_map_.count(s) > 0;
    }

    void ComputeStats()
    {
        assert(counts_.empty());
        // resize vector that don't grow in time
        // vector initialized to 0
        counts_.resize(18);
        for (Word w : words_)
        {
            int len = w.word.length();
            if (len < 18)
            {
                counts_[len]++;
            }
        }
    }

    void PrintStats() const
    {
        for (int i = 1; i < counts_.size(); i++)
        {
            cout << counts_[i] << " words of " << i << " character(s) " << endl;
        }
    }

    string GetWord(int i) const
    {
        assert(i >= 0 && i < words_.size());
        return words_[i].word;
    }

    void ReadFromFile(string filename)
    {
        ifstream f;
        f.open(filename);
        while (!f.eof())
        {
            string line;
            getline(f, line);
            // cout << line << "   (" << line.length() << ")" << endl;
            if (!line.empty())
            {
                line = ToUpper(line);
                int len = line.length();
                if (line[len - 1] == '\r')
                {
                    line = line.substr(0, len - 1);
                }
                words_.push_back(Word(line));
                word_map_[line] = Word(line);
                // cout << "DEBUG: new bucket_count=" << word_map_.bucket_count() << " load_factor=" << word_map_.load_factor() << endl;
            }
        }

        // cout << words[0].word << endl;
        // cout << words[0].word.length() << endl;
        for (char c : words_[0].word)
        {
            int x = c;
            // cout << c << " " << x << endl;
        }

        f.close();

        cout << "Read " << words_.size() << " words from file '" << filename << "'" << endl;
    }

    void DebugBuckets() const
    {
        for (int i = 0; i < word_map_.bucket_count(); i++)
        {
            cout << "[" << i << "] " << word_map_.bucket_size(i) << endl;
        };
    }

private:
    Words words_;
    WordMap word_map_;
    vector<int> counts_;
};

struct Grid
{

    Grid(string n)
    {
        name = n;
    }

    int rows() const { return lines.size(); }

    int cols() const
    {

        if (lines.empty())
        {
            return 0;
        }
        else
        {
            return lines[0].size();
        }
    }

    void LoadFromFile(string filename)
    {
        ifstream f;
        f.open(filename);
        while (!f.eof())
        {
            string line;
            getline(f, line);
            // cout << line << "   (" << line.length() << ")" << endl;
            if (!line.empty() && line[0] != '#')
            {
                lines.push_back(line);
            }
        }
        f.close();

        // lines.pop_back();
    }

    int Check() const
    {

        for (string s : lines)
        {
            assert(s.size() == cols());
        }
        return 0;
    }
    int Print() const
    {

        cout << "Grid : " << name << endl
             << endl;

        for (string s : lines)
        {
            cout << s << endl;
        }

        cout << endl
             << "Rows : " << rows() << endl;
        cout << "Columns : " << cols() << endl;

        return 0;
    }

    vector<string> lines;
    string name;
};

int main()
{

    Library lib;

    lib.ReadFromFile("top_12000.txt");

    // cout << lib.GetWord(876) << endl;

    // lib.ComputeStats();
    // lib.PrintStats();

    cout << lib.IsWord("DOG") << endl;
    cout << lib.IsWord("GOD") << endl;
    cout << lib.IsWord("ASDFEW") << endl;
    cout << lib.IsWord("THANKS") << endl;
    lib.DebugBuckets();

    // string s = "dog";
    // cout << s << endl;
    // cout << ToUpper(s) << endl;
    // cout << s << endl;

    // Grid grid("MY GRID");

    // grid.LoadFromFile("test.txt");
    // grid.Check();
    // grid.Print();
};
```

### 11. How Memory Works

[https://youtu.be/-o8DVeVvA4s ](https://youtu.be/-o8DVeVvA4s )

`void*`
: pointer to a memory address

`&`
: address of an object

Methods for passing parameters to functions
- by value
ex. `void Foo(int x) {x += 1;};`
- by reference
ex. `void Foo(int& x) {x += 1;};`
- by pointer
ex. `void Foo(int* x) {*x += 3;};`

`new`
: command allocates memory on the heap

`delete`
: command  frees memory allocated by `new`

`unique_ptr`
: `unique_ptr` is a managed pointer

```cpp=
#include <iostream>
#include <memory>
#include <string>
#include <vector>

using namespace std;

void ToUpper(string& s) {
  // method 1
  for (char& c : s) {
    c = toupper(c);
  }
  // method 2
  // for (int i = 0; i < s.length(); i++) {
  //   s[i] = toupper(s[i]);
  // }
}
void Foo(int x, int& y, int* z) {
  cout << "FOO x = " << x << endl;
  cout << "FOO y = " << y << endl;
  cout << "FOO z = " << *z << endl;
  x += 1;
  y += 2;
  *z += 3;
  cout << "BAR x = " << x << endl;
  cout << "BAR y = " << y << endl;
  cout << "BAR z = " << *z << endl;
};

int main() {
  // char c = 'A';
  // int i = 10;
  // void* p0 = &c;
  // void* p1 = &i;
  // cout << c << endl;
  // cout << i << endl;
  // cout << p0 << endl;
  // cout << p1 << endl;
  // cout << sizeof(c) << endl;
  // cout << sizeof(i) << endl;

  // char c = 'A';
  // char* p = &c;
  // int i = 1000;
  // int* n = &i;
  // cout << c << endl;
  // *p = 'B';
  // cout << c << endl;
  // cout << i << endl;
  // *n = 2000;
  // cout << i << endl;

  // int i = 10;
  // int j = 20;
  // int k = 30;
  // cout << "ORI i = " << i << endl;
  // cout << "ORI j = " << j << endl;
  // cout << "ORI k = " << k << endl;
  // Foo(i, j, &k);
  // cout << "AFTER i = " << i << endl;
  // cout << "AFTER j = " << j << endl;
  // cout << "AFTER k = " << k << endl;

  // string name("dog");
  // cout << name << endl;
  // ToUpper(name);
  // cout << name << endl;

  // vector<int> x(1000);
  // x[450] = 5;
  // cout << x[450] << endl;
  // cout << "size of x = " << sizeof(x) << endl;

  // int* p = new int(8);
  // cout << *p << endl;
  // int x = *p;
  // cout << x << endl;
  // delete p;

  unique_ptr<int> p(new int(8));
  cout << *p << endl;
  int x = *p;
  cout << x << endl;
};
```
### 12. Pattern Hash

Declaring a function "const" is not enough to avoid collateral damage. Each parameter provided must also be declared "const".

[https://youtu.be/PJqoQMKlKjQ](https://youtu.be/PJqoQMKlKjQ)

```cpp=
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
  Grid(string n) { name = n; }

  int rows() const { return lines.size(); }

  int cols() const {
    if (lines.empty()) {
      return 0;
    } else {
      return lines[0].size();
    }
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
  Library lib;

  lib.ReadFromFile("top_12000.txt");

  lib.FindWord("D--");

  // TODO continue video at 30:00

  // Grid grid("MY GRID");

  // grid.LoadFromFile("test.txt");
  // grid.Check();
  // grid.Print();
};
```

### 13. Points and Spans

[https://youtu.be/7uS0hrpERcY](https://youtu.be/7uS0hrpERcY)

```cpp=
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

ostream& operator<<(ostream& os, Point& p) {
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

ostream& operator<<(ostream& os, Span& s) {
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
  Grid(string n) { name = n; }

  int rows() const { return lines.size(); }

  int cols() const {
    if (lines.empty()) {
      return 0;
    } else {
      return lines[0].size();
    }
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
  Library lib;
  lib.ReadFromFile("top_12000.txt");

  Grid grid("MY GRID");
  grid.LoadFromFile("test.txt");
  grid.Check();
  // grid.Print();

  Point p1;
  Point p2(2, 1);

  cout << "point1 is " << p1 << endl;
  cout << "point2 is " << p2 << endl;

  Span s1(p1, 3, true);
  Span s2(p2, 5, false);

  cout << "span1 is " << s1 << endl;
  cout << "span2 is " << s2 << endl;
};
```

### 14. Find Spans in the Grid

[https://youtu.be/_LlUZLRsxcU](https://youtu.be/_LlUZLRsxcU)

```cpp=
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

  // Point p1;
  // cout << "block=" << grid.is_block(p1) << endl;
  // cout << "blank=" << grid.is_blank(p1) << endl;
  // cout << "letter=" << grid.is_letter(p1) << endl;
  // Point p2(3, 3);
  // cout << "block=" << grid.is_block(p2) << endl;
  // cout << "blank=" << grid.is_blank(p2) << endl;
  // cout << "letter=" << grid.is_letter(p2) << endl;
  // Point p3(5, 2);
  // cout << "block=" << grid.is_block(p3) << endl;
  // cout << "blank=" << grid.is_blank(p3) << endl;
  // cout << "letter=" << grid.is_letter(p3) << endl;
};
```

### 15. Get Strings from the Grid

[https://youtu.be/IyqaPP-I6UQ](https://youtu.be/IyqaPP-I6UQ)

```cpp=
```

### 16. Solver Class

[https://youtu.be/b05M5oPZGgc](https://youtu.be/b05M5oPZGgc)

```cpp=
```

### 17. Write Words to the Grid

[https://youtu.be/fFqyXMxfMVE](https://youtu.be/fFqyXMxfMVE)

```cpp=
```

### 18. Preventing Duplicates

[https://youtu.be/AIjy3TcH924](https://youtu.be/AIjy3TcH924)

```cpp=
```
