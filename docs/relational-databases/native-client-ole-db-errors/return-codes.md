---
title: リターンコード (Native Client OLE DB プロバイダー)
description: SQL Server Native Client OLE DB でサポートされるリターンコードについて説明します。これには、一般的に発生する HRESULT 値 DB_S_ERRORSOCCURRED が含まれます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2644a34817c4319dff877a162963b2525d259cae
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869291"
---
# <a name="return-codes-native-client-ole-db-provider"></a>リターンコード (Native Client OLE DB プロバイダー)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  最も基本的なレベルでは、メンバー関数は成功するか失敗するかのどちらかです。 それよりもやや詳細なレベルでは、関数は成功しても、その成功はアプリケーション開発者が意図した状態ではない場合があります。  
  
 OLE DB のリターン コードの詳細については、「[リターン コード (OLE DB)](/previous-versions/windows/desktop/ms725451(v=vs.85))」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーのメンバー関数が S_OK を返すと、関数は成功します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーのメンバー関数が S_OK を返さない場合、OLE/COM HRESULT 展開に失敗し、IS_ERROR マクロは関数の全体的な成功または失敗を判断できます。  
  
 失敗した場合、または IS_ERROR が TRUE を返した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーは、メンバー関数の実行が失敗したことを保証します。 失敗した場合、または IS_ERROR が FALSE を返し、HRESULT が S_OK と一致しない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーコンシューマーは、何らかの意味で関数が成功したことを保証します。 コンシューマーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのエラーインターフェイスから、この "情報で成功" を返す詳細情報を取得できます。 また、関数が明確に失敗した場合 (失敗したマクロが TRUE を返した場合) は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのエラーインターフェイスから拡張エラー情報を取得できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーは、通常、"情報による成功" という HRESULT を返す DB_S_ERRORSOCCURRED に遭遇します。 通常、DB_S_ERRORSOCCURRED を返すメンバー関数では、コンシューマーに状態値を提供するパラメーターが 1 つ以上定義されています。 コンシューマーは状態値パラメーターに返される情報以外のエラー情報を取得できない場合があるので、状態値が提供された場合にこの値を取得できるアプリケーション ロジックを実装することをお勧めします。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーのメンバー関数は、成功コード S_FALSE を返しません。 すべて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Native Client OLE DB プロバイダーのメンバー関数は、成功を示すために常に S_OK を返します。  
  
## <a name="see-also"></a>参照  
 [エラー](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
