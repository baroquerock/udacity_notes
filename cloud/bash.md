# BASH basics


- __echo X__ - repeat the string X back

``` bash
echo hello
hello
```
<br/>
<br/>

- __!!__ - re-run the last command

``` bash
!!
echo hello
hello
```
<br/>
<br/>

- __$X__ - reference of the variable X

``` bash
x=100 
echo $x
100
```
<br/>
<br/>

- __ls__ - list the contents of the current directory

  __ls -l__ - a more detailed list 

  __cd X__ - change directory to X

  __pwd__ - print the current (working) directory
<br/>
<br/>

- Shortcuts:

 . - working directory 

 .. - parent directory

 ~ - home directory
<br/>
<br/>
<br/>

- __mkdir X__ - create a new directory X

  __mv X Y__ - more the file X to the directory Y
<br/>
<br/>

- __curl 'http://www.google.com'__ - download the page

  __curl -L -o some_file.html 'http://www.google.com'__ - download the page following redirects (-L) and outputing the result to the _some_file.html_ (-o)
<br/>
<br/>

- __cat X__ - display the contents of a file to the terminal

  __less X__ - display the contents of a file to the terminal with the possibility to search and scroll
<br/>
<br/>

- Managing the __less__ command:

    scroll down - spacebar or down arrow

    scroll up - b key or up arrow

    search - forward slack /

    exit less - q key
<br/>
<br/>

- __rm X__ - permanently delete the file X

  __rm -i X__ - permanently delete the file X but double check first

  __rm X Y Z__ permanently delete the files X, Y, Z

  __rmdir X__ - permanently delete the directory X (should be empty)

  __rmdir -r X__ - permanently delete the directory X with all it's content


