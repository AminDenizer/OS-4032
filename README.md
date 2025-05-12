# **Simple C++ Program Setup and Execution**

## Video Explanation

For a visual explanation, watch this video:

▶️ [Watch on YouTube](https://youtu.be/wesT2P4rUwM)


## **Step 1: Create the Program File**

Open the terminal and run the following command to create a new file using `nano`:

```bash
nano myprogram.cpp
```

Paste the following C++ code inside the file:

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

Save and exit the editor:

* Press `Ctrl+O`, then `Enter` to save
* Press `Ctrl+X` to exit

---

## **Step 2: Compile the Program**

Use the `g++` compiler to compile your program:

```bash
g++ myprogram.cpp -o myprogram
```

To run it:

```bash
./myprogram
```

You should see the following output:

```
Hello, World!
```

---

## **Step 3: Make It a Shell Command**

To run your program like a built-in shell command, copy it to a system-wide directory (e.g., `/usr/local/bin`):

```bash
sudo cp myprogram /usr/local/bin/myprogram
```

Now you can execute it from anywhere in the terminal:

```bash
myprogram
```
