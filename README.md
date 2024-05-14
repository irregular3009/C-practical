# C++ Programs

## 1. Sum of Series
```cpp
#include <iostream>
#include <cstdlib> // For atoi function

double computeSum(int n) {
    double total = 0.0;
    for (int i = 1; i <= n; ++i) {
        if (i % 2 == 0)
            total -= 1.0 / (i * i);
        else
            total += 1.0 / (i * i);
    }
    return total;
}

int main(int argc, char* argv[]) {
    int n;
    if (argc > 1) {
        n = atoi(argv[1]);
    } else {
        std::cout << "Enter the number of terms (n): ";
        std::cin >> n;
    }

    if (n <= 0) {
        std::cout << "Please enter a positive integer for n." << std::endl;
        return 1;
    }

    double seriesSum = computeSum(n);
    std::cout << "The sum of the first " << n << " terms of the series is: " << seriesSum << std::endl;

    return 0;
}

```
## 2. Remove Duplicates from Array

```C++
#include <iostream>
#include <unordered_set>
#include <vector>

std::vector<int> removeDuplicates(std::vector<int>& nums) {
    std::unordered_set<int> seen;
    std::vector<int> result;
    for (int num : nums) {
        if (seen.find(num) == seen.end()) {
            seen.insert(num);
            result.push_back(num);
        }
    }
    return result;
}

int main() {
    std::vector<int> nums = {1, 2, 2, 3, 4, 4, 5};
    std::vector<int> result = removeDuplicates(nums);
    std::cout << "Array after removing duplicates: ";
    for (int num : result) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    return 0;
}
```
## 3. Alphabet Occurrence Counter

```C++
#include <iostream>
#include <string>
#include <unordered_map>

void countAlphabets(const std::string& text) {
    std::unordered_map<char, int> freq;
    for (char c : text) {
        if (std::isalpha(c)) {
            freq[std::tolower(c)]++;
        }
    }
    std::cout << "Alphabet frequencies:" << std::endl;
    for (const auto& pair : freq) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }
}

int main(int argc, char* argv[]) {
    if (argc < 2) {
        std::cout << "Please provide a text as command line argument." << std::endl;
        return 1;
    }
    std::string text = argv[1];
    countAlphabets(text);
    return 0;
}

```

## 4. String Manipulation Menu-Driven Program

```C++
#include <iostream>
#include <cstring>
#include <cctype>

void showAddress(const char* str) {
    for (int i = 0; str[i] != '\0'; ++i) {
        std::cout << "Address of " << str[i] << ": " << static_cast<void*>(&str[i]) << std::endl;
    }
}

void concatenateStrings(char* str1, const char* str2) {
    strcat(str1, str2);
}

int compareStrings(const char* str1, const char* str2) {
    return strcmp(str1, str2);
}

int stringLength(const char* str) {
    int len = 0;
    while (str[len] != '\0') {
        len++;
    }
    return len;
}

void toUpperCase(char* str) {
    for (int i = 0; str[i] != '\0'; ++i) {
        str[i] = std::toupper(str[i]);
    }
}

void reverseString(char* str) {
    int len = stringLength(str);
    for (int i = 0; i < len / 2; ++i) {
        std::swap(str[i], str[len - i - 1]);
    }
}

void insertString(char* str, const char* insertStr, int pos) {
    int len = stringLength(str);
    if (pos < 0 || pos > len) {
        std::cout << "Invalid position." << std::endl;
        return;
    }
    strcat(str + pos, insertStr);
}

int main() {
    char str1[100], str2[50];
    std::cout << "Enter a string: ";
    std::cin.getline(str1, 100);
    std::cout << "Enter another string: ";
    std::cin.getline(str2, 50);

    // Example usage of menu-driven operations
    // Choose the operation you want
    // switch(operation) {
    //     case 'a': showAddress(str1); break;
    //     case 'b': concatenateStrings(str1, str2); break;
    //     case 'c': compareStrings(str1, str2); break;
    //     case 'd': stringLength(str1); break;
    //     case 'e': toUpperCase(str1); break;
    //     case 'f': reverseString(str1); break;
    //     case 'g': insertString(str1, str2, pos); break;
    //     default: std::cout << "Invalid operation." << std::endl;
    // }

    return 0;
}

```

## 5. Merge Ordered Arrays

```C++
#include <iostream>
#include <vector>

std::vector<int> mergeArrays(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::vector<int> merged;
    int i = 0, j = 0;
    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] <= arr2[j]) {
            merged.push_back(arr1[i]);
            i++;
        } else {
            merged.push_back(arr2[j]);
            j++;
        }
    }
    while (i < arr1.size()) {
        merged.push_back(arr1[i]);
        i++;
    }
    while (j < arr2.size()) {
        merged.push_back(arr2[j]);
        j++;
    }
    return merged;
}

int main() {
    std::vector<int> arr1 = {1, 3, 5, 7, 9};
    std::vector<int> arr2 = {2, 4, 6, 8, 10};
    std::vector<int> merged = mergeArrays(arr1, arr2);
    std::cout << "Merged array: ";
    for (int num : merged) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    return 0;
}

```

## 6. Binary Search

```C++
#include <iostream>
#include <vector>

// Binary search without recursion
int binarySearch(std::vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1; // Not found
}

// Binary search with recursion
int binarySearchRecursive(std::vector<int>& nums, int target, int left, int right) {
    if (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            return binarySearchRecursive(nums, target, mid + 1, right);
        } else {
            return binarySearchRecursive(nums, target, left, mid - 1);
        }
    }
    return -1; // Not found
}

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int target = 5;

    // Using binary search without recursion
    int index = binarySearch(nums, target);
    if (index != -1) {
        std::cout << "Element found at index " << index << std::endl;
    } else {
        std::cout << "Element not found." << std::endl;
    }

    // Using binary search with recursion
    index = binarySearchRecursive(nums, target, 0, nums.size() - 1);
    if (index != -1) {
        std::cout << "Element found at index " << index << std::endl;
    } else {
        std::cout << "Element not found." << std::endl;
    }

    return 0;
}

```

## 7. GCD Calculation
```C++
#include <iostream>

// GCD calculation without recursion
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// GCD calculation with recursion
int gcdRecursive(int a, int b) {
    if (b == 0) {
        return a;
    }
    return gcdRecursive(b, a % b);
}

int main() {
    int num1 = 24, num2 = 36;

    // Using GCD calculation without recursion
    int result = gcd(num1, num2);
    std::cout << "GCD of " << num1 << " and " << num2 << " is " << result << std::endl;

    // Using GCD calculation with recursion
    result = gcdRecursive(num1, num2);
    std::cout << "GCD of " << num1 << " and " << num2 << " is " << result << std::endl;

    return 0;
}

```

## 8. Matrix Operations

```C++
#include <iostream>
#include <vector>

class Matrix {
private:
    std::vector<std::vector<int>> data;
    int rows, cols;

public:
    Matrix(int r, int c) : rows(r), cols(c) {
        data.resize(rows, std::vector<int>(cols, 0));
    }

    // Function to perform matrix addition
    Matrix add(const Matrix& other) const {
        if (rows != other.rows || cols != other.cols) {
            throw std::invalid_argument("Matrices are not of the same size.");
        }
        Matrix result(rows, cols);
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                result.data[i][j] = data[i][j] + other.data[i][j];
            }
        }
        return result;
    }

    // Function to perform matrix multiplication
    Matrix multiply(const Matrix& other) const {
        if (cols != other.rows) {
            throw std::invalid_argument("Number of columns in the first matrix must be equal to the number of rows in the second matrix.");
        }
        Matrix result(rows, other.cols);
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < other.cols; ++j) {
                for (int k = 0; k < cols; ++k) {
                    result.data[i][j] += data[i][k] * other.data[k][j];
                }
            }
        }
        return result;
    }

    // Function to transpose the matrix
    Matrix transpose() const {
        Matrix result(cols, rows);
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                result.data[j][i] = data[i][j];
            }
        }
        return result;
    }

    // Function to display the matrix
    void display() const {
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                std::cout << data[i][j] << " ";
            }
            std::cout << std::endl;
        }
    }
};

int main() {
    Matrix A(2, 3);
    Matrix B(3, 2);

    // Example matrix initialization
    // Fill matrices A and B with appropriate values

    // Matrix addition
    Matrix sum = A.add(B);
    std::cout << "Sum of matrices:" << std::endl;
    sum.display();

    // Matrix multiplication
    Matrix product = A.multiply(B);
    std::cout << "Product of matrices:" << std::endl;
    product.display();

    // Transpose of a matrix
    Matrix transpose = A.transpose();
    std::cout << "Transpose of matrix A:" << std::endl;
    transpose.display();

    return 0;
}

```

## 9. Inheritance and Polymorphism

```C++
#include <iostream>
#include <string>

class Person {
protected:
    std::string name;

public:
    Person(const std::string& n) : name(n) {}

    virtual void display() const {
        std::cout << "Name: " << name << std::endl;
    }
};

class Student : public Person {
private:
    std::string course;
    int marks;
    int year;

public:
    Student(const std::string& n, const std::string& c, int m, int y) : Person(n), course(c), marks(m), year(y) {}

    void display() const override {
        Person::display();
        std::cout << "Course: " << course << std::endl;
        std::cout << "Marks: " << marks << std::endl;
        std::cout << "Year: " << year << std::endl;
    }
};

class Employee : public Person {
private:
    std::string department;
    double salary;

public:
    Employee(const std::string& n, const std::string& d, double s) : Person(n), department(d), salary(s) {}

    void display() const override {
        Person::display();
        std::cout << "Department: " << department << std::endl;
        std::cout << "Salary: " << salary << std::endl;
    }
};

int main() {
    Person* person1 = new Person("John Doe");
    Person* student1 = new Student("Alice Smith", "Computer Science", 90, 2023);
    Person* employee1 = new Employee("Bob Johnson", "Engineering", 75000);

    person1->display();
    student1->display();
    employee1->display();

    delete person1;
    delete student1;
    delete employee1;

    return 0;
}
```

## 10. Triangle Class with Exceptional Handling

```C++
#include <iostream>
#include <stdexcept>

class Triangle {
private:
    double side1, side2, side3;

public:
    Triangle(double s1, double s2, double s3) : side1(s1), side2(s2), side3(s3) {
        if (side1 <= 0 || side2 <= 0 || side3 <= 0 || side1 + side2 <= side3 || side1 + side3 <= side2 || side2 + side3 <= side1) {
            throw std::invalid_argument("Invalid triangle sides.");
        }
    }

    double calculateArea() {
        double s = (side1 + side2 + side3) / 2;
        return std::sqrt(s * (s - side1) * (s - side2) * (s - side3));
    }
};

int main() {
    try {
        Triangle triangle(3, 4, 5);
        double area = triangle.calculateArea();
        std::cout << "Area of the triangle: " << area << std::endl;
    } catch (const std::invalid_argument& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }

    return 0;
}

```

## 11. Student Class with File I/O

```C++
#include <iostream>
#include <fstream>
#include <string>

class Student {
private:
    int rollNo;
    std::string name;
    std::string className;
    int year;
    int totalMarks;

public:
    Student(int r, const std::string& n, const std::string& c, int y, int t) : rollNo(r), name(n), className(c), year(y), totalMarks(t) {}

    void saveToFile(std::ofstream& file) const {
        file << rollNo << " " << name << " " << className << " " << year << " " << totalMarks << std::endl;
    }

    static Student readFromFile(std::ifstream& file) {
        int rollNo;
        std::string name, className;
        int year, totalMarks;
        file >> rollNo >> name >> className >> year >> totalMarks;
        return Student(rollNo, name, className, year, totalMarks);
    }

    void display() const {
        std::cout << "Roll No.: " << rollNo << std::endl;
        std::cout << "Name: " << name << std::endl;
        std::cout << "Class: " << className << std::endl;
        std::cout << "Year: " << year << std::endl;
        std::cout << "Total Marks: " << totalMarks << std::endl;
    }
};

int main() {
    // Write student data to file
    std::ofstream outFile("students.txt");
    if (outFile.is_open()) {
        Student student1(1, "John Doe", "Class X", 2023, 450);
        Student student2(2, "Alice Smith", "Class XI", 2022, 480);
        student1.saveToFile(outFile);
        student2.saveToFile(outFile);
        outFile.close();
    } else {
        std::cerr << "Unable to open file for writing." << std::endl;
    }

    // Read student data from file
    std::ifstream inFile("students.txt");
    if (inFile.is_open()) {
        Student student1 = Student::readFromFile(inFile);
        Student student2 = Student::readFromFile(inFile);
        student1.display();
        student2.display();
        inFile.close();
    } else {
        std::cerr << "Unable to open file for reading." << std::endl;
    }

    return 0;
}

```

## 12. File Content Copy with Whitespaces Removal

```C++
#include <iostream>
#include <fstream>
#include <string>

void copyFileWithWhitespaceRemoval(const std::string& sourceFile, const std::string& destinationFile) {
    std::ifstream inFile(sourceFile);
    std::ofstream outFile(destinationFile);
    if (inFile.is_open() && outFile.is_open()) {
        char c;
        while (inFile.get(c)) {
            if (!std::isspace(c)) {
                outFile.put(c);
            }
        }
        std::cout << "File content copied with whitespaces removed." << std::endl;
        inFile.close();
        outFile.close();
    } else {
        std::cerr << "Unable to open files." << std::endl;
    }
}

int main() {
    std::string sourceFile = "input.txt";
    std::string destinationFile = "output.txt";
    copyFileWithWhitespaceRemoval(sourceFile, destinationFile);
    return 0;
}

```
