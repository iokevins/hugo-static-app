---
title: 'SunRocket + Panasonic KX-FP145 Fax Machine'
date: 2007-04-16T15:37:00.000-07:00
draft: false
---

[![](/images/KX-FP145320.jpg)](/images/KX-FP145.jpg)  
In a pinch, I purchased the [Panasonic KX-FP145](http://wize.com/fax-machines) fax-machine last week so I might reliably send and receive faxes from my home. I use [SunRocket](http://sunrocket.com/) VOIP service, and purchased it after reviewing their web site for compatibility. SunRocket uses G.711 for VOIP and fax. It also supports T.38 for fax transmissions in cases where a phone company doesn't support G.711.  
  
The KX-FP145 doesn't come with a pass-through line, so on the advice of a friend I installed a line-cord splitter into the port on the [Gizmo AC-211](https://www.sunrocket.com/_resources/pdf/ac211_install_web.pdf). One line-cord from the splitter goes to the fax machine and the other goes to the phone system (in my case, two SunRocket-provided [Uniden DCT746](http://uniden.com/products/productdetail.cfm?product=DCT746M&page=2) telephones). Panasonic provides a digital version of the KX-FP145 manual [here](http://www2.panasonic.com/webapp/wcs/stores/servlet/vProdSupportModel?displayTab=R&surfModel=KX-FP145&modelNo=KX-FP145&storeId=15001&amp;catalogId=11017&itemId=70389&displayServiceCenter=true#) (PDF, 7MB) if you want to refer to it while reading the following.  
  
I performed these steps to configure it to work with SunRocket:  

1.  Insert a line-cord splitter into port Phone 1 on the gizmo. Connect line-cords from the splitter to the existing phone system and fax machine.  
    
2.  Configure fax machine:  
    

1.  Assign your extra phone number (SunRocket's Signature Account number) to be the fax machine number. See the KX-FP145 manual, page 23, for details. If you don't know your extra phone number, log-in to the SunRocket web site or call SunRocket customer support.  
    
2.  Set up the fax to use Distinctive Ring mode. When someone calls the extra phone number, the fax machine will recognize the distinctive ring and know it's a fax. See the KX-FP145 manual, page 17, for details.

1.  Note: In FAX ONLY mode, the answering machine picks up every call.  
    

4.  Activate Distinctive Ring. See KX-FP145 manual, page 38, for details.
5.  Set up the fax to answer after four rings--see page 51 of the manual (Code #06: Changing the ring setting in TAM/FAX mode (Telephone Answering Machine/Fax mode)).

4.  Configure SunRocket:

1.  Change voice-mail for Household Account number to three rings.
2.  Change distinctive ring for Signature Account number to two-four.  
    

That's it!  
  
Advantages of this setup:  

*   Use fax machine and external telephone(s) independently on same SunRocket line
*   Use SunRocket voice-mail instead of fax machine's answering machine  
    

Disadvantages of this setup:  

*   Reduces SunRocket's rings-to-answer to three to bypass the fax machine's answering machine. The fax machine's answering machine picks up after four rings--even if the call is placed to the telephone number.

Notes:  

*   SunRocket's distinctive rings map to the Panasonic KX-FP145 distinctive rings like this:

*   SunRocket Ring 1 -> KX-FP145 Ring A (one long ring)  
    
*   SunRocket Ring 2 -> KX-FP145 Ring B (two short rings)  
    
*   SunRocket Ring 3 -> KX-FP145 Ring D (short-short-long rings)  
    
*   SunRocket Ring 4 -> KX-FP145 Ring C (short-long-short rings)