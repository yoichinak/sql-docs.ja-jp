---
description: '&#x40;&#x40;CPU_BUSY (Transact-SQL)'
title: CPU_BUSY (Transact-SQL)
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@CPU_BUSY_TSQL'
- '@@CPU_BUSY'
dev_langs:
- TSQL
helpviewer_keywords:
- CPU [SQL Server]
- status information [SQL Server], CPU
- ticks [SQL Server]
- time [SQL Server], CPU activity
- '@@CPU_BUSY function'
- statistical information [SQL Server], CPU
- CPU [SQL Server], activity
ms.assetid: 81ae0e64-79fa-4a74-9aa5-37045c4cd211
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8d921cdb5e8550942ade08f0e68d0337864d2e38
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91114851"
---
# <a name="x40x40cpu_busy-transact-sql"></a>&#x40;&#x40;CPU_BUSY (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この関数は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最後の起動以降にアクティブな操作に使用した時間を返します。 `@@CPU_BUSY` は、CPU 時間の増分 (つまり "ティック") 単位の結果を返します。 この値はすべての CPU 時間を累積したものなので、実際の経過時間を超える場合があります。 マイクロ秒に変換するには、[@@TIMETICKS](./timeticks-transact-sql.md) を乗算します。
  
> [!NOTE]  
>  @@CPU_BUSY または @@IO_BUSY で返される時間が、約 49 日分の累積 CPU 時間を超えた場合は、演算オーバーフロー警告が表示されることがあります。 その場合、`@@CPU_BUSY`、`@@IO_BUSY`、および `@@IDLE` の各変数は正確ではありません。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```syntaxsql
@@CPU_BUSY  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]


## <a name="return-types"></a>戻り値の型
**integer**
  
## <a name="remarks"></a>注釈  
CPU アクティビティなどの複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 統計情報を含むレポートを表示するには、[sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md) を実行します。
  
## <a name="examples"></a>例  
この例では、現在の日付と時刻の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU アクティビティを返します。 この例では、値の 1 つを `float` データ型に変換します。 こうすることで、マイクロ秒単位の値を計算する際の算術オーバーフローの問題を回避できます。
  
```sql
SELECT @@CPU_BUSY * CAST(@@TIMETICKS AS FLOAT) AS 'CPU microseconds',   
   GETDATE() AS 'As of' ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
CPU microseconds As of
---------------- -----------------------
18406250         2006-12-05 17:00:50.600
```
  
## <a name="see-also"></a>関連項目
[sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE &#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md):  
[システム統計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  
