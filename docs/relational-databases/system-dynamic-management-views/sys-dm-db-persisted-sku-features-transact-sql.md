---
description: dm_db_persisted_sku_features (Transact-sql)
title: dm_db_persisted_sku_features (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server]
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 552bb8927c8609a2cfa406243be102372b855c0c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548662"
---
# <a name="sysdm_db_persisted_sku_features-transact-sql"></a>dm_db_persisted_sku_features (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  の一部の機能 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] データベースファイルに情報を格納する方法を変更します。 これらの機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の特定のエディションでのみ使用できます。 これらの機能を備えたデータベースを、それらをサポートしない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションに移動することはできません。 現在のデータベースで有効になっているエディション固有の機能を一覧表示するには、dm_db_persisted_sku_features 動的管理ビューを使用します。
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降)。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|データベースでは有効になっているが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションでサポートされるとは限らない機能の外部名。 データベースをの利用可能なすべてのエディションに移行する前に、この機能を削除する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|feature_id|**int**|機能に関連付けられている機能 ID。 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>解説  
 特定のエディションで制限されている機能がデータベースで使用されていない場合、ビューは行を返しません。  
  
 dm_db_persisted_sku_features には、特定のエディションに限定された次のデータベース変更機能が表示される場合があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   **Changecapture**: データベースで変更データキャプチャが有効になっていることを示します。 変更データキャプチャを削除するには、 [sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) ストアドプロシージャを使用します。 詳細については、「[変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)」を参照してください。  
  
-   **Columnstoreindex**: 少なくとも1つのテーブルに列ストアインデックスがあることを示します。 この機能をサポートしていないのエディションにデータベースを移動できるようにするに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、 [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) または [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) ステートメントを使用して列ストアインデックスを削除します。 詳細については、「 [列ストアインデックス](../../relational-databases/indexes/columnstore-indexes-overview.md)」を参照してください。  
  
    **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。  
  
-   **Compression**: 少なくとも1つのテーブルまたはインデックスで、データ圧縮または vardecimal ストレージ形式が使用されていることを示します。 この機能をサポートしていないのエディションにデータベースを移動できるようにするには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [alter TABLE](../../t-sql/statements/alter-table-transact-sql.md) ステートメントまたは [alter INDEX](../../t-sql/statements/alter-index-transact-sql.md) ステートメントを使用して、データ圧縮を解除します。 vardecimal ストレージ形式を削除するには、sp_tableoption ステートメントを使用します。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。  
  
-   複数の**fsコンテナ**: データベースが複数の FILESTREAM コンテナーを使用することを示します。 データベースには、複数のコンテナー (ファイル) を含む FILESTREAM ファイルグループがあります。 詳細については、「[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)」をご覧ください。  
  
-   **Inmemoryoltp**: データベースがインメモリ oltp を使用することを示します。 データベースには MEMORY_OPTIMIZED_DATA ファイルグループがあります。 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
  **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降)。 
  
-   **パーティション.** データベースにパーティションテーブル、パーティションインデックス、パーティション構成、またはパーティション関数が格納されていることを示します。 Enterprise edition または Developer edition 以外ののエディションにデータベースを移動できるようにするに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、テーブルを1つのパーティションに変更するだけでは不十分です。 パーティションテーブルを削除する必要があります。 テーブルにデータが含まれている場合は、[パーティションの切り替え] を使用して各パーティションを非パーティションテーブルに変換します。 次に、パーティションテーブル、パーティション構成、およびパーティション関数を削除します。  
  
-   **TransparentDataEncryption。** 透過的なデータ暗号化を使用してデータベースが暗号化されていることを示します。 Transparent data encryption を削除するには、ALTER DATABASE ステートメントを使用します。 詳細については、「[透過的なデータ暗号化 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。  

> [!NOTE]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]Service Pack 1 以降では、TransparentDataEncryption を除くこれらの機能が使用さ**れています。** は、複数のエディションで使用でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 Enterprise edition または Developer edition に限定されません。

 特定のエディションでのみ使用できる機能がデータベースで使用されているかどうかを確認するには、データベースで次のステートメントを実行します。  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;データベース関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [エディションと SQL Server 2016 のサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [エディションと SQL Server 2017 のサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
