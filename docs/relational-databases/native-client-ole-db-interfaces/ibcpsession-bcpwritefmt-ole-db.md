---
description: 'IBCPSession:: BCPWriteFmt (Native Client OLE DB プロバイダー)'
title: 'IBCPSession:: BCPWriteFmt (Native Client OLE DB provider) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IBCPSession::BCPWriteFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPWriteFmt method
ms.assetid: add50425-2ed6-411a-a391-4ce63c364892
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aed7080561bdf82ea9f921dfac68a11ece8282e6
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081591"
---
# <a name="ibcpsessionbcpwritefmt-native-client-ole-db-provider"></a>IBCPSession:: BCPWriteFmt (Native Client OLE DB プロバイダー)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  フォーマット ファイルに列ごとのフォーマット情報を書き込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT BCPWriteFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>解説  
 フォーマット ファイルでは、一括コピーで作成されるデータ ファイルのデータの形式を指定します。 [IBCPSession::BCPColumns](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) メソッドと [IBCPSession::BCPColFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) メソッドの呼び出しでは、データ ファイルの形式を定義します。 **BCPWriteFmt** メソッドでは、この定義を pwszFormatFile 引数で参照されるファイルに保存します。  
  
 **BCPWriteFmt** メソッドでは、XML 形式またはテキスト形式のいずれかの形式でフォーマット ファイルを保存できます。 そのためには、BCP_OPTION_XML 制御オプションを指定して [IBCPSession::BCPControl](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) メソッドを使用する必要があります。  
  
 保存されたフォーマット ファイルを読み込むには、[IBCPSession::BCPReadFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) メソッドを使用します。  
  
## <a name="arguments"></a>引数  
 *pwszFormatFile*[in]  
 データ ファイルのフォーマット情報を含むファイルのパスとファイル名。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。詳細を確認するには、[ISQLServerErrorInfo](isqlservererrorinfo-geterrorinfo-ole-db.md) インターフェイスを使用してください。  
  
 E_OUTOFMEMORY  
 メモリ不足エラーです。  
  
 E_UNEXPECTED  
 メソッドの呼び出しが予期されませんでした。 たとえば、このメソッドが呼び出される前に、[IBCPSession::BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) メソッドが呼び出されなかった場合などです。  
  
## <a name="see-also"></a>参照  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [一括コピー操作の実行](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
