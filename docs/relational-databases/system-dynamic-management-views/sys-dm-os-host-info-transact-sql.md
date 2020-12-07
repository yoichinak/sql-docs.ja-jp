---
description: sys.dm_os_host_info (Transact-sql)
title: sys.dm_os_host_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e2c6e374061a847e168421b30971469ff60e4348
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834084"
---
# <a name="sysdm_os_host_info-transact-sql"></a>sys.dm_os_host_info (Transact-sql)
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

オペレーティングシステムのバージョン情報を表示する1行を返します。  
  
|列名 |データ型 |説明 |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar (256)** |オペレーティングシステムの種類: Windows または Linux |
|**host_distribution** |**nvarchar (256)** |オペレーティングシステムの説明。 |
|**host_release**|**nvarchar (256)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows オペレーティングシステムのリリース (バージョン番号)。 値と説明の一覧については、「 [オペレーティングシステムのバージョン (Windows)](/windows/desktop/SysInfo/operating-system-version)」を参照してください。 <br> Linux の場合、は空の文字列を返します。 |  
|**host_service_pack_level**|**nvarchar (256)**|Windows オペレーティングシステムの Service pack のレベル。 <br> Linux の場合、は空の文字列を返します。 |  
|**host_sku**|**int**|Windows 株価保持ユニット (SKU) ID。 SKU Id と説明の一覧については、「 [Getproductinfo 関数](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getproductinfo)」を参照してください。 NULL 値が許可されます。 <br> Linux の場合、は NULL を返します。 |  
|**os_language_version**|**int**|オペレーティングシステムの Windows ロケール識別子 (LCID)。 LCID 値と説明の一覧については、「 [Microsoft によって割り当てられたロケール id](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)」を参照してください。 null にすることはできません。|  

## <a name="remarks"></a>注釈  
このビューは、Windows と Linux を区別するために列を追加する [sys.dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)に似ています。
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
`SELECT`既定では、に対する権限 `sys.dm_os_host_info` がロールに付与され `public` ます。 取り消す場合は、 `VIEW SERVER STATE` サーバーに対する権限が必要です。   
 
> [!CAUTION]
>  バージョン [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.3 以降では、 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] `SELECT` `sys.dm_os_host_info` に接続するために、バージョン17でに対するアクセス許可が必要です [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 。 `SELECT`権限がから取り消された場合 `public` 、 `VIEW SERVER STATE` 最新バージョンの SSMS で接続できるのは、権限を持つログインのみです。 (などの他のツールは、 `sqlcmd.exe` に対する権限なしで接続でき `SELECT` `sys.dm_os_host_info` ます)。

  
## <a name="examples"></a>例  
 次の例では、 **sys.dm_os_host_info** ビューからすべての列を返します。  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Windows での結果セットの例を次に示します。
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1033 |  

Linux での結果セットの例を次に示します。
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |1033 |  

  
## <a name="see-also"></a>参照  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-sql)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
