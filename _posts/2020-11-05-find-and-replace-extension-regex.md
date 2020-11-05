---
layout: post
title: Find and replace basics with `find` and `sed`
tags: [bash, shell, find, sed, xargs]
author: Ozan Öğreden
comment: false
---

I'm pretty comfortable with within-file find and replace operations since I know the regex syntax well.
I'm way less confident with finding and replacing across files.

I finally sat down smoe time to learn about this.

## Goal

Make find and replace for `s/old_name/new_name/g` in files with certain extensions, in specified folders.

### Find and replace

`sed` is the tool to go here.
The syntax for making inplace changes in one file is:

```
sed -i '' 's/old_name/new_name/g' file
```

Note the `''` after `-i` (`--in-place`) option.
This isn't required for all flavors of `sed`, but _is_ required on macOS.

For a dry run, you can use:

```
sed -n 's/old_name/new_name/gp' file
```

### Find files in a directory

`find` is the tool to go for this.

The syntax for a simple version of the task at hand looks like this:

```
find . -type f -name "*.py" 
```

You can specify a folder name prefix to filter folders to be searched:

```
find data-* -type f -name "*.py" 
```

It's common that you might need other extensions.
`-o` (or ;)) option will help you here:

```
find . -type -f -name "*.py" -o -name "*.pyc"
```

### Combining 

This was the trickiest bit for me...

We'll need [xargs](https://en.wikipedia.org/wiki/Xargs) for this.

I tried, but this failed due to file/folder names containing spaces.

```
find . -type -f -name "*.py" -o -name "*.pyc" | xargs sed -i '' 's/old_name/new_name/gp'
```

That problem can be solved by using `-print0` option of the find and `-0` option of xargs.
The former makes `find` print null terminated strings, and the latte makes `xargs` split arguments at null characters:

```
find . -type -f -name "*.py" -o -name "*.pyc" -print0 | xargs -0 sed -i '' 's/old_name/new_name/gp'
```

This would not make all the changes, for some reason!
The reason was the innocent looking `-o` option:
I expected that `-print0` would hold for the whole statement, but that was not the case.

The solution then becomes:

```
find . -type -f \( -name "*.py" -o -name "*.pyc" \) -print0 | xargs -0 sed -i '' 's/old_name/new_name/gp'
```

Voilà!

p.s. If you're not familiar with shell utilities and the options, check out the excellent [explainshell.com](https://explainshell.com/explain?cmd=true%20%26%26%20%7B%20echo%20success%3B%20%7D%20%7C%7C%20%7B%20echo%20failed%3B%20%7D).
