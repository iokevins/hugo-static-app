---
title: 'GDB and Ignoring Break Points on the First Instruction'
date: 2007-05-21T23:33:00.000-07:00
draft: false
---

I wondered this semester why GDB ignores breakpoints on the first instruction:  

> GDB normally ignores breakpoints when it resumes execution, until at least one instruction has been executed. If it did not do this, you would be unable to proceed past a breakpoint without first disabling the breakpoint. This rule applies whether or not the breakpoint already existed when your program stopped. [Source](http://sourceware.org/gdb/current/onlinedocs/gdb_6.html).