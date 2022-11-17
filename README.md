# michellundell/13a C/C++

## Agenda

1. Github actions with Flaw finder 
2. Assigment Setup a repository with github action Flawfinder
3. Repetition / finishing C++ assignment.

## 1. Github actions

Read/view: https://docs.github.com/en/actions 

Github actions is about automatically do actions on your code on specific actions like a commit, pull-request etc.
It can automatically perform things like compiling, run or test your program .. (anything you want).

Its great to use when managing a repository. Example: pull requests should at least be able to compile...
There is a lot of actions that could be performed, we will cover the most basic usage to check that a
pull request is compiled ...

1. Create a new repository
   Make sure it is "public"!
   Let github add a README file.
   Click on "Create repository"

2. Add an action

Click on the "(>)Actions"

Search workflows for "C++"

Select the "C/C++ with Make" workflow by clicking on  "Configure"

You will then see an editor with the code for your action that looks like:

```
name: C/C++ CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: configure
      run: ./configure
    - name: make
      run: make
    - name: make check
      run: make check
    - name: make distcheck
      run: make distcheck
```

Delete the following lines beneath the "steps:"

```
    - name: configure
      run: ./configure
    - name: make check
      run: make check
    - name: make distcheck
      run: make distcheck
```

Your action should now look like

```
name: C/C++ CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: make
      run: make
```

Now click on the green "Start Commit"

In the dialogue, the "Commit directly to main branch" should be checked. Then click on "Commit new file".

Now go back to your repository and click on "Add file"

The name should be "Makefile" with a capital letter M.

Change "Spaces" to "Tabs", and set it to 4 spaces.

Now in the Makefile write the following code:

```
target:
	echo "Running target"
	cc sample.c -o sample
	./sample
```

Scroll down and set "Commit directly to the main branch", and click "Commit new file"

Then add a new file by clicking on "Add file"

Name the file to sample.c

Add the following code to the file
```
/* 
* This example is copied from
* https://www.thegeekstuff.com/2013/06/buffer-overflow/
*/

#include <stdio.h>
#include <string.h>

int main(int argc, char **argv)
{
    char buff[15];
    int pass = 0;

    printf("\n Enter the password : \n");
    gets(buff);

    if(strcmp(buff, "thesecretpassword"))
    {
        printf ("\n Wrong Password \n");
    }
    else
    {
        printf ("\n Correct Password \n");
        pass = 1;
    }

    if(pass)
    {
       /* Now Give root or admin rights to user*/
        printf ("\n Root privileges given to the user \n");
    }

    return(0);
}
```
Then scroll down and click "Commit new file"


So lets show what this all does....

Click on your sample.c
Edit it so it looks like

```
/* 
* This example is copied from
* https://www.thegeekstuff.com/2013/06/buffer-overflow/
*/

#include <stdio.h>
#include <string.h>

int main(int argc, char **argv)
{
    char buff[15];
    int pass = 0;

    printf("\nI understand I will never write a program like this\n");

    printf("\n Enter the password : \n");
    gets(buff);

    if(strcmp(buff, "thesecretpassword"))
    {
        printf ("\n Wrong Password \n");
    } else {
        printf ("\n Correct Password \n");
        pass = 1;
    }

    if(pass)
    {
       /* Now Give root or admin rights to user*/
        printf ("\n Root privileges given to the user \n");
    }

    return(0);
}
```
Then scroll down and "Create a new branch for this commit and start a pull request. "

Then click "Propose changes"

Write a comment and click on "Create pull request"


At the "top" you see pull requests are increased, click on pull-requests ...

You will see a pull request we made has a red cross beside it. This means it did not pass the checks.

Select the pull-request

You will see something like
```
C/C++ CI / build (pull_request) Successful in 3s

```

Now we add another action that could he useful in your projects .. a flawfinder!!

Add a new action "Flawfinder" and configure it to use C language.

Aha, by setting up an action, the code will automatically check your code for flaws  and the status is noted in the pull-request.
Nice, I don't want to merge any pull requests that have obvious flaws.

Now, go back to your repository. 

Then select your branch "patch ..."

Click on the sample.c file, and edit it (click on the pen).

Add some spaces or printfs ...

Scroll down and make sure it is comitted to your branch

Click on "Commit changes"

Now click on you "pull requests" again ...

You should now see a red cross to the right of your pull request. 
Some checks failed!

```
C/C++ CI / build (pull_request) Successful in 3s
Code scanning results / Flawfinder Failing after 4s — 10 new alerts including 1 error, 1 fix
```

Now you need to find the flaw in the software and correct it!


## 2. Assigment Setup a repository with github actions as described above. 


Create your own repository and make the steps of setting up an action that compiles your project.

Test it by making a branch of your code and create a pull-request and see what happens.
Find bad C or C++ coding examples on the net and add it to the sample.c to see if the Flawfinder finds the bad code!

If you got time before lunch, try completing your C++ assignment.

Add the Findflaw action to your C++ assignment!

## 3.  Repetition
I will explain further anything you are unsure about in the previous lessons again.
Think about it and we do repetition of the topics you are unsure about.

Yesterday we covered getopt(), templates (function & class) and when to use . or -> to access attributes and class methods.

