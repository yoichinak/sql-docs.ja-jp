---
description: '&#x40;&#x40;CONNECTIONS (Transact-SQL)'
title: '@@CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- '@@CONNECTIONS'
- '@@CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CONNECTIONS function'
- connections [SQL Server], number of
- connections [SQL Server], attempted
- number of connection attempts
- attempted connections
ms.assetid: c59836a8-443c-4b9a-8b96-8863ada97ac7
author: cawrites
ms.author: chadam
ms.openlocfilehash: 0d8e3ee7fcdaf287ecb0919c8c3215c2adc6aec7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99184229"
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;CONNECTIONS (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この関数は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最後に開始された後に試行された接続数 (成功と失敗の両方) を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```syntaxsql
@@CONNECTIONS  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
**integer**
  
## <a name="remarks"></a>注釈  
接続の数はユーザーの数とは異なります。 たとえば、アプリケーションでは、ユーザーがこれらの接続を監視することなく、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への複数の接続を開くことができます。
  
接続試行回数など、いくつかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 統計情報を含むレポートを表示するには、**sp_monitor** を実行します。
  
@@MAX_CONNECTIONS は、サーバーに対する同時接続の最大許容数です。 @@CONNECTIONS はログインが試行されるたびに増えるため、@@CONNECTIONS は @@MAX_CONNECTIONS を超える可能性があります。
  
## <a name="examples"></a>例  
この例では、現在の日付と時刻のログイン試行回数を返します。
  
```sql
SELECT GETDATE() AS 'Today''s Date and Time',   
@@CONNECTIONS AS 'Login Attempts';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
``` 
Today's Date and Time  Login Attempts  
---------------------- --------------  
12/5/2006 10:32:45 AM  211023         
```  
  
## <a name="see-also"></a>関連項目
[システム統計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md):
  
  
