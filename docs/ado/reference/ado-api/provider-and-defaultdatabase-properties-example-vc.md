---
description: Provider および DefaultDatabase プロパティの例 (VC++)
title: Provider および DefaultDatabase プロパティの例 (VC + +) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- provider property [ADO], VC++ example
- DefaultDatabase property [ADO], VC++ example
ms.assetid: d9868c99-425a-4b10-af67-1929ed513fda
author: rothja
ms.author: jroth
ms.openlocfilehash: 5842bbdfc43a76797dd48aa75db133b9942a368e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989923"
---
# <a name="provider-and-defaultdatabase-properties-example-vc"></a>Provider および DefaultDatabase プロパティの例 (VC++)
この例では、異なるプロバイダーを使用する3つの[接続](./connection-object-ado.md)オブジェクトを開くことによって、[プロバイダー](./provider-property-ado.md)プロパティを示します。 また、 [defaultdatabase](./defaultdatabase-property.md) プロパティを使用して、Microsoft ODBC プロバイダーの既定のデータベースを設定します。  
  
```  
// Provider_and_DefaultDatabase_Properties.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ProviderX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   ProviderX();  
   ::CoUninitialize();  
}  
  
void ProviderX() {  
   HRESULT hr = S_OK;  
  
   // Define ADO object pointers.  Initialize pointers on define. These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection1 = NULL;  
   _ConnectionPtr pConnection2 = NULL;  
   _ConnectionPtr pConnection3 = NULL;  
  
   try {  
      // Open a Connection using the Microsoft ODBC provider.  
      TESTHR(pConnection1.CreateInstance(__uuidof(Connection)));  
      pConnection1->ConnectionString = "DSN=Data;user id='MyUserId';password='MyPassword';";  
      pConnection1->Open("", "", "", adConnectUnspecified);  
      pConnection1->DefaultDatabase = "pubs";  
      // Display the provider  
      printf("\n\nConnection1 provider: %s \n\n", (LPCSTR)pConnection1->Provider);  
  
      // Open a connection using the OLE DB Provider for Microsoft Jet.  
      TESTHR(pConnection2.CreateInstance(__uuidof(Connection)));  
      pConnection2->Provider = "Microsoft.Jet.OLEDB.4.0";  
  
      char *sConn = "c:\\Northwind.mdb";  
      pConnection2->Open(sConn, "admin", "", NULL);  
      // Display the provider  
      printf("Connection2 provider: %s \n\n",(LPCSTR)pConnection2->Provider);  
  
      // Requires SQL Server authentication  
      // Open a Connection using the Microsoft SQL Server provider.  
      TESTHR(pConnection3.CreateInstance(__uuidof(Connection)));  
      pConnection3->Provider = "sqloledb";  
      pConnection3->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", NULL);  
      // Display the provider.  
      printf("Connection3 provider: %s\n\n", (LPCSTR)pConnection3->Provider);  
   }  
  
   catch (_com_error &e) {  
      // Notify the user of errors if any.  
      PrintProviderError(pConnection1);  
      if (pConnection2)  
         PrintProviderError(pConnection2);  
  
      if (pConnection3)   
         PrintProviderError(pConnection3);  
  
      PrintComError(e);  
   }  
  
   if (pConnection1)  
      if (pConnection1->State == adStateOpen)  
         pConnection1->Close();  
  
   if (pConnection2)  
      if (pConnection2->State == adStateOpen)  
         pConnection2->Close();  
  
   if (pConnection3)  
      if (pConnection3->State == adStateOpen)  
         pConnection3->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("Error number: %x\t%s\n", pErr->Number, (LPCSTR) pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print COM errors.   
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>参照  
 [Connection オブジェクト (ADO)](./connection-object-ado.md)   
 [DefaultDatabase プロパティ](./defaultdatabase-property.md)   
 [Provider プロパティ (ADO)](./provider-property-ado.md)