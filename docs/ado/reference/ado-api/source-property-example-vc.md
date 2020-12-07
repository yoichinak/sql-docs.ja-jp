---
description: Source プロパティの例 (VC++)
title: Source プロパティの例 (VC + +) |Microsoft Docs
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
- Source property [ADO], VC++ example
ms.assetid: e10d33da-ea30-4138-ae40-e9f6aa9d17d9
author: rothja
ms.author: jroth
ms.openlocfilehash: 7b582582fa3acc91921aeee41a465915979a6c7d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988893"
---
# <a name="source-property-example-vc"></a>Source プロパティの例 (VC++)
この例では、さまざまなデータソースに基づいて3つの[レコードセット](./recordset-object-ado.md)オブジェクトを開くことによって、 [Source](./source-property-ado-recordset.md)プロパティを示します。  
  
```  
// Source_Property_Sample.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void SourceX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   SourceX();  
   ::CoUninitialize();  
}  
  
void SourceX() {  
   // Define string variables.  
   _bstr_t strCmdSQL("Select title ,type, pubdate FROM titles ORDER BY title");    
   _bstr_t strSQL("SELECT title_ID AS TitleID, title AS Title, "   
      "publishers.pub_id AS PubID, pub_name AS PubName "  
      "FROM publishers INNER JOIN titles "   
      "ON publishers.pub_id = titles.pub_id "   
      "ORDER BY Title");  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB:: namespace.  
   _ConnectionPtr pConnection = NULL;  
   _RecordsetPtr pRstTitles = NULL;  
   _RecordsetPtr pRstPublishers = NULL;  
   _RecordsetPtr pRstPublishersDirect = NULL;  
   _RecordsetPtr pRstTitlesPublishers = NULL;  
   _CommandPtr pCmdSQL = NULL;  
  
   try {  
      // Open a connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
      // Open a recordset based on a command object.  
      TESTHR(pCmdSQL.CreateInstance(__uuidof(Command)));  
      pCmdSQL->ActiveConnection = pConnection;  
      pCmdSQL->CommandText = strCmdSQL;  
      pRstTitles = pCmdSQL->Execute(NULL, NULL, adCmdText);  
  
      // Open a recordset based on a table  
      TESTHR(pRstPublishers.CreateInstance(__uuidof(Recordset)));  
      pRstPublishers->Open ("publishers", _variant_t((IDispatch *) pConnection, true),  
         adOpenForwardOnly, adLockReadOnly, adCmdTable);  
  
      // Open a recordset based on a table  
      TESTHR(pRstPublishersDirect.CreateInstance(__uuidof(Recordset)));  
      pRstPublishersDirect->Open ("publishers", _variant_t((IDispatch *) pConnection, true),  
         adOpenForwardOnly, adLockReadOnly, adCmdTableDirect);  
  
      // Open a recordset based on a SQL string.  
      TESTHR(pRstTitlesPublishers.CreateInstance(__uuidof(Recordset)));  
      pRstTitlesPublishers->Open(strSQL, _variant_t((IDispatch *) pConnection, true),  
         adOpenForwardOnly, adLockReadOnly, adCmdText);  
  
      // Use the Source property to display the source of each recordset.  
      printf("rstTitles source: \n%s\n\n",  
         (LPCSTR)(_bstr_t) pRstTitles->GetSource().bstrVal);  
  
      printf("rstPublishers source: \n%s\n\n",  
         (LPCSTR)(_bstr_t) pRstPublishers->GetSource().bstrVal);  
  
      printf("rstPublishersDirect source: \n%s\n\n",  
         (LPCSTR)(_bstr_t) pRstPublishersDirect->GetSource().bstrVal);  
  
      printf("rstTitlesPublishers source: \n%s\n\n",  
         (LPCSTR)(_bstr_t) pRstTitlesPublishers->GetSource().bstrVal);  
   }  
   catch (_com_error &e) {  
      // Notify the user of errors if any.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen)  
         pRstTitles->Close();  
   if (pRstPublishers)  
      if (pRstPublishers->State == adStateOpen)  
         pRstPublishers->Close();  
   if (pRstPublishersDirect)  
      if (pRstPublishersDirect->State == adStateOpen)  
         pRstPublishersDirect->Close();  
   if (pRstTitlesPublishers)  
      if (pRstTitlesPublishers->State == adStateOpen)  
         pRstTitlesPublishers->Close();  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
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
  
   // Print Com errors.    
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>参照  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)   
 [Source プロパティ (ADO Recordset)](./source-property-ado-recordset.md)