---
title: 'SyncFusion XlsIO: ListObject'
date: 2019-01-31T19:45:00.002-08:00
draft: false
tags: 
- list object
- syncfusion
- format as table
- listobject
---

SyncFusion XlsIO List Objects seem to represent the result of Microsoft Excel "Format as Table" operation on a worksheet.  
  
The following vb.net code creates a ListObject, then sets the table style:  
  
' Populate the ReportWorksheet  
' ...  
' Table (viz., ListObject)  
ReportWorksheet.ListObjects.Create(name:="AListObjectName", range:=ReportWorksheet.UsedRange).BuiltInTableStyle = TableBuiltInStyles.TableStyleLight15  

  
UPDATE: A previous version of this post mentioned Component Pro, which represents software stolen from SyncFusion and repackaged/resold by Component Pro. More: [http://cheated.by.safabyte.net/](http://cheated.by.safabyte.net/)