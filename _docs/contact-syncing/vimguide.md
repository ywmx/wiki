  Vim Text Editor Guide  body { background-color: black; color: white; font-family: monospace; font-size: 18px; }  [SpaceLegion.wiki](index.html)  

Vim Text Editor Guide

  

Every letters in vim are case sensitive

=======================================

  
  

i -for insert mode

  
  

esc -escape from insert mode & go to command mode

  
  

j -move down

  
  

k -move up

  
  

l -right

  
  

h -left

  
  

:wq -to save and exit vim

  
  

:w -save changes and stay in vim

  
  

shift+zz -another way to save and exit

  
  

:q -exit vim

  
  

:q! -exiting without saving changes

  
  

dd -deletes a line in command mode (to delete multiple eg: 10dd, deleting a line will copy it to your clipboard)

  
  

G -go to bottom

  
  

gg -go to top

  
  

} -skips a block of code (combine d to delete a block of code)

  
  

{ -reverse the process

  
  

Use number in front of movement keys to reach specific line eg: 20j, 10k, h50, 70l, 20{, }100

  
  

u -to undo

  
  

control+r -to redo

  
  

To undo or redo multiple actions eg: u20 or ctrl+50

  
  

control+r -to redo

  
  

. -repeat the latest action (add numbers in front to multiply)

  
  

yy -copies line to clipboard

  
  

p -paste below

  
  

P -paste above

  
  

V -visual mode (In visual mode use combination of G,gg,h,j,k,l,dd,yy,{,} and other work arounds to highlight,delete and copy etc)

  
  

o -goes to insert mode and add new line below cursor

  
  

O - same thing above the cursor

  
  

w - moves to the next word

  
  

W - skips space

  
  

b - backwards a word

  
  

:"line number" -go to a specific line

  
  

0 -beginning of the line (use w0 combo)

  
  

t -go to a charactor, eg: t&

  
  

f -go to a charator with cursor on it, eg: f#

  
  

% -deletes code between a block, bring cursor to the beginning of block and d%

  
  

:tabnew - creates new tab in vim, (tab to auto complete)

  
  

:tabprevious - go to previous tab

  
  

:wq "file name" - saving a file in a new tab

  
  

:tabNext - routes through tabs, if there are multiple tabs

  
  

:terminal - opens a terminal in vim

  
  

ctrl+ww - switch between editor and terminal

  
  
  

/"character or pattern" - search in vim (use n and N to navigate through search terms)

  
  
By **[Nebulaxyz](https://github.com/nebulaxyz)**