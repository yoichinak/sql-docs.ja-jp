---
description: MaxRecords プロパティの例 (VC++)
title: MaxRecords プロパティの例 (VC + +) |Microsoft Docs
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
- MaxRecords property [ADO], VC++ example
ms.assetid: af6b399b-e546-4de5-9cd1-5a6e0ec7ddc7
author: rothja
ms.author: jroth
ms.openlocfilehash: 612ec3cd9e2fbdfba40fd554d52558c8c14baba6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990613"
---
# <a name="maxrecords-property-example-vc"></a>MaxRecords プロパティの例 (VC++)
この例では、 [MaxRecords](./maxrecords-property-ado.md)プロパティを使用して、***タイトル***テーブルに最も高価な10個のタイトルを含む[レコードセット](./recordset-object-ado.md)を開きます。  
  
## <a name="example"></a>例  
  
```  
// MaxRecords_Property_Example.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF","EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// This class extracts titles and type from the titles table  
class CTitleRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CTitleRs)  
  
      // Column title is the 1st field in the Recordset  
      ADO_VARIABLE_LENGTH_ENTRY2(1, adVarChar,m_szau_Title,  
      sizeof(m_szau_Title), lau_TitleStatus, FALSE)  
  
      // Column price is the 2nd field in the Recordset  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adDouble, m_szau_Price,  
      sizeof(m_szau_Price), lau_PriceStatus, FALSE)  
  
   END_ADO_BINDING()  
  
public:  
   CHAR m_szau_Title[81];  
   ULONG lau_TitleStatus;  
   DOUBLE m_szau_Price;  
   ULONG lau_PriceStatus;  
};  
  
// Function Declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void MaxRecordsX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   MaxRecordsX();  
   ::CoUninitialize();  
}  
  
void  MaxRecordsX() {  
   // Define ADO ObjectPointers.  Initialize Pointers on define  
   // These are in the ADODB :: namespace  
   _RecordsetPtr pRstTemp = NULL;  
  
   // Define Other Variables  
   IADORecordBinding *picRs = NULL;   // Interface Pointer Declared    
   CTitleRs titlers;   // C++ Class Object  
  
   try {  
      // Assign Connection String to Variable  
      _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
      // Open Recordset containing the 10 most expensive titles in the Titles table.  
      TESTHR(pRstTemp.CreateInstance(__uuidof(Recordset)));  
  
      pRstTemp->MaxRecords = 10;  
  
      pRstTemp->Open("SELECT title,price FROM Titles ORDER BY Price DESC",  
         strCnn, adOpenForwardOnly, adLockReadOnly, adCmdText);  
  
      // Open IADORecordBinding interface pointer for binding Recordset to a class  
      TESTHR(pRstTemp->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ class here  
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Display the contents of the Recordset  
      printf("Top Ten Titles by Price:\n\n");  
  
      while ( !(pRstTemp->EndOfFile) ) {  
         printf("%s ---  %6.2lf\n", titlers.lau_TitleStatus == adFldOK ?   
            titlers.m_szau_Title : "<NULL>", titlers.lau_PriceStatus == adFldOK ?   
            titlers.m_szau_Price : 0.00);  
         pRstTemp->MoveNext();  
      }  
   }  
   catch(_com_error &e) {  
      // Display errors, if any.  Pass connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstTemp->GetActiveConnection();  
  
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
  
   // Clean up objects before exit. Release the IADORecordset Interface here     
   if (picRs)  
      picRs->Release();  
  
   if (pRstTemp)  
      if (pRstTemp->State == adStateOpen)  
         pRstTemp->Close();  
};  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object  
   // pErr is a record object in the Connection's Error collection  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count)>0 ) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount-1  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error Number :%x \t %s", pErr->Number, pErr->Description);  
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
  
 **価格別の上位10件のタイトル:**  
**しかし、ユーザーにとってわかりやすいでしょうか。---22.95**  
**コンピューター Phobic と Phobic 以外のユーザー: 動作のバリエーション---21.59**  
**タマネギ、Leeks、ニンニク: 地中海---20.95 の料理シークレット**  
**シリコンバレー---20.00 のシークレット**  
**忙しい役員のデータベースガイド---19.99**  
**コンピューター---19.99 についての説明**  
**シリコンバレー Gastronomic は---19.99 を扱います**  
**データの長時間分割: 4 つのケーススタディ---19.99**  
**すし、だれでも---14.99**  
**Buckingham Palace Kitchens---11.95 の50年**   
## <a name="see-also"></a>参照  
 [MaxRecords プロパティ (ADO)](./maxrecords-property-ado.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)