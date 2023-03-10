# Lab Report 5 - Review Week 6 Lab Activity
March 11, 2023
## Week 6 Overview

For this week's lab, we wrote a grade server to autograde a students submission on github. 

My code is located [here](https://github.com/jesszhu71/list-examples-grader/blob/main/grade.sh). 

The overall workflow of the script was given to us (numbered below), and here is the parts of my script that correspond to those steps. 



### 1. Clone the repository of the student submission to a well-known directory name (provided in starter code)

We want to start by cloning the student's submission into the repository, which is given into the bash script 
as an input. To do this, we want to clear and previous creations of directories named student-submission
and then clone the inputted repository to the current directory. 


```
rm -rf student-submission
git clone $1 student-submission
echo 'Finished cloning'
```

### 2. Check that the student code has the correct file submitted. If they didn’t, detect and give helpful feedback about it.
Useful tools here are if and -e/-f. You can use the exit command to quit a bash script early.

In this step we want to go into the newly cloned submission folder and make sure that ListExamples.java exists. If it doesn't, 
we must stop and print a message explaining so, otherwise we can continue to the next part of our script. 


```
cd student-submission

if [[ -f ListExamples.java ]]
then 
    echo "ListExamples found"
else 
    echo "need file ListExamples"
    exit 1
fi
```

### 3. Somehow get the student code and your test .java file into the same directory. Useful tools here might 
be cp and maybe mkdir

I used cp to get the ListExamples.java file from the submission to the same directory as the test file. 
Starting at the directory where my test file is located, I used the cp command to move the student's ListExample.java
file to the current directory. 

```
cd ..
cp student-submission/ListExamples.java ./
```
### 4. Compile your tests and the student’s code from the appropriate directory with the appropriate classpath commands. If the compilation fails, detect and give helpful feedback about it.
Aside from the necessary javac, useful tools here are output redirection and error codes ($?) along with if
This might be a time where you need to turn off set -e. Why?

To compile, I compile all the java files in the directory using the junit CPATH and then 
redirected the errors into an text file named javac-err.txt. Then we check on the status of 
the compile command and if it exited successfully then report a successfull compile message. Otherwise we report a compile 
error and then exit the bash script. 

```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'
javac -cp $CPATH *.java 2> javac-err.txt
if [[ $? -eq 0 ]]
then
    echo "compiled correctly"
else
    echo "error compiling"
    exit 1
    # cat javac-err.txt
fi
```

### 5. Run the tests and report the grade based on the JUnit output.
Again output redirection will be useful, and also tools like grep could be helpful here

We run the test file here and and redirect the errors of this command to a text file called java-err.txt.
Then I'd check for the exit status of the execute test command. If the run of the test is successful, we display
a successful message, otherwise we print a failed test message and print out the errors of the error from the java-err.txt file

```

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > java-err.txt
if [[ $? -eq 0 ]]
then 
    echo "passed tests"
else 
    echo "did not pass tests"
    cat java-err.txt
fi
```

## Usage Examples (in the server)

I ran the following examples on a local server by compiling, running the server, and then 
opening up the links with the corresponding inputs. 

<img width="1303" alt="Screenshot 2023-03-11 at 4 57 51 PM" src="https://user-images.githubusercontent.com/43154527/224518445-094e68ba-a234-4928-97b8-60eed3b68859.png">

Example with [passing files](https://github.com/ucsd-cse15l-f22/list-methods-corrected). 

<img width="960" alt="Screenshot 2023-03-11 at 5 38 56 PM" src="https://user-images.githubusercontent.com/43154527/224519493-6139eeae-2b09-4080-94be-d9744eaf5abb.png">

Example with a [failing files](https://github.com/ucsd-cse15l-f22/list-methods-lab3). 

<img width="960" alt="Screenshot 2023-03-11 at 5 39 47 PM" src="https://user-images.githubusercontent.com/43154527/224519517-51004d0e-1b0b-493a-b2a9-61f4787c7509.png">

Example with [files that don't compile](https://github.com/ucsd-cse15l-f22/list-methods-signature). 

<img width="921" alt="Screenshot 2023-03-11 at 5 40 31 PM" src="https://user-images.githubusercontent.com/43154527/224519535-f92c9ab4-0a74-4d32-a539-8c94d3d21b16.png">


Example with [files that have wrong type arguments](https://github.com/ucsd-cse15l-f22/list-methods-signature). 

<img width="956" alt="Screenshot 2023-03-11 at 5 41 59 PM" src="https://user-images.githubusercontent.com/43154527/224519558-2b62f0c6-2d00-449a-8bd1-9730666cdc99.png">

Example with [incorrect names files](https://github.com/ucsd-cse15l-f22/list-methods-filename). 

<img width="959" alt="Screenshot 2023-03-11 at 5 42 23 PM" src="https://user-images.githubusercontent.com/43154527/224519568-50bd5a19-afd9-4b31-87e9-f0c9fde7f1f5.png">



## Future reference and further purposes

Using a bash script to grade files is helpful for grading large amounts of code at once. 
We can alter our script to accomodate large amounts of homework assignments and pipeline the process
so that we can document each student's score. In addition, we could add additional conditions to give a more personalize score
possibly according to how many tests they pass or the extent of the exact error that was in the student
submitted code. This would be a super quick process that would eliminate the need for hand-running and hand-grading code






---
That's the end of lab 5!



