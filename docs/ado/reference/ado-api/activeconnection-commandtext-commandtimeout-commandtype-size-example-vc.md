---
description: ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VC + +)
title: ストアドプロシージャのプロパティの例 (VC + +) |Microsoft Docs
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
- CommandTimeout property [ADO], VC++ example
- CommandText property [ADO], VC++ example
- CommandType property [ADO], VC++ example
- Direction property [ADO], VC++ example
- ActiveConnection property [ADO], VC++ example
ms.assetid: 0d9917c4-9ef0-4d7a-b4ce-4f1fa6ce1817
author: rothja
ms.author: jroth
ms.openlocfilehash: 608d6258f0f8b458e346c4e56166439dd7ba934e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977043"
---
# <a name="activeconnection-commandtext-commandtimeout-commandtype-size-and-direction-properties-example-vc"></a>ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VC + +)
この例では、 [ActiveConnection](./activeconnection-property-ado.md)、 [CommandText](./commandtext-property-ado.md)、 [CommandTimeout](./commandtimeout-property-ado.md)、 [CommandType](./commandtype-property-ado.md)、 [Size](./size-property-ado-parameter.md)、および [Direction](./direction-property.md) プロパティを使用してストアドプロシージャを実行します。  
  
## <a name="example"></a>例  
  
```  
// BeginActiveConnectionCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#define TESTHR(x) if FAILED(x) _com_issue_error(x)  
  
#include <stdio.h>  
#include <ole2.h>  
#include "conio.h"  
#include "icrsint.h"  
  
// class extracts  fname,lastname  
class CEmployeeRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CEmployeeRs)  
  
   // Column au_id is the 1st field in the recordset     
   ADO_VARIABLE_LENGTH_ENTRY2(1, adVarChar, m_szau_id, sizeof(m_szau_id),   
                              lau_idStatus, TRUE)  
  
   ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_szau_lname, sizeof(m_szau_lname),   
                              lau_lnameStatus, TRUE)  
  
   ADO_VARIABLE_LENGTH_ENTRY2(3, adVarChar, m_szau_fname, sizeof(m_szau_fname),   
                              lau_fnameStatus, TRUE)  
  
   END_ADO_BINDING()  
  
public:  
   CHAR m_szau_id[20];  
   ULONG lau_idStatus;  
   CHAR m_szau_fname[40];  
   ULONG lau_fnameStatus;  
   CHAR m_szau_lname[40];  
   ULONG lau_lnameStatus;  
};  
  
// Function declaration  
void ActiveConnectionX();  
void PrintProviderError(_ConnectionPtr pConnection);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   ActiveConnectionX();  
   ::CoUninitialize();  
}  
  
void ActiveConnectionX() {  
   HRESULT hr = S_OK;    
  
   // Define ADO object pointers, initialize pointers on define. These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   _CommandPtr pCmdByRoyalty = NULL;  
   _RecordsetPtr pRstByRoyalty = NULL;  
   _RecordsetPtr pRstAuthors = NULL;  
   _ParameterPtr pPrmByRoyalty = NULL;  
  
   // Define Other variables  
   IADORecordBinding *picRs = NULL;   // Interface Pointer declared.(VC++ Extensions)  TCS(SPA)  
   CEmployeeRs emprs;   // C++ class object  TCS(SPA)  
   _bstr_t strAuthorId;  
   int intRoyalty;  
   VARIANT vtroyal;  
  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Define a command object for a stored procedure.   
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      hr = pConnection->Open(strCnn, "", "", adConnectUnspecified);  
  
      TESTHR(pCmdByRoyalty.CreateInstance(__uuidof(Command)));  
  
      pCmdByRoyalty->ActiveConnection = pConnection;  
      pCmdByRoyalty->CommandText = "byRoyalty";  
      pCmdByRoyalty->CommandType = adCmdStoredProc;  
      pCmdByRoyalty->CommandTimeout = 15;  
  
      // Define stored procedure's input parameter.   
      printf("Enter Royalty :  ");  
      scanf_s("%d",&intRoyalty);  
  
      // Assign Integer value   
      vtroyal.vt = VT_I2;  
      vtroyal.iVal = intRoyalty;  
  
      TESTHR(pPrmByRoyalty.CreateInstance(__uuidof(Parameter)));  
      pPrmByRoyalty->Type = adInteger;  
      pPrmByRoyalty->Size = 3;  
      pPrmByRoyalty->Direction = adParamInput;  
      pPrmByRoyalty->Value = vtroyal;  
      pCmdByRoyalty->Parameters->Append(pPrmByRoyalty);  
  
      // Create a recordset by executing a command.  
      pRstByRoyalty = pCmdByRoyalty->Execute(NULL,NULL,adCmdStoredProc);   
  
      // Open the authors table to get author names for display.   
      TESTHR(pRstAuthors.CreateInstance(__uuidof(Recordset)));  
      hr = pRstAuthors->Open("authors", strCnn, adOpenForwardOnly, adLockReadOnly, adCmdTable);  
  
      // Open an IADORecordBinding interface pointer which we'll use for Binding Recordset to a class  
      TESTHR(pRstAuthors->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ Class here  
      TESTHR(picRs->BindToRecordset(&emprs));  
  
      // Print current data in the recordset ,adding author names from author table.   
      printf("Authors With  %d  Percent Royalty", intRoyalty);  
  
      while (!(pRstByRoyalty->EndOfFile)) {  
         strAuthorId = pRstByRoyalty->Fields->Item["au_id"]->Value;  
         pRstAuthors->Filter = "au_id = '" + strAuthorId + "'";  
  
         printf("\n\t%s, %s %s",emprs.lau_idStatus == adFldOK ? emprs.m_szau_id : "<NULL>",\  
            emprs.lau_fnameStatus == adFldOK ? emprs.m_szau_fname : "<NULL>",\  
            emprs.lau_lnameStatus == adFldOK ? emprs.m_szau_lname : "<NULL>");  
  
         pRstByRoyalty->MoveNext();   
      }  
  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      PrintProviderError(pConnection);  
      printf("Source : %s \n Description : %s \n", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
  
   // Clean up objects before exit. Release the IADORecordset Interface here  
   if (picRs)   
      picRs->Release();  
  
   if (pRstByRoyalty)  
      if (pRstByRoyalty->State == adStateOpen)  
         pRstByRoyalty->Close();  
   if (pRstAuthors)  
      if (pRstAuthors->State == adStateOpen)  
         pRstAuthors->Close();  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
   long nCount = 0;  
   long i = 0;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for (i = 0 ; i < nCount ; i++) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("Error number: %x\t%s", pErr->Number, (LPCSTR)pErr->Description);  
      }  
   }  
}  
```  
  
 入力  
  
```  
25  
```  
  
## <a name="sample-output"></a>サンプル出力  
  
```  
Authors With  25  Percent Royalty  
        724-80-9391, Stearns MacFeather  
        899-46-2035, Anne Ringer  
```  
  
## <a name="see-also"></a>参照  
 [ActiveConnection プロパティ (ADO)](./activeconnection-property-ado.md)   
 [CommandText プロパティ (ADO)](./commandtext-property-ado.md)   
 [CommandTimeout プロパティ (ADO)](./commandtimeout-property-ado.md)   
 [CommandType プロパティ (ADO)](./commandtype-property-ado.md)   
 [Direction プロパティ](./direction-property.md)   
 [Size プロパティ (ADO Parameter)](./size-property-ado-parameter.md)