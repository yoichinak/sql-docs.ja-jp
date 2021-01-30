---
description: Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VC + +)
title: Error オブジェクトプロパティの例 (VC + +) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- Number property [ADO], VC++ example
- HelpContext property [ADO], VC++ example
- NativeError property [ADO], VC++ example
- SQLState property [ADO], VC++ example
- Source property [ADO], VC++ example
- HelpFile property [ADO], VC++ example
- Description property [ADO], VC++ example
ms.assetid: 5321fc0f-cd0c-4e2a-a5bc-0008fba86b59
author: rothja
ms.author: jroth
ms.openlocfilehash: 78bafcdac03072c82314b45f0744299d3ab6e300
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99171258"
---
# <a name="description-helpcontext-helpfile-nativeerror-number-source-and-sqlstate-properties-example-vc"></a>Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VC + +)
この例では、エラーをトリガーし、トラップして、結果として生成される[error](../../../ado/reference/ado-api/error-object.md)オブジェクトの[Description](../../../ado/reference/ado-api/description-property.md)、 [helpcontext](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)、 [HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)、の[エラー](../../../ado/reference/ado-api/nativeerror-property-ado.md)、 [Number](../../../ado/reference/ado-api/number-property-ado.md)、 [Source](../../../ado/reference/ado-api/source-property-ado-error.md)、および[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)の各プロパティを表示します。  
  
```  
// BeginDescriptionCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void DescriptionX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   DescriptionX();  
   ::CoUninitialize();  
}  
  
void DescriptionX() {  
   // Define ADO object pointers. Initialize pointers on define. These are in the ADODB::  namespace  
   _ConnectionPtr pConnection = NULL;  
   ErrorPtr errorLoop = NULL;  
  
   // Define Other Variables  
   HRESULT hr = S_OK;  
  
   try {  
      // Intentionally trigger an error.  open connection  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
  
      if (FAILED(hr = pConnection->Open("Nothing", "", "", adConnectUnspecified))) {  
         _com_issue_error(hr);  
         exit(1);  
      }  
  
      // Cleanup object before exit.  
      pConnection->Close();  
   }  
   catch(_com_error) {  
      // Pass a connection pointer.  
      PrintProviderError(pConnection);  
   }  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Define Other Variables  
   HRESULT hr = S_OK;  
   _bstr_t strError;  
   ErrorPtr pErr = NULL;  
  
   try {  
      // Enumerate Errors collection and display properties of each Error object.  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount - 1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("Error #%d\n", pErr->Number);  
         printf(" %s\n", (LPCSTR)pErr->Description);  
         printf(" (Source: %s)\n", (LPCSTR)pErr->Source);  
         printf(" (SQL State: %s)\n", (LPCSTR)pErr->SQLState);  
         printf(" (NativeError: %d)\n", (LPCSTR)pErr->NativeError);  
  
         if ((LPCSTR)pErr->GetHelpFile() == NULL)  
            printf("\tNo Help file available\n");  
         else {  
            printf("\t(HelpFile: %s\n)" ,pErr->HelpFile);  
            printf("\t(HelpContext: %s\n)" , pErr->HelpContext);  
         }  
      }  
   }  
  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      PrintComError(e);  
   }  
}  
  
void PrintComError(_com_error &e) {  
   // Notify the user of errors if any.  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print Com errors.  
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>参照  
 [Description プロパティ](../../../ado/reference/ado-api/description-property.md)   
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)   
 [HelpContext、HelpFile プロパティ](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [HelpContext、HelpFile プロパティ](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 ["メッセージのエラー" プロパティ (ADO)](../../../ado/reference/ado-api/nativeerror-property-ado.md)   
 [Number プロパティ (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source プロパティ (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [SQLState プロパティ](../../../ado/reference/ado-api/sqlstate-property.md)
