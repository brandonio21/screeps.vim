screeps.vim
===========

This is a small extension of the standard vim syntax file for javascript so that
vim highlights all the keywords and constants from [screeps](http://screeps.com)

Usage
-----
Usage is a little tricky since you probably want to keep the default behaviour
of *.js files opening with Javascript syntax highlighting, but screeps .js files
opening with Javascript+Screeps syntax highlighting. I solved the problem in the
following way:  
1) Copy `screeps.vim` to `~/.vim/syntax/screeps.vim`  
2) Add this line to my ~/.vimrc:  
```
au BufRead,BufNewFile *.screepsjs set syntax=screeps
```
3) Instead of pushing my code to screeps using the standard `grunt screeps`, I
use the following bash script, which copies all files with the *.screepsjs
extension to files with the *.js extension, calls `grunt screeps`, and then
removes the *.js files.
```bash
#!/bin/bash

for file in ${PWD}/code/*.screepsjs; do
	cp ${file} $(echo ${file} | sed 's/screepsjs/js/')
done

grunt screeps

for file in ${PWD}/code/*.js; do
		rm ${file}
done
```
