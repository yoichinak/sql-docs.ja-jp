---
description: Parameters コレクションおよび Command プロパティの例 (VC++)
title: Parameters Collection、Command プロパティの例 (VC + +) |Microsoft Docs
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
- Parameters collection [ADOX], VC++ example
- Command property [ADOX], VC++ example
ms.assetid: 8636fa08-b3db-4e9a-a918-585e76dd59c8
author: rothja
ms.author: jroth
ms.openlocfilehash: 015179970822398d1c3a08735ff9d68af138b7fa
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983793"
---
# <a name="parameters-collection-command-property-example-vc"></a>Parameters コレクションおよび Command プロパティの例 (VC++)
次のコード [は、command プロパティを](./command-property-adox.md) [command](../ado-api/command-object-ado.md) オブジェクトと共に使用して、プロシージャのパラメーター情報を取得する方法を示しています。  
  
```  
// BeginProcedureParametersCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ProcedureParametersX(void);  
  
int main() {  
    if ( FAILED(::CoInitialize(NULL)) )  
        return -1;  
  
    ProcedureParametersX();  
  
    ::CoUninitialize();  
}  
  
void ProcedureParametersX() {  
    HRESULT hr = S_OK;  
  
    // Define and initialize ADOX object pointers. These are in ADODB namespace.  
    _CatalogPtr m_pCatalog = NULL;  
  
    //Define ADODB object pointers.  
    ADODB::_ConnectionPtr m_pCnn = NULL;  
    ADODB::_CommandPtr m_pCommand = NULL;  
    ADODB::_ParameterPtr m_pParameter = NULL;  
  
    try {  
        TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
  
        // Open the Connection  
        m_pCnn->Open("Provider='Microsoft.JET.OLEDB.4.0';Data Source='c:\\Northwind.mdb';", "", "", NULL);  
  
        TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
  
        // Open the catalog  
        m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
  
        // Get the command object  
        m_pCommand = m_pCatalog->Procedures->GetItem("CustomerById")->GetCommand();  
  
        _variant_t vIndex;  
  
        // Retrieve Parameter information  
        m_pCommand->Parameters->Refresh();  
        for ( long lIndex = 0 ; lIndex < m_pCommand->Parameters->Count ; lIndex ++ ) {  
            vIndex = lIndex;  
            m_pParameter = m_pCommand->Parameters->GetItem(vIndex);  
            cout << m_pParameter->Name << ":" << m_pParameter->Type << "\n" << endl;  
        }  
    }  
    catch(_com_error &e) {  
        // Notify the user of errors if any.  
        _bstr_t bstrSource(e.Source());  
        _bstr_t bstrDescription(e.Description());  
  
        printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
    }  
    catch(...) {  
        cout << "Error occurred in ProcedureParametersX...." << endl;  
    }  
}  
```