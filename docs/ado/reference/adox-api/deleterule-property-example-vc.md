---
description: DeleteRule プロパティの例 (VC++)
title: DeleteRule プロパティの例 (VC + +) |Microsoft Docs
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
- DeleteRule property [ADOX], VC++ example
ms.assetid: 7a1def31-2b6f-4542-aac3-ec35b54c89ef
author: rothja
ms.author: jroth
ms.openlocfilehash: 581acace73f7186b724f78f79e768310d44c3379
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984583"
---
# <a name="deleterule-property-example-vc"></a>DeleteRule プロパティの例 (VC++)
この例では、[キー](./key-object-adox.md)オブジェクトの[DeleteRule](./deleterule-property-adox.md)プロパティを示します。 コードによって新しい [テーブル](./table-object-adox.md) が追加され、新しい主キーが定義され、 **DeleteRule** が **adRICascade**に設定されます。  
  
```  
// BeginDeleteRuleCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _KeyPtr m_pKeyPrimary = NULL;  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTblNew = NULL;  
  
   // Define string variables.  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = 'c:\\Northwind.mdb';");  
   try {  
      TESTHR(hr = m_pKeyPrimary.CreateInstance(__uuidof(Key)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      TESTHR(hr = m_pTblNew.CreateInstance(__uuidof(Table)));  
  
      // Connect the catalog.  
      m_pCatalog->PutActiveConnection(strcnn);  
  
      // Name new table.  
      m_pTblNew->Name = "NewTable";  
  
      // Append a numeric and a text field to new table.  
      m_pTblNew->Columns->Append("NumField", adInteger, 20);  
      m_pTblNew->Columns->Append("TextField", adVarWChar, 20);  
  
      // Append the new table.  
      m_pCatalog->Tables->Append(_variant_t((IDispatch*)m_pTblNew));  
      printf("Table 'NewTable' is added.\n");  
  
      // Define the Primary key.  
      m_pKeyPrimary->Name = "NumField";  
      m_pKeyPrimary->Type = adKeyPrimary;  
      m_pKeyPrimary->RelatedTable = "Customers";  
      m_pKeyPrimary->Columns->Append("NumField", adInteger,20);  
      m_pKeyPrimary->Columns->GetItem("NumField")->RelatedColumn = "CustomerId";  
      m_pKeyPrimary->DeleteRule = adRICascade;  
  
      // to pass an optional column parameter to Key's Apppend method  
      _variant_t vOptional;  
      vOptional.vt = VT_ERROR;  
      vOptional.scode = DISP_E_PARAMNOTFOUND;  
  
      // Append the primary key.  
      m_pCatalog->Tables->GetItem("NewTable")->Keys->Append( _variant_t((IDispatch*)m_pKeyPrimary),   
         adKeyPrimary,vOptional,   
         L"",   
         L"");  
  
      // Delete the table as this is a demonstration.  
      m_pCatalog->Tables->Delete(m_pTblNew->Name);  
      printf("Table 'NewTable' is deleted.\n");  
   }  
  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
  
   catch(...) {  
      cout << "Error occurred in include files...."<< endl;  
   }  
  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>参照  
 [DeleteRule プロパティ (ADOX)](./deleterule-property-adox.md)   
 [Key オブジェクト (ADOX)](./key-object-adox.md)