---
description: Attributes と Name プロパティの例 (VC + +)
title: Attributes と Name プロパティの例 (VC + +) |Microsoft Docs
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
- Attributes property [ADO], VC++ example
- Name property [ADO], VC++ example
ms.assetid: 2db7c9ca-d7d0-4c8e-840b-b27d7933ec40
author: rothja
ms.author: jroth
ms.openlocfilehash: c4eb8b682e7e539c1c0af784eb70016fa1bb25c1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975963"
---
# <a name="attributes-and-name-properties-example-vc"></a>Attributes と Name プロパティの例 (VC + +)
この例では、[接続](./connection-object-ado.md)、[フィールド](./field-object.md)、および[プロパティ](./property-object-ado.md)オブジェクトの[Attributes](./attributes-property-ado.md)プロパティの値を表示します。 [Name](./name-property-ado.md)プロパティを使用して、各**フィールド**と**プロパティ**オブジェクトの名前を表示します。  
  
```  
// BeginAttributesCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// This class extracts LastName, FirstName, FaxPhone from Employees table  
  
class CEmployeeRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CEmployeeRs)  
  
      // Column LastName is the 2nd field in the table  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_szemp_LastName, sizeof(m_szemp_LastName), lemp_LastNameStatus, TRUE)  
  
      // Column FirstName is the 17th field in the table  
      ADO_VARIABLE_LENGTH_ENTRY2(17, adVarChar, m_szemp_FirstName, sizeof(m_szemp_FirstName), lemp_FirstNameStatus, TRUE)  
  
      // Column FaxPhone is the 18th field in the table  
      ADO_VARIABLE_LENGTH_ENTRY2(18, adVarChar, m_szemp_Faxphone, sizeof(m_szemp_Faxphone), lemp_FaxphoneStatus, TRUE)  
  
      END_ADO_BINDING()  
  
public:  
   CHAR  m_szemp_LastName[21];  
   ULONG lemp_LastNameStatus;  
   CHAR  m_szemp_FirstName[11];  
   ULONG lemp_FirstNameStatus;  
   CHAR  m_szemp_Faxphone[25];  
   ULONG lemp_FaxphoneStatus;  
};  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void AttributesX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
   AttributesX();  
   ::CoUninitialize();  
}  
  
void AttributesX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace  
   _RecordsetPtr pRstEmployee  = NULL;  
   _ConnectionPtr pConnection = NULL;  
   FieldsPtr fldLoop = NULL;      
   PropertiesPtr proLoop = NULL;  
  
   // Define Other Variables  
   HRESULT hr = S_OK;  
   _variant_t Index;  
   Index.vt = VT_I2;  
   int j = 0;        
   // Open a recordset using a Client Cursor for the Employee Table  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='(local)'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // open connection and record set  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open(strCnn, "", "", adConnectUnspecified);  
  
      TESTHR(pRstEmployee.CreateInstance(__uuidof(Recordset)));  
      pRstEmployee->Open("Employee", _variant_t((IDispatch *)pConnection,true), adOpenForwardOnly,  
         adLockReadOnly, adCmdTable);  
  
      // Display the attributes of Connection.  
      printf("Connection attributes: %d \n", pConnection->Attributes);  
  
      // Display the attribute of the employee table's fields  
      printf("\nFields attributes:\n");  
      fldLoop = pRstEmployee->GetFields();  
  
      for (int i = 0 ; i < (int)fldLoop->GetCount() ; i++) {  
         Index.iVal = i;  
         printf ("   %s = %d \n", (LPSTR)fldLoop->GetItem(Index)->GetName(),  
            (int)fldLoop->GetItem(Index)->GetAttributes());  
      }  
  
      // Display Fields of the Employee table which are NULLBALE  
      printf("\nNULLABLE Fields :");  
  
      for (int i1 = 0 ; i1 < (int)fldLoop->GetCount() ; i1++) {  
         Index.iVal = i1;  
  
         if (fldLoop->GetItem(Index)->GetAttributes()  & adFldIsNullable)  
            printf ("%s  \n", (LPSTR)fldLoop->GetItem(Index)->GetName());      
      }  
  
      // Display the attributes of the Employee tables's  properties  
      printf("\nProperty attributes:\n");  
      proLoop = pRstEmployee->GetProperties();  
  
      for (int i2 = 0 ; i2 < (int)proLoop->GetCount() ; i2++) {  
         j = j + 1;  
         Index.iVal = i2;  
         printf (" %s = %d \n", (LPSTR)(_bstr_t)proLoop->GetItem(Index)->GetName(),  
            (int)proLoop->GetItem(Index)->GetAttributes());   
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   // Clean up objects before exit.  
   if (pRstEmployee)  
      if (pRstEmployee->State == adStateOpen)  
         pRstEmployee->Close();  
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
         printf("\t Error number: %x\t%s", (LPCSTR) pErr->Number, (LPCSTR) pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print Com errors.    
   printf("\nError\n");  
   printf("Code = %08lx\n", e.Error());  
   printf("Code meaning = %s\n", e.ErrorMessage());  
   printf("Source = %s\n", (LPCSTR) bstrSource);  
   printf("Description = %s\n", (LPCSTR) bstrDescription);    
}  
```  
  
## <a name="see-also"></a>参照  
 [Attributes プロパティ (ADO)](./attributes-property-ado.md)   
 [Connection オブジェクト (ADO)](./connection-object-ado.md)   
 [Field オブジェクト](./field-object.md)   
 [Name プロパティ (ADO)](./name-property-ado.md)   
 [Property オブジェクト (ADO)](./property-object-ado.md)