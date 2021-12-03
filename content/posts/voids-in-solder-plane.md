---
title: 'Voids In the Solder Plane'
date: 2009-01-25T21:10:00.000-08:00
draft: false
---

[![](/images/297720320.JPG)](/images/297720.JPG)  
The picture above is an x-ray from a HP nc6000 laptop's MAXIM MAX1987 chip, which "shows up what look to be voids in the solder plane underneath the MAX chip."  
  
The MAX1987 chip lives on the bottom of our HP nc6000 laptops. Opening and closing the laptop flexes the motherboard near the hinges. Over time, this causes the MAX1987's connection to the motherboard to break. The chip costs [~$8](http://www.pchub.com/uph/laptop/507-29494-6753/Maxim-MAX1987-ETM-IC-Component.html). The cost of a motherboard costs [~$100](http://shop.ebay.com/items/__nc6000-motherboard_W0QQQ5ftrkparmsZ66Q253A2Q257C65Q253A15Q257C39Q253A1QQ_scZ1QQ_sopZ15QQ_trksidZp3286Q2ec0Q2em14?_fpos=95821&_fcid=1&gbr=1). x\_x  
  
The MAX1987 chip regulates power to the CPU (see link below and search for "Thomas Rolfe"). So if it fails, the CPU freezes and cannot recover. Even worse, the faulty connections prevent system start up. The short-term workaround is to press down on the section of the laptop where this chip lives while pressing the power button. The pressure reconnects the chip to the motherboard long enough to start up. Everything works fine as long as the motherboard does not get flexed too much.  
  
The permanent solution is to re-solder the chip. Since this chip does not have "legs" like other chips, it needs to be heated, then cooled, using a [hot air gun](http://www.maplin.co.uk/Module.aspx?ModuleNo=34959&C=Newsletter&U=08P06-1&T=12592445). Other reports say that they have clamped a pin to the end of their soldering iron and heated the chip that way with success.  
  
Last but not least, no thanks to HP for this solution. It came from dedicate users of the link below. HP continues to ignore this issue, to their discredit.  
  
Forum post: [http://forums13.itrc.hp.com/service/forums/bizsupport/questionanswer.do?admit=109447627+1232937065039+28353475&threadId=1046903](http://forums13.itrc.hp.com/service/forums/bizsupport/questionanswer.do?admit=109447627+1232937065039+28353475&threadId=1046903)