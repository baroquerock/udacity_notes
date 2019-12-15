# BASH basics


1. __echo X__ - repeat the string X back

``` bash
echo hello
hello
```


2. __!!__ - re-run the last command

``` bash
!!
echo hello
hello
```

3. __$X__ - reference of the variable X

``` bash
x=100 
echo $x
100
```

4. __ls X__ (list) - list the contents of the X directory

   __cd X__ (change directory) - 

ls - 
cd 
cd ..
ls ..


shortcuts
Working directory .
Parent directory ..
Home directory ~

pwd Print the current (working) directory to the terminal.


Absolute vs. relative path
relative to your current location (the current working directory).
a partial path to the directory you want to go, as long as the partial path includes all the steps needed to get there from wherever you're currently located.

The other option is to give an absolute path. This is where you provide the full path, all the way from the home directory.

cd /home/workspace/Desktop/Photos


cd ~



ls -l(ong)
a more detailed list


ls *.txt

mkdir - create a new dir
mv X Y move the file X to the dir Y


curl 'http://www.google.com'
Note: You may have noticed we put single quotes ' around the URL. A lot of URLs have special characters in them, such as the & sign, which have unusual meanings to the shell. That's why we're always putting these URLs in quotes … even though these particular examples would work without them, it's a good practice to get into.

If you add the -L option to curl, it will first follow any redirects, and then download the file from wherever the redirects ultimately go. In other words, if you enter:


Following redirects (-L)


Output to a file (-o)
By default, curl will output whatever it downloads directly to the terminal. This typically results in a big mess of code filling up your terminal window, something that isn't always particularly useful.

Instead, you can tell curl to output the data to a file by adding the -o option:

curl -L -o 'http://www.google.com'
Of course, it also needs to create a file to put the data into, so you'll need to tell it that as well:

curl -L -o some_file.html 'http://www.google.com'



cat and less
Karl described two ways of viewing the contents of a file. The cat command will display the full contents of the file:

cat dictionary.txt
The limitation is that files often have more text than will fit on the screen at once. When that's the case, you can use less, as in:

less dictionary.txt
This displays the output in a format that allows you to search and scroll.


Once you've started the less program, you can use some different keys to move around. See if you can remember which key to press for each of these things:


Scroll down. - spacebar or down arrow


Scroll up. - b key or up arrow


Search. forward slack /

 
Exit less. q key


rm example
rm -i example (permanently but double checl)

rmdir example1 example2 example3


By the way, when using the rmdir command, it will only delete a directory that is empty. If the directory has files inside, you'll get an error saying Directory not empty. This helps prevent you from accidentally deleting a folder that contains a bunch of files.



















