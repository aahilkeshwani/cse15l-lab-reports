Lab Report 5!
In this lab report I will show a senario of a student struggling with their lab and a TA helping them. In this case I will be using lab 3 as an example.
Student:
In the lab description it says that the file `ArrayExamples.java` has bugs in both methods. I used a bash script file called `test.sh` to compile and run the java files in the `lab3` directory. When I run `test.sh` the output shows no errors. Is there something wrong wtih my bash script? Is it testing the wrong files?

<img width="1027" alt="Screen Shot 2024-03-12 at 2 57 03 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/7ff01a09-db05-462c-87cf-95236963c5fa">

TA:
Hey there Student. Your bash script looks good and should be compiling and running the files as needed. Take a look at the tester file that tests `ArrayExamples.java`. What is an issue with these testers? Do these tests actually test wether the methods are implemented? Good luck!

Student looks at `ArrayTests.java`. 
Student:
I noticed that in `ArrayTest.java` the first test tests the method `reverseInPlace` with an array of length 1. With just one element in the array the array stays the same before and afeter the method is implemented. Thus this is a bad test. Similarly in the second test testing the method `reversed`, the test uses an array of length 0. This is a very unhelpful test. Thank you TA!
Screenshot of `ArrayTest.java`:
<img width="733" alt="Screen Shot 2024-03-12 at 3 09 10 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/6e5f9330-fdda-40c3-bde9-a992061f2f9a">

To change the tests in `ArrayTest.java` to be more helpful I will add more elements to the arrays we are conducting the tests on. Perhaps this will provide me with the errors I need to recognize the bugs in the methods. 
`ArrayTest.java` after making changes to the tests:

<img width="800" alt="Screen Shot 2024-03-12 at 3 13 17 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/89f2d8b5-4700-4bf1-97ac-7015ff8f1454">

Output of bash script `test.sh`:

<img width="994" alt="Screen Shot 2024-03-12 at 3 14 32 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/c3da8d26-6c72-451e-aedf-96992d140990">

As we can see in the output the element at index 2 which is the last element in the array is the same as the first element in the array. Our array went from [1, 2, 3] to [3, 2, 3]. 
The issue with the method `reverseInPlace` is that it tries to change the every element to its index subtracted from the last index. The issue with this is after iterating through half the array, we are now switching each element with itself. To fix this we need to create a temp variable to store the element at the iteration, and iterate through half the array instead of all of it.

Here we have the fixed method `reverseInPlace`:

<img width="596" alt="Screen Shot 2024-03-12 at 3 51 41 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/0e5d1510-dc25-4436-8d48-3c032dbc03f1">

The following is the file and directory structure:
```
lab3
~lib
ArrayExamples.java
ArrayTest.java
test.sh
```
Contents of `test.sh`:
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
```
The contents of the method `reverseInPlace` before:
```
static void reverseInPlace(int [] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[ arr.length - i -1];
    }
  }
```
The contents of the method `reverseInPlace` after:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i]
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```
Here is a description of what I changed in the `reverseInPlace` method to fix the bug:
I created a local variable called `temp` that stores the integer at the point of iteration the for loop is in. So `temp = arr[i]`. We then assign the back half of the array `arr[arr.length - i -1]` to `temp`. Then finally we iterate through half the array instead of all of it. 

Part 2: Reflection

I thought it was cool how we progressed through commands in the command line. When I first started coding I thought the command line/terminal was really only for compiling and running files and code. As we progressed further and into the second half of the class I learned we can do so much more. One of my favorite commadns is `vim`. I thought it was so cool how we could debug and edit straight from the command line without even having to go into the file. Even within `vim` there are so many things you can do like copy a line or even copy two lines through `yy` and `2yy`. There are so many shortcuts to move the cursor fast, and you can even move forwards and backwards. Anyways yeah I just loved `vim` and loved learning how important and useful command line operations are.
