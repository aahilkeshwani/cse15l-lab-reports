Lab Report 3! - Bugs and Commands (week 5)
Part 1 - Bugs
In week 4's lab, we learned about debugging and testing methods. In this lab report, I will be addressing issues from the `reverseInPlace` method.
The following test input induces a failure:
```
@Test
public void testReverseInPlace() {
  int [] input1 = {1, 2, 3};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[] {3, 2, 1}, input1);
}
```
Even when the method doesn't accurately reverse the array, certain tests do not induce failure. Here is an example of one:
```
@Test
public void testReverseInPlace() {
  int [] input1 = {1};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[] {1}, input1);
}
```
The test above doesn't induce a failure since an array with one element reversed is still the same array.
Here are the outputs of running the two tests above, respectively. 
<img width="1079" alt="Screen Shot 2024-02-13 at 12 31 24 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/f171d1b7-dc3e-48b0-a77f-11119e367c27">

<img width="1066" alt="Screen Shot 2024-02-13 at 12 30 59 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/bb354ae6-068f-41f9-aeee-96cd985f8fd4">

Here is the initial code for the `reverseInPlace` method:
```
static void reverseInPlace(int [] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[ arr.length - i -1];
    }
  }
```
The above code has a bug where the method moves the first half of elements to the back half but cannot move the elements at the end of the array to the beginning.
Here is the method's code after it has been fixed:
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length/2; i += 1) {
    int temp = arr[i];
    arr[i] = arr[arr.length - i -1];
    arr[arr.length - i - 1] = temp;
    }
  }
```
The first change I made was to create a local variable for the method called `temp` of type `int`, that stores variables at `i` during the for loop. The initial method wasn't able to map the first half of the elements to the end, because the first half elements were not saved. By creating a variable to store them, we can assign the back half of the array to the `temp` variable.

Part 2 - Researching Commands
For this section of the lab report, I chose to research the `grep` command, which searches a file for a pattern of characters and prints out all lines following the pattern. 
The `-c` option prints out the number of lines matching the pattern instead of the lines themselves. Here are a couple of examples of using `-c` with `grep`: 
```
find technical/ > find-results.txt
grep -c ".txt" find-results.txt
1391
```
The example above shows using `grep` to find the number of `.txt` files in the `technical` directory. The first line uses the `find` command to create a `.txt` file containing all the files and directories in `technical`. Then we use `grep` with the `-c` option to find the number of `.txt` files in `technical`. This is useful especially since it only took two lines of code. 
```
grep -c "flight" technical/911report/chapter-1.txt
74
```
This example shows how to call `grep` with the `-c` option on a file itself. Here, we call it on `chapter-1.txt` in the `911report` directory. `grep` reads through `chapter-1.txt` and returns the number of times "flight" appears in the text.
Next, the `-v` option for the `grep` command filters all lines that don't have the specified string. For example:
```
find technical/ > find-results.txt
grep -v ".txt" find-results.txt
technical/
technical//government
technical//government/About_LSC
technical//government/Env_Prot_Agen
technical//government/Alcohol_Problems
technical//government/Gen_Account_Office
technical//government/Post_Rate_Comm
technical//government/Media
technical//plos
technical//biomed
technical//911report
```
In the example above, we first put all files and directories under `technical/` in a txt file `find-results.txt`. We then use `grep` and `-v` to find all lines in `find-results.txt` that don't contain ".txt". Thus we filter out all text files and are left with directories. This is an easy way to find all directories in the current directory. 
```
grep -v ".txt" find-results.txt > notxt-results.txt
grep -v "government" notxt-results.txt
technical/
technical//plos
technical//biomed
technical//911report
```
In this example, we use `-v` in a similar way. First, we put our results from the previous example into a text file called `notxt-results.txt`. Then we use `grep` and `-v` to filter out all lines with `government`. This leaves us with 4 directories that are unrelated to government. 
Another useful option for the `grep` command is the `-e` option which allows you to filter multiple strings or expressions. In the following example I am using the same text file I created in the last example, `notxt-results.txt`.
```
grep -e "government" -e "biomed" notxt-results.txt
technical//government
technical//government/About_LSC
technical//government/Env_Prot_Agen
technical//government/Alcohol_Problems
technical//government/Gen_Account_Office
technical//government/Post_Rate_Comm
technical//government/Media
technical//biomed
```
Here, we are filtering all lines that contain either `government` or `biomed`. This is very useful to be able to find files that contain certain keywords. 
Finally `-An`, where n is an integer, outputs n-lines after the line containing the specified string. In the following example I will again use the `notxt-results.txt` file. 
```
grep -A1 "technical//plos" notxt-results.txt
technical//plos
technical//biomed
```
In this example, I used the `-An` option to find the line after `technical//plos`. The usefulness of this command isn't super obvious now but, we can use this command in files with code to debug iterators. For example:
```
grep -A2 "for(File f: paths)" DocSearchServer.java
               for(File f: paths) {
                   if(FileHelpers.readFile(f).contains(parameters[1])) {
                       foundPaths.add(f.toString());
```
In the above example, I show how we can use the same command option to find the contents of a for loop. This is very useful because if you think you have an error in one of your for loops you can use `grep` and the `-A` option to print out lines after the for loop, where the error most likely resides.
All the research for part 2 of this lab report used the following source: https://www.geeksforgeeks.org/grep-command-in-unixlinux/
