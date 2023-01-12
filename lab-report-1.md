# Lab Report 1 - Set up & your CSE 15L account
January 16, 2023
## Installing VScode
To download Visual Studio Code, visit their [website](https://code.visualstudio.com/) and follow the download instructions

Once that is downloaded, you should see this when you open the application

<img width="807" alt="Screen Shot 2023-01-12 at 11 01 37 AM" src="https://user-images.githubusercontent.com/43154527/212157568-63f8df92-d5fd-4034-ad05-da30c60b817d.png">

---

## Remotely Connecting
Each student will have their own CSE 15l specific account that can be retrieved [here](https://sdacs.ucsd.edu/~icc/index.php). 

From this site, you will enter your student ID and username. Once you have retrieved your account username, you will need to reset the password to that account. 

Head over to VSCode and open a new terminal and set terminal to default git bash (if on windows system) and then use the ssh command (below) to connect to the server. 

```
$ ssh cs15lwi23[your_account]@ieng6.ucsd.edu
// where your_account refers the the username you retrieved earlier
```

The first time connecting to the server will prompt a autheticity warning which you will say yes to and you will enter your password.

<img width="585" alt="Screen Shot 2023-01-12 at 11 17 11 AM" src="https://user-images.githubusercontent.com/43154527/212160577-618d9d03-77f6-446c-bb52-c26c7f92d2bb.png">

Once you have successfully logged in, you will see this message, meaning that you are connect to the remote server. 

<img width="598" alt="Screen Shot 2023-01-12 at 11 19 12 AM" src="https://user-images.githubusercontent.com/43154527/212160972-ab9ba1e5-e077-4fb0-bc92-f5812c035b0e.png">

---

## Trying Commands
Now that we are in the server, we can use bash commands to explore the file architecture of the server.

<img width="522" alt="Screen Shot 2023-01-12 at 11 26 20 AM" src="https://user-images.githubusercontent.com/43154527/212162290-f226ebd4-4d43-4246-b5c3-8ceefe62c1e2.png">

<img width="369" alt="Screen Shot 2023-01-12 at 11 26 52 AM" src="https://user-images.githubusercontent.com/43154527/212162371-9df7cb3d-203b-465b-a6e7-6bc266f225d1.png">


---
That's the end of lab 1!




