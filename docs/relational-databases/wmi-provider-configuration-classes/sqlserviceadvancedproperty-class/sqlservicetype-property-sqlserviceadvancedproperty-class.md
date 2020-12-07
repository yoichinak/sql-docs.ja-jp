---
description: SqlServiceType プロパティ (SqlServiceAdvancedProperty クラス)
title: SqlServiceType プロパティ (Sqlserviceadvanced プロパティ)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a726b0e38909b8831926da20bd6682f2b244f9a7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550819"
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>SqlServiceType プロパティ (SqlServiceAdvancedProperty クラス)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  詳細プロパティに関連付けられたマネージド サービスの型を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.SetBoolValue(NumValue)  
```  
  
## <a name="parts"></a>指定項目  
 *object*  
 詳細プロパティを表す [SqlServiceAdvancedProperty クラス](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスの種類を指定する uint32 値。  
  
## <a name="remarks"></a>解説  
 戻り値は次のいずれかです。  
  
|Type|定義|  
|----------|----------------|  
|*1*|MSSQLSERVER は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスです。|  
|*2*|SQLSERVERAGENT は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスです。|  
|*3*|MSFTESQL は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フルテキスト検索エンジン サービスです。|  
|*4*|MsDtsServer は [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] サービスです。|  
|*5*|MSSQLServerOLAPService は [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] サービスです。|  
|*6*|ReportServer は [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サービスです。|  
|*7*|SQLBrowser は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Browser サービスです。|  
|*8*|Nsservice.exe は [!INCLUDE[ssNoVersion](../../../includes/ssns-md.md)] Notification service です。|  
|*9*|MSSQLFDLauncher は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フルテキストフィルターデーモンランチャーサービスです。|  
|"*10*"|SQLPBENGINE は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Polybase エンジンサービスです。|  
|*11*|SQLPBDMS は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Polybase データ移動サービスです。|  
|*12*|MSSQLLaunchpad は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] スタートパッドサービスです。|  
  
## <a name="see-also"></a>参照  
 [サービスの開始および停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
