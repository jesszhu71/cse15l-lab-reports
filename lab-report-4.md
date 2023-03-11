# Lab Report 4 - Set up & your CSE 15L account
February 23, 2023

Note: any new lines I use to write the keys pressed in a step are for ease of reading the lab and not part of the completion of the challenge. 

## 1. Setup Delete any existing forks of the repository you have on your account if applicable. 

<img width="629" alt="Screenshot 2023-02-23 at 11 42 02 PM" src="https://user-images.githubusercontent.com/43154527/221121544-bdafc443-5a68-481c-8b1c-d176034efb90.png">

Remove any forks of the repository from your own github. 

## 2. Setup Fork the repository

Go to the [repository](https://github.com/ucsd-cse15l-w23/lab7) and fork. 

<img width="778" alt="Screenshot 2023-02-23 at 11 49 16 PM" src="https://user-images.githubusercontent.com/43154527/221122139-a1c59aa7-80d0-42d8-a62b-f67625799683.png">

<img width="782" alt="Screenshot 2023-02-23 at 11 50 29 PM" src="https://user-images.githubusercontent.com/43154527/221122386-7ef82679-3ae1-4026-85ec-5c3c60f348f2.png">

<img width="783" alt="Screenshot 2023-02-23 at 11 50 54 PM" src="https://user-images.githubusercontent.com/43154527/221122450-36216057-9f11-47fe-82de-e97ac8722963.png">


## 3. The real deal Start the timer!

## 4. Log into ieng6

Starting at local computer (anywhere), log into the remote server by typing the following:

### keys pressed: 

    <up><up><enter>
  
The following command below was 2 up in the command line history so I used the up arrow to access it. 

``` 
ssh cs15lwi23[your-account]@ieng6.ucsd.edu
```
Now you should be logged in as shown here. 

<img width="911" alt="Screenshot 2023-02-24 at 12 09 58 AM" src="https://user-images.githubusercontent.com/43154527/221126283-f290ab83-8ce9-4325-93a8-c49fa5d948f1.png">

## 5. Clone your fork of the repository from your Github account
  
### keys pressed:  
    
    <up><up><up><up><up><up><up><up><up><up><up><up><up><up><enter>cd lab7<enter>
  
  
The following command below was 14 lines up in the command line history so I used the up arrow to access it. 
  
  
```
  git clone git@github.com:jesszhu71/lab7.git
```
<img width="910" alt="Screenshot 2023-02-24 at 12 15 38 AM" src="https://user-images.githubusercontent.com/43154527/221127338-15d352a2-bf61-4a6b-bc38-95559298d349.png">
  
  Then I used the cd command to go into the new repository file directory. 

## 6. Run the tests, demonstrating that they fail
  
### keys pressed: 
    
    <up><up><up><up><up><enter><up><up><up><up><up><enter>

The commands below were 5 lines up in the command line history so I used the up arrow to access the first line.
Then I repeated the exact same process to get the second line. 
                
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests     
```
  
<img width="777" alt="Screenshot 2023-02-24 at 12 27 17 AM" src="https://user-images.githubusercontent.com/43154527/221129594-6a04ee04-cafb-4182-aaba-379a3017996d.png">
  
## 7. Edit the code file to fix the failing test

### keys pressed: 

    nano ListExamples.java<enter>

    <down><down><down><down>

    <right><right><right><right><right><right><right><right><right><right>

    <right><right><right><right><right><right><right><right><right>

    implements StringChecker <down>

    public boolean checkString(String s){ return "bye" == s;} <enter>

    <down><down><down><down><down><down><down><down><down><down>

    <down><down><down><down><down><down><down><down><down><down>

    <down><down><down><down><down><down><down><down><down><down>

    <down><down><down><down><down><down>

    <right><right><right><right><right><right><right><right><right><right>

    <right><right><backspace>2

    ^xy<enter>
                
I used nano to open the file at the command line for editing. Then I used the arrow keys (\<down\>x4, \<right\>x19) to implement
the string checker into our class. Then I navigate (\<down\>) to add the string checker method into our class and type out the 
missing line for the string checker. Next, I used the arrow keys (\<down\>x36, \<right\>x12) to navigate to line 43 and edit the
"1" to a "2". Then I exited the file using the nano commands, making sure to save the changes made to the file and specifying 
the file name. 


  <img width="1236" alt="Screenshot 2023-02-24 at 1 30 33 AM" src="https://user-images.githubusercontent.com/43154527/221143012-b9673e83-6e64-461c-b6a3-9430ba79b85e.png">
                

  <img width="587" alt="Screenshot 2023-02-24 at 1 30 13 AM" src="https://user-images.githubusercontent.com/43154527/221142924-077237ab-dd0a-4232-9ecb-5ebe56fb8394.png">


## 8. Run the tests, demonstrating that they now succeed

### keys pressed: 

    <up><up><up><enter><up><up><up><enter>
                
The commands below were 3 lines up in the command line history so I used the up arrow to access the first line.
Then I repeated the exact same process to get the second line. 
                
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests   
```

<img width="1239" alt="Screenshot 2023-02-24 at 1 02 11 AM" src="https://user-images.githubusercontent.com/43154527/221136984-2c519d28-ffc8-4fbe-bc48-0c9775813dd0.png">

## 9. Commit and push the resulting change to your Github account

### keys pressed: 
  
    git add<enter>

    git commit -m "fix ListExamples"<enter>

    git push<enter>
                
To commit the changes made to ListExamples, I used git add to add the file to changes. Then I committed the change with a commit message.
Finally I pushed the changes to my github repository and now the files are updated at the master branch of my copy of the repository. 
<img width="1058" alt="Screenshot 2023-02-24 at 1 05 03 AM" src="https://user-images.githubusercontent.com/43154527/221137490-39342b9e-f35d-4d6b-8015-446ff4c9e8dd.png">


---
That's the end of lab 4!

