---
description: State プロパティの例 (VC++)
title: State プロパティの例 (VC + +) |Microsoft Docs
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
- State property [ADO], VC++ example
ms.assetid: 1c38cd3b-e4f5-4754-b115-ef5e46d24ab9
author: rothja
ms.author: jroth
ms.openlocfilehash: c1eeb97d29525a7aa3a48b0c123f60776fc5e223
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988793"
---
# <a name="state-property-example-vc"></a>State プロパティの例 (VC++)
この例では、非同期接続が開いており、非同期コマンドが実行中の場合に、 [State](./state-property-ado.md) プロパティを使用してメッセージを表示します。  
  
```  
// BeginStateCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void StateX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   StateX();  
   ::CoUninitialize();  
}  
  
void StateX() {  
   HRESULT  hr = S_OK;  
  
   // Define string variables.  
   _bstr_t strSQLChange("UPDATE Titles SET Type = 'self_help' WHERE Type = 'psychology'");  
   _bstr_t strSQLRestore("UPDATE Titles SET Type = 'psychology' WHERE Type = 'self_help'");  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   _ConnectionPtr pConnection2 = NULL;  
   _CommandPtr pCmdChange = NULL;  
   _CommandPtr pCmdRestore = NULL;  
  
   try {  
      // Open two asynchronous connections,displaying a message while connecting.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      TESTHR(pConnection2.CreateInstance(__uuidof(Connection)));  
  
      pConnection->Open (strCnn, "", "", adAsyncConnect);  
      while(pConnection->State == adStateConnecting)  
         printf("Opening first connection....\n\n");  
  
      pConnection2->Open (strCnn, "", "", adAsyncConnect);  
      while(pConnection2->State == adStateConnecting)  
         printf("Opening second connection....\n\n");  
  
      // Create two command objects.  
      TESTHR(pCmdChange.CreateInstance(__uuidof(Command)));  
      pCmdChange->ActiveConnection = pConnection;  
      pCmdChange->CommandText = strSQLChange;  
  
      TESTHR(pCmdRestore.CreateInstance(__uuidof(Command)));  
      pCmdRestore->ActiveConnection = pConnection2;  
      pCmdRestore->CommandText = strSQLRestore;  
  
      // Executing the commands,displaying a message while they are executing.  
      pCmdChange->Execute(NULL,NULL,adAsyncExecute);  
      while(pCmdChange->State == adStateExecuting)  
         printf("Change command executing...\n\n");  
  
      pCmdRestore->Execute(NULL,NULL,adAsyncExecute);  
      while(pCmdRestore->State == adStateExecuting)  
         printf("Restore command executing...\n\n");  
   }  
   catch (_com_error &e) {  
      // Notify the user of errors if any.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
   if (pConnection2)  
      if (pConnection2->State == adStateOpen)  
         pConnection2->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for (long i = 0 ; i < nCount ; i++) {  
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
 [State プロパティ (ADO)](./state-property-ado.md)