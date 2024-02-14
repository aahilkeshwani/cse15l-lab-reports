Lab Report 2! - Bugs and Commands (week 5)
Part 1 - Bugs
In week 4's lab we learned about debugging and testing methods. In this lab report, I will be addressing issues from the `reverseInPlace` method.
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
252
```
The example above shows using `grep` to find the number of `.txt` files in the `technical` directory. The first line uses the `find` command to create a `.txt` file containing all the files and directories in `technical`. Then we use `grep` with the `-c` option to find the number of `.txt` files in `technical`. This is useful especially since it only took two lines of code. 
