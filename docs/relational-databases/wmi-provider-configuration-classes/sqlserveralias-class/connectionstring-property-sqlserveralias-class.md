---
description: ConnectionString プロパティ (SqlServerAlias クラス)
title: ConnectionString プロパティ (SqlServerAlias)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ConnectionString Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b0a8cacce04ad0ef376d7ed6516b017f3c1b85d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550927"
---
# <a name="connectionstring-property-sqlserveralias-class"></a>ConnectionString プロパティ (SqlServerAlias クラス)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  サーバー接続別名に対応する接続を確立するために使用される接続文字列を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.ConnectionString [= value]  
```  
  
## <a name="parts"></a>指定項目  
 *object*  
 [の別名を表す](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) SqlServerAlias クラス [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 サーバー接続別名に対応する接続を確立するために使用される接続文字列を指定する文字列。  
  
## <a name="remarks"></a>解説  
  
