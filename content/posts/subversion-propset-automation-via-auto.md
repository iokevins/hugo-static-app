---
title: 'subversion propset automation via auto-props'
date: 2008-02-24T10:57:00.000-08:00
draft: false
---

Found it:  
  
Link: [http://svnbook.red-bean.com/en/1.1/ch07.html#svn-ch-7-sect-1.3.2](http://svnbook.red-bean.com/en/1.1/ch07.html#svn-ch-7-sect-1.3.2)  
  
config on my host currently reads:  

> ...  
> enable-auto-props = yes  
>   
> \### Section for configuring automatic properties.  
> \### The format of the entries is:  
> \### file-name-pattern = propname\[=value\]\[;propname\[=value\]...\]  
> \### The file-name-pattern can contain wildcards (such as '\*' and  
> \### '?'). All entries which match will be applied to the file.  
> \### Note that auto-props functionality must be enabled, which  
> \### is typically done by setting the 'enable-auto-props' option.  
> \[auto-props\]  
> \*.c = svn:eol-style=native;svn:keywords=Id Date LastChangedDate HeadURL URL Author LastChangedBy Rev Revision  
> \*.cpp = svn:eol-style=native;svn:keywords=Id Date LastChangedDate HeadURL URL Author LastChangedBy Rev Revision  
> \*.h = svn:eol-style=native;svn:keywords=Id Date LastChangedDate HeadURL URL Author LastChangedBy Rev Revision  
> \*.dsp = svn:eol-style=CRLF;svn:keywords=Id Date LastChangedDate HeadURL URL Author LastChangedBy Rev Revision  
> \*.dsw = svn:eol-style=CRLF;svn:keywords=Id Date LastChangedDate HeadURL URL Author LastChangedBy Rev Revision  
> \*.sh = svn:eol-style=native;svn:executable;svn:keywords=Id Date LastChangedDate HeadURL URL Author LastChangedBy Rev Revision  
> \*.txt = svn:eol-style=native;svn:keywords=Id Date LastChangedDate HeadURL URL Author LastChangedBy Rev Revision  
> \*.png = svn:mime-type=image/png  
> \*.jpg = svn:mime-type=image/jpeg  
> Makefile = svn:eol-style=native;svn:keywords=Id Date LastChangedDate HeadURL URL Author LastChangedBy Rev Revision  

Notes:  

*   Quotes in file "config" prevented subversion from updating property Id in my test file. For example, this does not work:

*   \*.cpp = svn:eol-style=native;svn:keywords="Id ..."

*   Whitespace confuses subversion propset application. For example:

*   This works:

*   $Id$
*   $Id:$

*   This does not work (note the whitespace):

*   $Id : $  
    

*   Steps I applied to test:

*   Add this example header to a dummy file (new.cpp):  
    /\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
    \* #  
    \* # Author: author  
    \* #  
    \* # $Id: $  
    \* #  
    \* # \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*/
*   svn add new.cpp

*   A new.cpp  
    

*   svn proplist --verbose new.cpp

*   Properties on 'new.cpp':  
    svn:keywords : Id Date LastChangedDate HeadURL URL Author LastChangedBy Rev Revision  
    svn:eol-style : native  
    

*   svn commit new.cpp -m "Initial revision"

*   Replacing new.cpp  
    Transmitting file data .  
    Committed revision 11.  
    

*   cat new.cpp

*   /\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
    \* #  
    \* # Author: author  
    \* #  
    \* # $Id: new.cpp 11 2008-02-24 19:26:30Z user $  
    \* #  
    \* # \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*/
*   Italicized items above represent environment-specific text