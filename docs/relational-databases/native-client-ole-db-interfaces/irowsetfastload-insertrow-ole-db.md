---
description: 'IRowsetFastLoad:: InsertRow (Native Client OLE DB プロバイダー)'
title: 'IRowsetFastLoad:: InsertRow (Native Client OLE DB provider) |Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
ms.assetid: 594d3461-34d2-41e7-8ad4-bd2753601ab6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b465832e99c08cc8c4a17380fc894ecd3076a9c7
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866732"
---
# <a name="irowsetfastloadinsertrow-native-client-ole-db-provider"></a>IRowsetFastLoad:: InsertRow (Native Client OLE DB プロバイダー)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  一括コピー行セットに行を追加します。 サンプルについては、「[IRowsetFastLoad を使用したデータの一括コピー (OLE DB)](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)」と「[IROWSETFASTLOAD と ISEQUENTIALSTREAM を使用した SQL SERVER への BLOB データの送信 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT InsertRow(  
      HACCESSOR hAccessor,  
      void* pData);  
```  
  
## <a name="arguments"></a>引数  
 *hAccessor*[in]  
 一括コピーの行データを定義するアクセサーのハンドルを指定します。 参照されるアクセサーは行アクセサーで、データ値を保持するコンシューマー所有のメモリをバインドします。  
  
 *pData*[in]  
 データ値を保持するコンシューマー所有のメモリへのポインターを指定します。 詳細については、「[DBBINDING 構造体](/previous-versions/windows/desktop/ms716845(v=vs.85))」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。 すべての列のバインド状態値は、DBSTATUS_S_OK または DBSTATUS_S_NULL です。  
  
 E_FAIL  
 エラーが発生しました。 エラー情報は、行セットのエラー インターフェイスから参照できます。  
  
 E_INVALIDARG  
 *pData* 引数に NULL ポインターが設定されました。  
  
 E_OUTOFMEMORY  
 SQLNCLI11 では、要求を完了するのに必要なメモリを割り当てることができませんでした。  
  
 E_UNEXPECTED  
 既に [IRowsetFastLoad::Commit](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md) メソッドによって無効になっている一括コピー行セットに対して呼び出されました。  
  
 DB_E_BADACCESSORHANDLE  
 コンシューマーが指定した *hAccessor* 引数が無効でした。  
  
 DB_E_BADACCESSORTYPE  
 指定されたアクセサーが行アクセサーではなかったか、コンシューマー所有のメモリが指定されませんでした。  
  
## <a name="remarks"></a>解説  
 コンシューマーデータを列のデータ型に変換するときにエラーが発生する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーから E_FAIL が返されます。 **InsertRow** メソッドを使用するか、**Commit** メソッドのみを使用して、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に転送できます。 **InsertRow** メソッドを使用する場合、コンシューマー アプリケーションは、データ型変換エラーの通知を受け取るまで、誤ったデータを使用してこのメソッドを何回も呼び出す可能性があります。 **Commit** メソッドでは、すべてのデータがコンシューマーにより正しく指定されたことが保証されるので、コンシューマーは適切に **Commit** を使用することで、必要に応じてデータを検証できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーの一括コピー行セットは書き込み専用です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーは、行セットのコンシューマークエリを許可するメソッドを公開しません。 処理を終了する場合、コンシューマーは **Commit** メソッドを呼び出さずに、[IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) インターフェイスの参照を解放できます。 コンシューマーが行セットに挿入した行にアクセスして値を変更する機能や、そのような行を行セットから個別に削除する機能はありません。  
  
 一括コピーされる行は、サーバー上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用に形式が設定されます。 行の形式は、ANSI_PADDING など、接続やセッションに設定されたオプションの影響を受けます。 このオプションは、Native Client OLE DB プロバイダーを介して行われるすべての接続に対して既定で設定され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="see-also"></a>参照  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)  
  
