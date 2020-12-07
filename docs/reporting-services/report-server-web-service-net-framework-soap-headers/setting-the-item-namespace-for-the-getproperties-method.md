---
description: GetProperties メソッドのアイテム名前空間の設定
title: GetProperties メソッドのアイテム名前空間の設定 | Microsoft Docs
Description: GetProperties メソッドと ItemNamespaceHeader SOAP ヘッダーを使用して、項目のパスまたは ID に基づいてプロパティを取得する方法について説明します。
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-soap-headers
ms.topic: reference
helpviewer_keywords:
- item properties [Reporting Services]
- ItemNamespaceHeader SOAP header
- GetProperties method
ms.assetid: b0a08639-3101-40a2-abe2-3a41753826d1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fc0d61726a885b6a2422a4fe048121e65b8642f8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423246"
---
# <a name="setting-the-item-namespace-for-the-getproperties-method"></a>GetProperties メソッドのアイテム名前空間の設定
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] で <xref:ReportService2010.ItemNamespaceHeader> SOAP ヘッダーを使用すると、アイテムの完全なパスとアイテムの ID という 2 つの異なる識別子に基づいてアイテムのプロパティを取得できます。  
  
 <xref:ReportService2010.ReportingService2010.GetProperties%2A> メソッドへの呼び出しを作成する場合、一般的にはプロパティを取得するアイテムの完全なパスを引数として渡します。 <xref:ReportService2010.ItemNamespaceHeader> を使用すると、メソッド呼び出しの SOAP ヘッダーを設定して、アイテムの ID を識別子として渡すことによって <xref:ReportService2010.ReportingService2010.GetProperties%2A> を使用できます。  
  
 次のコード サンプルは、アイテムの ID に基づいてアイテムのプロパティ値を取得します。  
  
> [!NOTE]  
>  既定では、<xref:ReportService2010.ItemNamespaceHeader> メソッドに完全なパス名をアイテム識別子として渡す場合は、<xref:ReportService2010.ReportingService2010.GetProperties%2A> の値を設定する必要がありません。  
  
```vb  
Imports System  
Imports System.Collections  
  
Class Sample  
   Sub Main()  
      Dim rs As New ReportingService2010()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
      rs.Url = "https://<Server Name>/reportserver/ReportService2010.asmx"  
  
      Dim items() As CatalogItem  
  
      Try  
         ' Need the ID property of items. Normally, you would already have   
         ' this stored somewhere.  
         items = rs.ListChildren("/AdventureWorks Sample Reports", False)  
  
         ' Set the item namespace header to be GUID-based  
         rs.ItemNamespaceHeaderValue = New ItemNamespaceHeader()  
         rs.ItemNamespaceHeaderValue.ItemNamespace = ItemNamespaceEnum.GUIDBased  
  
         ' Call GetProperties with item ID.  
         If Not (items Is Nothing) Then  
            Dim item As CatalogItem  
            For Each item In  items  
               Dim properties As [Property]() = rs.GetProperties(item.ID, Nothing)  
               Dim property As [Property]  
               For Each property In  properties  
                  Console.WriteLine(([property].Name + ": " + [property].Value))  
               Next property  
               Console.WriteLine()  
            Next item  
         End If  
  
      Catch e As Exception  
         Console.WriteLine((e.Message + ": " + e.StackTrace))  
      End Try  
   End Sub 'Main  
End Class 'Sample  
```  
  
```csharp  
using System;  
using System.Collections;  
  
class Sample  
{  
   static void Main()  
   {  
   ReportingService2010 rs = new ReportingService2010();  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
      rs.Url = "https://<Server Name>/reportserver/ReportService2010.asmx";  
  
      CatalogItem[] items;  
  
      try  
      {  
         // Need the ID property of items. Normally, you would already have   
         // this stored somewhere.  
         items = rs.ListChildren("/AdventureWorks Sample Reports", false);  
  
         // Set the item namespace header to be GUID-based  
         rs.ItemNamespaceHeaderValue = new ItemNamespaceHeader();  
         rs.ItemNamespaceHeaderValue.ItemNamespace = ItemNamespaceEnum.GUIDBased;  
  
         // Call GetProperties with item ID.  
         if (items != null)  
         {  
            foreach( CatalogItem item in items)  
            {  
               Property[] properties = rs.GetProperties(item.ID, null);  
               foreach (Property property in properties)  
               {  
                  Console.WriteLine(property.Name + ": " + property.Value);  
               }  
               Console.WriteLine();  
            }  
         }  
      }  
  
      catch (Exception e)  
      {  
         Console.WriteLine(e.Message);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>参照  
 [テクニカル リファレンス (SSRS)](../../reporting-services/technical-reference-ssrs.md)   
 [Reporting Services の SOAP ヘッダーの使用](../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)  
  
  
