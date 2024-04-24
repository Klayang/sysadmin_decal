###### tgz (1 / 2)

Run the following 2 shell commands, and you'll see a folder called `b01`. Why?

```shell
wget https://github.com/0xcf/decal-labs/raw/master/b1/b01.tgz
tar xvzf b01.tgz
```



###### tgz (2 / 2)

- A `.tgz` file is a composition of 2 file formats. You may see `.tar.gz` instead

- `tar` command is ued to archive multiple files into a single one, with `.tar` postfix
  
  - However, unless you ask it to, it does no compression

- `gzip` will compress your file, and thus `tar + gzip` is often used in conjunction
  
  - `file` -- `(tar)` --> `file.tar` -- `(gzip)` --> `file.tar.gz`

- A `z` option can be given to `tar` command, to compress (or decompress) files 
  
  - Which saves one line of shell command

    

###### A Series of Commands

- Go into the `b01` directory. Run `pwd` (*present working directory*), and we'll see:
  
  <img src="file:///C:/Users/yangs/AppData/Roaming/marktext/images/2024-04-24-11-12-40-image.png" title="" alt="" width="272">

- A hidden file in `b01`. Let's find it out and print its content by `ls -a` & `head`
  
  <img src="file:///C:/Users/yangs/AppData/Roaming/marktext/images/2024-04-24-11-14-04-image.png" title="" alt="" width="416">

    

###### xargs

- In `./nonsense`, a message is split across multiple files. How to find the message?

- `xargs` takes output of one command, and passes it as args to another command

- `cat` is used to concatenate files, then print content on console, or write into a file

- Thus, we can first get all the file names by `ls`, then pass them to `cat`, by `xargs`
  
  ```shell
  > ls | xargs cat
  # standford > berkerly
  ```

    

###### rm

We want to delete everything inside `./nonsense`, with `rm -r ./*`

    

###### grep

- `big_data.txt` in `./b01`, has a size of 80 MBs. Need to find some text there
  
  - The solution is 2 lines above a (and only one) URL in the file

- `grep` (*global regular expression print*) is used for searching text patterns within files
  
  ```shell
  grep [options] pattern [files]
  ```

- *Context Line Control* in Unix, specifically within the `grep` command, refers to:
  
  - The ability to display additional lines surrounding the matching lines
  
  - `-B n`: `n` lines after the match; `-A n`: `n` lines before the match; `-C n`: both

- Therefore, we can first use grep to find the url, and apply `-A 2` to find the solution
  
  <img src="file:///C:/Users/yangs/AppData/Roaming/marktext/images/2024-04-24-11-59-22-image.png" title="" alt="" width="591">

    

###### chmod (1 / 3)

- A file on Unix has 3 types of permissions: `r` (read), `w` (write / delete), `x`(execute)
  
  - Which could be assigned to 3 classes of users (*owner*, *group*, *others*)

- Can check the permission of a file via `ls -l` command, which is a 10-char string
  
  - e.g., `-rw-r--r--` (regular file, can be read&written by owner, read by other 2)

- The `chmod` (*change mode*) can change access permissions of files & directories
  
  - Only root, owner of the file, or user with `sudo` priviledges can do this

    

###### chmod (2 / 3)

```shell
chmod [OPTIONS] [ugoa…][-+=]perms…[,…] FILE...
```

- `[ugoa]` (user flag) defines which user classes the permissions are changed
  
  - `u`: owner; `g`: users in the group; `o`: all other users; `a`: `ugo`
  
  - `a` is the default if this flag is ommitted

- `[-+=]` defines if the permissions are to be removed, added or set
  
  - `-`: remove specified permissions; `+`: add specified permissions
  
  - `=`: change current to the specified permissions; set to none if nothing tailing

- `perms...` can be explicitly set using `>=0` following letters: `r`, `w`, `x`, `X`, `s`, `t`
  
  - Using 1 among `ugo`, is to copy permissions from one to another user class

    

###### chmod (3 / 3)

Now we could give owner the execute permission of `a_script` by:

```shell
> chmod u+x a_script
```

    

###### General Questions (1 / 4)

1. What differentiates Linux and Windows?
   
   - Linux is open-source, Windows is proprietary
   
   - Linux is free, Windows is purchased & pre-installed on pcs

2. What's the difference between the `CLI` & `GUI` usage of an OS?
   
   - `CLI` suits for users who need to perform complex tasks efficiently
   
   - `GUI` suits for general users who prefer visual interaction & simplicity

3. What is the root directory in Linux filesystems?
   
   - The topmost-level directory in the file management system, denoted by a `/` 
   
   - It serves as the base for all other directories & files within the system

    

###### General Questions (2 / 4)

4. How to see the size & have the files ordered by last date edited, oldest on top?
   
   - `ls -ltrh` (`l`: display in long format; `t`: sort by edit time, newest first)
   
   - (`r`: reverse the order of sort; `h`: show the file size in human-readble format)

5. How to use the `head` command to show the first 4 lines of `big_data.txt`?
   
   - `head -n 5 big_data.txt`

6. What’s the difference between `cat foo > out.txt` and `cat foo >> out.txt`?
   
   - The former one overwrites the file, while the latter appends to the file

    

###### General Questions (3 / 4)

7. What is the difference between permissive and copyleft licenses?
   
   - *Permissive* & *copyleft* licenses are 2 categories of open-source licenses that:
   
   - Differs in terms of the condition they impose on redistribution of the software

    

###### Permissive vs. Copyleft (1 / 4)

*Permissive* licenses:

- Less restrictive: users can use, modify, distribute software with fewer restrictions

- Commercial use: users can incorporate the software into proprietary products
  
  - Without disclosing the source code

    

###### Permissive vs. Copyleft (2 / 4)

*Copyleft* licenses:

- More Restrictive: Require that any modified versions of the software 
  
  - Also be distributed under the same license terms

- Source Code Sharing: if the software is redistributed, either modified or not
  
  - The source code must be made available under the same license

    

###### Permissive vs. Copyleft (3 / 4)

- *Permissive* examples: MIT License, Apache License, BSD Licenses

- *Copyleft* examples: GNU General Public License (GPL), Mozilla Public License (MPL)

    

###### General Questions (4 / 4)

8. Give an example of a permissive license: Apache License

9. Give an example of a free, but closed-source software that you use: Skype

    


