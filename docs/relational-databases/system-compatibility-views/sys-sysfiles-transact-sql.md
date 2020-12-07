---
description: sys.sysファイル (Transact-sql)
title: sys.sysファイル (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
author: rothja
ms.author: jroth
ms.openlocfilehash: dfc6430023a4123e029ebdec4f2fca56491b3632
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455113"
---
# <a name="syssysfiles-transact-sql"></a>sys.sysファイル (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース内のファイルごとに1行のデータを格納します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|各データベースで一意なファイル ID 番号です。|  
|**groupid**|**smallint**|ファイルグループの id 番号。|  
|**size**|**int**|ファイルのサイズ (8 KB ページ単位)。|  
|**maxsize**|**int**|最大ファイル サイズ (8 KB ページ単位) です。<br /><br /> 0 = ファイル サイズが拡張しないことを表します。<br /><br /> -1 = ディスクがいっぱいになるまでファイル サイズが拡張します。<br /><br /> 268435456 = ログファイルは、最大サイズの 2 TB まで拡張されます。<br /><br /> 注: ログファイルのサイズを無制限にアップグレードしたデータベースは、ログファイルの最大サイズに対して-1 を報告します。|  
|**成長**|**int**|データベースの拡張サイズ。 **Status**の値に応じて、ページ数またはファイルサイズのパーセンテージのいずれかになります。<br /><br /> 0 = ファイル サイズが拡張しないことを表します。|  
|**status**|**int**|メガバイト (MB) またはキロバイト (KB) のいずれかの **拡張** 値のステータスビット。<br /><br /> 0x2 = ディスク ファイル。<br /><br /> 0x40 = ログ ファイル。<br /><br /> 0x100000 = 拡張。 この値は、ページ数ではなくパーセンテージです。|  
|**perf**|**int**|予約済み。|  
|**name**|**sysname**|ファイルの論理名です。|  
|**ファイル名**|**nvarchar(260)**|物理デバイスの名前です。 これには、ファイルの完全パスが含まれます。|  
  
## <a name="see-also"></a>参照  
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
