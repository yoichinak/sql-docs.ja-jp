---
title: IRowsetFastLoad::Commit (OLE DB ドライバー) | Microsoft Docs
description: OLE DB Driver for SQL Server で、挿入された行のバッチの終わりを IRowsetFastLoad::Commit メソッドでマークし、SQL Server テーブルに書き込む方法について説明します。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e0248c160b80203a09f4712d697d1896732033e
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860693"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  挿入される行のバッチの終わりをマークし、挿入された行を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のテーブルに書き込みます。 サンプルについては、「[IRowsetFastLoad を使用したデータの一括コピー (OLE DB)](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)」と「[IROWSETFASTLOAD と ISEQUENTIALSTREAM を使用した SQL SERVER への BLOB データの送信 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>引数  
 *fDone*[in]  
 FALSE の場合、行セットは有効なまま保持され、コンシューマーはこの行セットを使用してさらに行を挿入できます。 TRUE の場合、行セットは無効になり、コンシューマーはこれ以上行を挿入できません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功し、挿入されたすべてのデータが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブルに書き込まれました。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。 特定のエラー テキストのエラー情報をプロバイダーから取得してください。  
  
 E_UNEXPECTED  
 既に **IRowsetFastLoad::Commit** メソッドによって無効になっている一括コピー行セットに対して呼び出されました。  
  
## <a name="remarks"></a>解説  
 OLE DB Driver for SQL Server の一括コピー行セットは、遅延更新モードの行セットとして動作します。 ユーザーが行セットを使用して行データを挿入すると、挿入された行は、**IRowsetUpdate** をサポートする行セットでの保留中の挿入と同様の形式で扱われます。  
  
 コンシューマーは、**IRowsetUpdate::Update** メソッドを使用して保留中の行を SQL Server のインスタンスに送信するのと同様に、一括コピー行セットに対して **Commit** メソッドを呼び出して、挿入された行を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブルに書き込む必要があります。  
  
 コンシューマーが **Commit** メソッドを呼び出さないで一括コピー行セットの参照を解放すると、挿入されてもそれ以前に書き込まれていない行はすべて失われます。  
  
 コンシューマーは、*fDone* 引数を FALSE に設定して **Commit** メソッドを呼び出すことにより、挿入される行をバッチ処理できます。 *fDone* を TRUE に設定すると、その行セットは無効になります。 無効な一括コピー行セットでは、**ISupportErrorInfo** インターフェイスと **IRowsetFastLoad::Release** メソッドのみがサポートされます。  
  
## <a name="see-also"></a>参照  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
