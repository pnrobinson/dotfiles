##############
VIM cheatsheat
##############


Basic operations
~~~~~~~~~~~~~~~~

* d: delete
* c: change (delete and enter insert mode)
* >: indent
* v: visually select
* y: yank (i.e., copy)
* .: (dot) repeat last command

Moving around
~~~~~~~~~~~~~

* w: move forward by one 'word'
* b: move back by one word
* j: move down by one line (5j: move down by 5 lines)
* e.g., :42  go to line 42

Text objects
~~~~~~~~~~~~

* iw: inner word
* it: inner tag (e.g.,HTML tag)
* i": inner quotes
* ip: inner paragraph
* as: a sentence

Parameterized text objects
~~~~~~~~~~~~~~~~~~~~~~~~~~
 
* f,F: find the next character
* t,T: 
* /,?: 

Copy paste from system clipboard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Enter insert mode and <CTRL><SHIFT>-v


Plugins
~~~~~~~

Nerdtree
^^^^^^^^

cd .vim/bundle
git clone https://github.com/scrooloose/nerdtree.git

To start automatically add the following to .vimrc

`autocmd vimeneter * if !argc() | NERDTree | endif`


Fugitive
^^^^^^^^

Git client
mkdir -p ~/.vim/pack/tpope/start
cd ~/.vim/pack/tpope/start
git clone https://tpope.io/vim/fugitive.git
vim -u NONE -c "helptags fugitive/doc" -c q

