---
title: 'Regex: Replace "Not a Is Nothing" With "a IsNot Nothing"'
date: 2020-04-03T16:58:00.002-07:00
draft: false
tags: 
- regex
- visual studio
- regular expression
- vb.net
---

In Microsoft Visual Studio Community 2019, updating legacy Visual Basic.NET (VB.NET) code to use the [IsNot operator](https://docs.microsoft.com/en-us/dotnet/visual-basic/language-reference/operators/isnot-operator) is a mild readability boost.  
  
Here's a solution using Regular Expressions.  
  
In Microsoft Visual Studio Community 2019:  
  
Edit > Find and Replace > Replace in Files  
  
Find: (Not )(.\*)( Is )(.\*)  
Replace: $2 IsNot $4  
  
Configuration:  
Use regular expressions: Checked  
Look in: Current document