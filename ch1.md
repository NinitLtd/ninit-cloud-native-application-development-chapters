### What is BASH ? (Bourne Again Shell)

> `BASH` (Bourne Again Shell ) Allows users to interact with system.

> Shell allows users to run commands, scripts and programs on `CLI` (Command Line Interfrace) and perform various tasks / operations.

Where ever you see `↵` symbol, it indicates the  `enter` key on your keyboard.

`Enter key on shell command prompt indicates the end of current command.`

-----------------------

### `stdin / stdout`

> Standard input -> keyboard

> Standard output  -> Usually the screen of your computer. We can stream output to a file and remote log servers as well. We will look that into bit more details later.

	Q: How to redirect outputs of a command or a scrip to a file ?
	A: with the GREATER-THAN symbol  >

> E.g if we execute following command

	$ ./a.sh > out.txt  ↵

- It will create a new file called `out.txt`. If the file `out.txt` is not present in the current directory.
- It will write the output of that script execution to the file `out.txt`
- If the file `out.txt`  is already present, it will override the content of that file. 

`If you want to add / amend existing file then use two` > ` symbols e.g`  >>

	$ ./a.sh >> out.txt  ↵

`This will amend the existing` **out.txt** `file every time you execute this command and it will create a new out.txt first time if it does not exist.`

	Q: What is a variable ?
	A: Variable is a placeholder to store some value. 
	e.g os=”Linux”  
> In this example the variable name is `os` and the value assigned to it is `Linux`

### Setting up temporary (Ad Hoc) environment variables. 

> While working on a day-to-day basis,  we may sometimes need to set up temporary variables on the SHELL prompt. We can do that using the `export` command.

> E.g say we want to set up variable called msg  with value  “Welcome to the world of Open Source” the 

	$ export msg=”Welcome to the world of Open Source”  ↵
	
**NOTE : Remember to add double or single quotes around strings with spaces and special characters  otherwise it will only print the first word or some part of the string.**
	
> To print out the value assigned to environment variable use echo command

	$ echo $msg ↵

**_FACTS About variable names :_**

`Variables contains lower & upper case alphabets [a-z,A-Z], numbers [0 - 9] and the (underscore sign _ )`

`Variable name must start with either alphabet or the underscore _ sign`

### Exercise : Setup following _environment_ variables using export command and print their values on screen with echo command.

	- Setup a variable called msg1 and value “This is msg1”
	- Setup a variable called _msg1 and value “This is  _msg1”
	- Setup a variable called _MSG1 and value “This is _MSG1”
	- Print out value of msg1 on screen.
	- Print out value of _msg1 on screen.
	- Print out value of _MSG1 on screen.

**NOTE: We can also set up multiple variables from the command line in 1 go with semicolon `(;)` delimiter.**

------

> **Lets try following commands**

	$ export x=varX ; export y=varY; export z=varZ ↵
	$ echo $x ; echo $y ; echo $z ↵
	AND
	$ echo $x $y $z ↵ 

`Notice what is the difference between above output methods to print variables.`

### Exercise : Repeat above both exercises by preparing a shell script called `print.sh`

> So far we saw how to declare and use variables temporarily from the shell prompt.

> Let’s take a look at how to declare them in a script so everytime we execute a script, variables are available.

#### How to declare variables in a script ?

	Lets create a new script named msg.sh.
	Add following lines to that script. 
Lines starting with # ( HASH or POUND ) signs are comments and they don’t have any impact on the script. I.e those lines are ignored.

```
#!/bin/bash
# This line will be ignored as it is starting with # sign.

msg="Welcome to the CNAD class" # This will be ignored as well
# Followng line will print the value of msg variable
echo $msg
```

	To execute the script from the prompt 
	$ sh msg.sh 
	OR
	$ ./msg.sh
	Welcome to the CNAD class

### Exercise: Extend this script `msg.sh`
* Add a new variable called `name=”Your Name”` before the msg variable.
* Change the `msg` variable to insert name variable at the end of the line.
* i.e “Welcome to the CNAD Class : $name”.
* Save the script and test your change.


	```
	$ sh msg.sh 
	Welcome to the CNAD class : Nilesh
	```

> Let's set up a few variables from the bash prompt and try to perform mathematical operations.

	```
	$ export num1=10 ↵
	$ export num2=20 ↵
	$ echo $(( num1 +  num2 )) ↵
	```

> You will see the output on your screen which will be the addition value of those 2 numbers.

### Exercise :  Prepare a script named `sum.sh` which should perform the following when we execute it.

* Print a welcome message - “Welcome to the Math class”
* Declare 2 variables num1 and num2 with positive integer values.
* Add those two numbers.
* Execute that script `sum.sh` and record the output to a file called `sumresults.txt`

```
	$ sh sum.sh 
	OR
	$ ./sum.sh
```

### Lets build a simple, interactive shell script which takes input from user, stores it in variable and prints out along with a string sprcifided by user. 

* The first`read` command allows users to enter value when user execute the script.
* The second argument along with `read` command is `variable name`. The value we enter gets assigned to the variable. e.g in following example we are asking user to enter `name` which will be stored in a variable called `name`
	```
	#!/bin/bash
	echo "Enter your name"
	read name
	echo $name
	```
*  Save above script in file called `name.sh` and execure it from the command prompt. 

### Now lets extend the above script and see how we can call a variable to inject value in another variable. 

* Create a new variable called `msg` with a welcome message and refer to the `name` variable to print a welcome message.

	```
	#!/bin/bash
	echo "Enter your name"
	read name
	msg="Welcome to the Math class : $name"
	echo $msg
	```

### Further lets extend our script so that we can ask user to enter two numbers one by one, assign those two number to a separate variable   and display sum of those 2 numbers.

* We will need to add two more `read` commands to capture user input for numbers.
* Let's say, the next`read` command will receive user input and assign it to variable `num1`.
* Then another `read` command will receive user input and assign it to variable `num2`.


	```
	#!/bin/bash
	echo "Enter your name"
	read name
	msg="Welcome to the Math class : $name"
	echo $msg
	echo "Enter the first number"
	read num1
	echo "Enter the second number"
	read num2
	result=$(( $num1 + $num2 ))
	echo "---------------"
	echo "Addition of $num1 and $num2 is : $result"
	```
### Extend above script to perform :
* Addition for 3 numbers.
* Multiplication for first 2 numbers.
* Store output in a `sum.txt` file.