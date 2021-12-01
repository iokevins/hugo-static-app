---
title: 'Sublime Text 2 nitpickiness'
date: 2012-05-27T17:13:00.000-07:00
draft: false
---

Some issues with Sublime Text 2:  

*   Selecting block of text (for example, using column selection via SHIFT + right-mouse button), scrolling back to the top of the block of selected text, and then indenting/outdenting moves changes the visible window screen area back down to the beginning of the cursor position. It should stay with where I scrolled to.
*   Column selecting a block of text and CTRL + dragging that text to a blank part of the line (for example, to the left) should append the column-selected text to each line in turn. Instead, it inserts all the text on the line at and under the cursor.
*   I emit spaces for tabs, but selecting Backspace goes back one full tab stop instead of one space. 
*   I CTRL + H to search/replace, type in the Find field, tab to get to the Replace field, and it does not auto-highlight the existing value; also, I cannot hit CTRL+A to replace all occurances
*   After column selecting, SHIFT + TAB continues to indent instead of outdenting; backspace does outdent (normally, TAB indents while SHIFT+TAB outdents)
*   Entered Distraction free mode and copied the same preferences from Preferences > Settings - Default to Preferences > Settings - More > Distraction Free - User, and the font and font size got all messed up. Leaving Distraction free mode reverts back to the "stock" font and size. Corrected by deleting everything from the Distraction Free preferences except for "color\_scheme"....
*   Word wrap...always on even though I have disabled in all the Preferences.....OK, turns out you have to edit file  %APPDATA%\\Sublime Text 2\\Packages\\Default\\Distraction Free.sublime-settings or   %APPDATA%\\Sublime Text 2\\Packages\\User\\Distraction Free.sublime-settings .... there may or may not be a difference between "false" and false....(no quotes)...even though Sublime Text 2 shows that as the default? These detailed file settings seem like a double-edged sword...pretty cool now that I am looking at them.
*   Right-clicking at a spot (for example, the end of line) and selecting Paste pastes the text at where the cursor was, not where you right-click.
*   Keeps forgetting I have selected "In Selection" for Search/Replace
*   Column-selecting text and indenting/outdenting does not display the column number as I go...