# Github Classroom

## Context/Problem
I've been using Github Classroom for a year, and I absolutely love it for distributing and collecting code. I've enjoyed how the Classroom Assistant can quickly download repos. However, my biggest frustration was not being able to `pull` new changes (and having to go through the entire process of downloading again). In this course, I learned that apparently `git pull` in fact _does_ work, but only for a limited time. Unfortunately, its expiration date is too soon to use practically. 

## Inspiration
The inspiration for the solution to this problem was a hybrid between two factors:
* [Lyuba](https://github.com/lfridman2016) asked if there was a way to keep all of our unplugged lesson plans in the same place, which made me want to hop on the bash scripting train.
* [Topher](https://github.com/tofr) mentioned scripting a command to automatically pull, assuming all repos were already downloaded manually:
```bash
for student in *; do cd $student; echo $student; git pull; cd ..; echo; done
```
Topher mentioned that he uses Google Sheets to generate the scripts, but I wanted to see if I could do it all in the terminal.

## Process
* As I tested this script throughout the process of building it, I found it incredibly useful to do all testing in a temporary directory, where I could easily remove unwanted folders that got created, etc.
* At first, my script included doing `mkdir` for each student, `cd`'ing into the folder, then `git clone`-ing. I forgot to `cd ..`, so of course, the nesting got really hairy. Delete!
* But more importantly, the default `clone` behavior is to **create** a folder. So I would end up with a less-than-desirable file tree like this:
```
├── student1
│   └── assignment-student1
│       ├── README.md
│       ├── index.html
│       ├── script.js
│       └── style.css
└── student2
    └── assignment-student2
        ├── README.md
        ├── index.html
        ├── script.js
        └── style.css
```
It's apparent that it was redundant to make a folder for each student. Without making the folder, `clone`-ing will result in every folder starting with the assignment name, but that leads to more work when I want to `cd`. The whole point of this is to work smarter, not harder, right?

Luckily `git clone` has the ability to clone into a folder (pre-existing _or_ created on-the-fly), i.e. `git clone URL folder`. So without further adieu...

## Result

```bash
org=hstatsep-students
repo=hello-world
students=(
githubUsername1
githubUsername2
githubUsername3
)
mkdir $repo
cd $repo
for student in "${students[@]}"
do 
	echo cloning $student
	git clone git@github.com:$org/$repo-$student $student
	echo ""
done

```
If you'd like to use the script, just update the `org`, `repo`, and `students`.

What's nice about Github Classroom is that it will generate a CSV for  individual students on your roster, but _also_ for group projects. Example of final result:

```
└── assignment
    ├── student1-student2-student3
    │   ├── README.md
    │   ├── index.html
    │   ├── script.js
    │   └── style.css
    ├── student4-student5
    │   ├── README.md
    │   ├── index.html
    │   ├── script.js
    │   └── style.css

```

Done!

## Other helpful scripts


### Printing file contents
```bash
org=hstatsep-students
file=index.html
repo=${PWD##*/}
for student in *
do
	echo $student
	echo http://github.com/$org/$repo-$student
	bat $student/$file --theme=ansi-light --paging=never
	printf "\n\n\n********************************\n\n"
done
```
* Update the `org`. This is used to create a link in case you want to see the file on github.com (on a Mac: <kbd>command+doubleClick</kbd> the printed link).
* Update the `file` you want to print.
* You won't need to update the `repo`, as it will go grab the name of the current directory (what `pwd` returns, i.e. `hello-world`).
* You will probably need to install `bat` first. It's like `cat`, but with color-coding.

### Opening files
```bash
file=index.html; for student in *; do echo $student; open $student/$file; done
```
* Update `file`

### Listing files
```bash
for student in *; do echo $student; ls $student; printf "\n\n\n********************************\n\n"; done
```

### Printing number of commits
```bash
for student in *; do echo $student; cd $student; git rev-list --all --count; cd ..; printf "\n\n\n********************************\n\n"; done
```

### Printing commits
```bash
for student in *; do echo $student; cd $student; git rev-list --all --count; cd ..; printf "\n\n\n********************************\n\n"; done
```
* Often requires you to press <kbd>q</kbd> to `quit` to jump to next student. (let me know if you have a workaround)



[Home](../index.md)