Lab Report 4! - Vim
For this lab report, I will be taking you through my steps to fix an error in a java file from the command line. 
I start by logging into ieng6 by typing `ssh akeshwani@ieng6.ucsd.edu`.
Then I remove the `lab7` directory in order to be able to clone it using the ssh clone URLs. To remove the `lab7` directory I type `rm -rf lab7` into the command line.
Then I clone the `lab7` repository by using the ssh clone. Since I can't see the contents of the directory in my explorer, I type `ls` to see the contents of my working directory. After seeing `lab7` was in my working directory I entered `cd lab7` into the command line to change my current directory to `lab7`.
Inputting `ls` again lists for me the contents of the `lab7` directory:

<img width="464" alt="Screen Shot 2024-02-27 at 9 17 25 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/15b84191-66f4-4861-9fd9-d3096f10e78f">

I noticed there is a `test.sh` file in the directory. Typing `cat test.sh` to show its contents shows it compiles and runs the tester for `ListExamples.java`. To run the tests, I type `bash test.sh` into the command line. We get:

<img width="630" alt="Screen Shot 2024-02-27 at 9 38 45 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/3e5793f3-7028-4b5c-97bf-4cbad4fe9a03">

Thus you can see the test initially fails. 
Seeing that `ListExamples.java` is contained in our current directory, we can now enter `vim ListExamples.java` into the command line to use `vim` to edit the file. Once we do our terminal now looks like this:

<img width="881" alt="Screen Shot 2024-02-27 at 9 25 54 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/1ee285b9-db48-4662-9a8b-9fbc8bf799f7">

The error we want to fix exists 43 lines below where our cursor is initially. So we type `43j e x i 2 <esc> :wq <enter>`. Here, `43j` moves our cursor down 43 lines of code. Next `e` moves our cursor to the end of the first word in the line. The first word in the ine in this case is `index1`, which is causing the error since it should be `index2` instead. Then the `x` deletes the 1 in `index1`. `i` allows us to insert text into the file, which then we insert 2. Finally `:wq <enter.` saves our changes and quits `vim`. We are left with the following:

<img width="593" alt="Screen Shot 2024-02-27 at 9 34 33 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/0df21d5f-8d6f-4607-b072-96794b913bf8">

To see if our changes fixed the error I type `<up> <up> <enter>` to run `bash test.sh` one more time. We get the following:

<img width="363" alt="Screen Shot 2024-02-27 at 9 42 03 PM" src="https://github.com/aahilkeshwani/cse15l-lab-reports/assets/156363135/a1cb14e7-0871-4961-8c49-139eed78179d">

As you can see we have successfully edited and fixed an error in a java file straight from the command line using vim!
