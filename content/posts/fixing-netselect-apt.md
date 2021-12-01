---
title: 'Fixing netselect-apt'
date: 2007-11-18T22:13:00.000-08:00
draft: false
tags: 
- linux
- debian
---

netselect-apt efficiently chooses the fastest download mirror for Debian packages out of a list of several hundred mirrors worldwide.  
  
Unfortunately, I noticed after installing a new version of Debian Etch that _netselect-apt_ failed with the message:  
  

netselect was unable to find a mirror, this probably means that  
you are behind a firewall and it is blocking traceroute.  

  
It turns out netselect-apt::_run\_netselect()_ produces this error when it fails to parse the HTML of the _Debian worldwide mirror sites_ page at [http://www.debian.org/mirror/mirrors\_full](http://www.debian.org/mirror/mirrors_full). This page no longer contains _\\n\\n_ delimiters.  
  
Last week, I resolved the problem by modifying _run\_netselect()_ to use "<br><br>" instead (highlighted):  
`  
run_netselect()  
{  
        SEARCH="$1"  
    PROTO="$2"  
    netselect -v -s 1 $(cat "$infile" \  
        | perl -n -e '  
            **$/="<br><br>";**  
            while(<>){  
              next if $_ !~ /Site:/;  
              if( m@'"$SEARCH"':.*<a href="('"$PROTO"'://.*?)">@i ){  
                    print("$1\n");  
              }  
            }') \  
        | awk '{print $2}'  
}`  
  
I also removed the check for _Archive Architectures_, since the phrase no longer appears on the page.  
  
Also, I noticed after patching _netselect-apt_ that running _netselect-apt_ occasionally fails due to negative values for _netselect_ field _host->num\_out_, but this is a bug for the _netselect_ package, not _netselect-apt_ .