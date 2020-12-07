---
description: GetString メソッドの例 (VC++)
title: GetString メソッドの例 (VC + +) |Microsoft Docs
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
- GetString method [ADO], VC++ example
ms.assetid: 4daa93aa-9727-4d1c-886a-e9d22017a1ea
author: rothja
ms.author: jroth
ms.openlocfilehash: a17c15f7ab3ec1764c9902a87ea4e7229af1fa2b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990853"
---
# <a name="getstring-method-example-vc"></a>GetString メソッドの例 (VC++)
この例では、 [GetString](./getstring-method-ado.md) メソッドを示します。  
  
 データアクセスの問題をデバッグしているときに、小さな [レコードセット](./recordset-object-ado.md)の現在の内容をすばやく簡単に印刷できるようにすることを想定しています。  
  
## <a name="example"></a>例  
  
```  
// BeginGetString.cpp  
// compile with: /EHsc /c  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include <string.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void GetStringX(void);  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
inline char* mygets(char* strDest, int n) {     
   char strExBuff[10];  
   char* pstrRet = fgets(strDest, n, stdin);  
  
   if (pstrRet == NULL)  
      return NULL;  
  
   // Exhaust the input buffer.  
   if (!strrchr(strDest, '\n'))  
      do {  
         fgets(strExBuff, sizeof(strExBuff), stdin);  
      } while (!strrchr(strExBuff, '\n'));  
   else  
      // Replace '\n' with '\0'  
      strDest[strrchr(strDest, '\n') - strDest] = '\0';  
  
   return pstrRet;  
}  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
   GetStringX();  
   ::CoUninitialize();  
}  
  
void GetStringX() {  
   HRESULT  hr = S_OK;  
  char * token1;  
  
   // Define ADO object pointers.  
   // Initialize pointers on define.  
   // These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   _RecordsetPtr pRstAuthors = NULL;  
  
   // Define string variables.  
   _bstr_t strCnn("Provider='sqloledb'; Data Source=My_Data_Source; Initial Catalog='pubs'; Integrated Security='SSPI';");  
   _bstr_t varOutput;   
   char *strPrompt = "Enter a state (CA, IN, KS, MD, MI, OR, TN, UT): ";  
   char strState[3], *pState;  
  
   try {  
      // Open connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
  
      // Open a command object for a stored procedure,   
      // with one parameter.  
      TESTHR(pRstAuthors.CreateInstance(__uuidof(Recordset)));  
  
      printf("%s",strPrompt);  
      mygets(strState, 3);  
  
      pState = strtok_s(strState," \t", &token1);  
  
      char strQry[100];  
      _snprintf_s(strQry, _countof(strQry), sizeof(strQry)-1, "SELECT au_fname, au_lname, address, city "  
         "FROM authors WHERE state = '%s'", pState);  
      strQry[sizeof(strQry)-1] = '\0';  
  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
      pRstAuthors->Open(strQry, _variant_t((IDispatch*)pConnection, true),   
         adOpenStatic, adLockReadOnly, adCmdText);  
  
      if (pRstAuthors->RecordCount > 0)  {  
         // Use all defaults: get all rows, TAB column delimiter,   
         // CARRIAGE RETURN row delimiter, empty-string null delimiter  
         long lRecCount =  pRstAuthors->RecordCount;  
         _bstr_t varTab("\t");  
         _bstr_t varRet("\r");  
         _bstr_t varNull("");  
         varOutput = pRstAuthors->GetString(adClipString, lRecCount, varTab, varRet, varNull);  
         printf("State = '%s'\n", strState);  
         printf ("Name            Address            City\n");  
         printf ("%s\n", (LPCTSTR)varOutput);  
      }  
      else  
         printf("\nNo rows found for state = '%s'\n", pState);  
   }   
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      // Pass a connection pointer accessed from the Recordset.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   // Clean up objects before exit.  
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
  
   if( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for (long i = 0 ; i < nCount ; i++) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
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
  
## <a name="sample-input"></a>サンプル入力  
  
```  
MD  
```  
  
## <a name="sample-output"></a>サンプル出力  
  
```  
Enter a state (CA, IN, KS, MD, MI, OR, TN, UT): State = 'md'  
Name            Address            City  
Sylvia   Panteley   1956 Arlington Pl.   Rockville  
```  
  
## <a name="see-also"></a>参照  
 [GetString メソッド (ADO)](./getstring-method-ado.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)