---
description: Optimize プロパティの例 (VC++)
title: Optimize プロパティの例 (VC + +) |Microsoft Docs
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
- Optimize property [ADO], VC++ example
ms.assetid: cb335455-b027-4f66-868d-d0d8b2175de1
author: rothja
ms.author: jroth
ms.openlocfilehash: 85cfa464710579db5872155a0e27bcc57ccdda94
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990253"
---
# <a name="optimize-property-example-vc"></a>Optimize プロパティの例 (VC++)
この例では、 [Field](./field-object.md) オブジェクトの dynamic **Optimize** プロパティを示します。 **Pubs**データベースの Authors テーブルの**zip**フィールドにはインデックスが**作成**されません。 **Zip**フィールドの[Optimize](./optimize-property-dynamic-ado.md)プロパティを**True**に設定すると、ADO によって、 [Find](./find-method-ado.md)メソッドのパフォーマンスを向上させるインデックスが作成されます。  
  
## <a name="example"></a>例  
  
```  
// Optimize_Property_Sample.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void OptimizeX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   OptimizeX();  
   ::CoUninitialize();  
}  
  
void OptimizeX() {  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB:: namespace.  
   _RecordsetPtr pRst = NULL;  
  
   try {  
      TESTHR(pRst.CreateInstance(__uuidof(Recordset)));  
  
      // Enable Index creation.  
      pRst->CursorLocation = adUseClient;  
      pRst->Open ("SELECT * FROM authors", strCnn, adOpenStatic, adLockReadOnly, adCmdText);  
  
      // Create the index  
      pRst->Fields->GetItem("zip")->Properties->GetItem("Optimize")->PutValue("True");  
  
      // Find Akiko Yokomoto  
      pRst->Find("zip = '94595'", 1, adSearchForward);  
      printf("%s %s    %s %s %s",  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("au_fname")->Value,  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("au_lname")->Value,  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("address")->Value,  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("city")->Value,  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("state")->Value);  
  
      // Delete the index  
      pRst->Fields->GetItem("zip")->Properties->GetItem("Optimize")->PutValue("False");  
   }  
   catch (_com_error &e) {  
      // Display errors, if any.  Pass connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRst->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
      case VT_BSTR:  
         PrintComError(e);  
         break;  
      case VT_DISPATCH:  
         PrintProviderError(vtConnect);  
         break;  
      default:  
         printf("Errors occured.");  
         break;  
      }  
   }  
  
   // Clean up objects before exit.  
   if (pRst)  
      if (pRst->State == adStateOpen)  
         pRst->Close();  
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
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
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
  
 **Akiko Yokomoto 3 シルバー Ct Walnut ドーソンクリーク CA**   
## <a name="see-also"></a>参照  
 [Field オブジェクト](./field-object.md)   
 [Optimize プロパティ - 動的 (ADO)](./optimize-property-dynamic-ado.md)