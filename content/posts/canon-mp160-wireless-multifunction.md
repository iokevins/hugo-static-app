---
title: 'Canon MP160 + Wireless Multifunction Print Server'
date: 2008-02-10T18:31:00.000-08:00
draft: false
---

Wireless multifunction print servers have a few pitfalls--here's what I've been through.  
  
I own a [Canon Pixma MP160 multifunction USB 2.0 printer](http://www.usa.canon.com/consumer/controller?act=ModelInfoAct&fcategoryid=116&modelid=13368). Originally, I connected it to my laptop's docking station using a GigaWare four-port USB 2.0 hub and shared it on the network from my laptop. The downsides of this configuration:  

*   Undocking the laptop removes the printer from the network.
*   Once undocked, other laptops can still print, but they have to have a separate printer driver installed for local rather than remote printing, and they obviously have to hoof it over to the printer.
*   Desktops that rely on the shared printer are out-of-luck.  
    

Obviously a non-optimal solution. A wireless print server, theoretically, would mean all wireless-enabled desktops and laptops can print from wherever they are in the house.  
  
The seed of this idea has been in my head for several months. An opportunity to remedy the situation presented itself while I was shopping at a local tech store two weeks ago. On impulse (in hindsight, a regrettable decision) I purchased a [Linksys Wireless G print server](http://www.linksys.com/servlet/Satellite?c=L_Product_C2&childpagename=US%2FLayout&cid=1114037289494&pagename=Linksys%2FCommon%2FVisitorWrapper). Getting home, I discovered in my ignorance that print server manufacturers typically break down print servers into two sets--those that support multifunction printers and those that don't. The Linksys Wireless G print server doesn't support multifunction printers. Above and beyond that limitation, the installation and configuration process of the Linksys Wireless G proved frustrating:  

*   The print server web server crashes if you begin navigating from the home page. To avoid this bug, one has to [start navigating](http://forums.linksys.com/linksys/board/message?board.id=Wireless_Print_Servers&message.id=677) the print server's web server from http://\*ip\*/ps\_stat.htm. That's scary quality control.
*   Without knowing this trick, even though you set the local wireless SSID security key, it doesn't take--so it's even worse from the user's point of view, since they think they did everything right.

After researching this on the internet, I decided that I wasn't happy with the bugs and the loss of multifunction printing support for the price, and returned it.  
  
Before I did that, I decided to research wireless multifunction print servers further. My local tech store sells print servers from Hawking, D-Link, Linksys, AirLink, and TrendWare. I ignored the multifunction version from Linksys and decided after reading reviews online that the [D-Link Rangebooster G Multifunction print server](http://www.dlink.com/products/?sec=0&pid=482) represented the best bet. I knew from reading their web site that the Canon MP160 wasn't listed as [supported](http://support.dlink.com/faq/view.asp?prod_id=2316&question=DPR-1260) under the FAQ, but I decided to take a risk since they only had reviewed HP and Epson. This represented my second learning opportunity.  
  
Last night I hooked it up, and after a quick call to tech support (it needed a static IP to work), got it working. D-Link tech support confirmed that it doesn't work with the MP160 multifunction printer, however. Other than it's failure to work with DHCP, the D-Link seemed like a quality product.  
  
I finally got the idea to just call Canon and ask them point-blank what works with their printers. It turns out that they sell a model called the [Silex C-6700WG](http://estore.usa.canon.com/Specification.asp?ITEM_ID=37188) that works with the Canon printers. Unfortunately, it's $100. \*sigh\* I guess this is what is meant by vendor lock-in. I haven't decided whether or not to buy it, since in the future I'm hoping to upgrade to a color laser printer  
  
So why does it seem so hard to get printing right for multifunction printers? The answer seems to be (from TrendNet's now defunct page):  

> Printers that host multiple functions, such as faxing and scanning, use different communication standards to complete respective tasks. Traditional print servers are unable to interface with multi-function printers due to the use of different communication standards within one device. The result is that many multi-function printers are not currently linked to a home or office network.

So there you have it--multifunction print servers need to be fluent in fax, scanner, copier and printer standards--and apparently the communication pipeline of printer-driver<->print-server<->printer is pretty fragile.