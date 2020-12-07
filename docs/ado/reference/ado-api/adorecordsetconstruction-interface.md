---
description: ADORecordsetConstruction インターフェイス
title: ADORecordsetConstruction Interface |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
author: rothja
ms.author: jroth
ms.openlocfilehash: ecf8f8e12f8d12a3382e7b67b13e8bb12fb69ac9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976223"
---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction インターフェイス
**ADORecordsetConstruction**インターフェイスは、C/c + + アプリケーションの OLE DB**行**セットオブジェクトから ADO**レコードセット**オブジェクトを構築するために使用されます。  
  
 このインターフェイスは、次のプロパティをサポートしています。  
  
## <a name="properties"></a>プロパティ  
  
|プロパティ|説明|  
|-|-|  
|[章](./chapter-property-ado.md)|読み取り/書き込み。<br />この ADO**レコードセット**オブジェクトから OLE DB**チャプター**オブジェクトを取得/設定します。|  
|[RowPosition](./rowposition-property-ado.md)|読み取り/書き込み。<br />この ADO**レコードセット**オブジェクトの/から OLE DB **rowposition**オブジェクトを取得/設定します。|  
|[[行セット]](./rowset-property-ado.md)|読み取り/書き込み。<br />この ADO**レコードセット**オブジェクトの/から OLE DB**行**セットオブジェクトを取得/設定します。|  
  
## <a name="methods"></a>メソッド  
 なし。  
  
## <a name="events"></a>イベント  
 [なし] :  
  
## <a name="remarks"></a>解説  
 OLE DB の **行** セットオブジェクト ( `pRowset` ) がある場合、ADO **レコードセット** オブジェクト () の構造は、 `adoRs` 次の3つの基本的な操作になります。  
  
1.  ADO **レコードセット** オブジェクトを作成します。  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  **レコードセット**オブジェクトの**IADORecordsetConstruction**インターフェイスに対してクエリを実行します。  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  `IADORecordsetConstruction::put_Rowset`プロパティメソッドを呼び出して、ADO オブジェクトの OLE DB オブジェクトを設定し `Rowset` `Recordset` ます。  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 結果の `adoRs` オブジェクトは、OLE DB**行**セットオブジェクトから構築された ADO**レコードセット**オブジェクトを表します。  
  
 また、OLE DB**チャプター**または**ROWPOSITION**オブジェクトから ADO**レコードセット**オブジェクトを構築することもできます。  
  
## <a name="requirements"></a>必要条件  
 **バージョン:** ADO 2.0 以降  
  
 **ライブラリ:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>参照  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)   
 [Rowset プロパティ (ADO)](./rowset-property-ado.md)