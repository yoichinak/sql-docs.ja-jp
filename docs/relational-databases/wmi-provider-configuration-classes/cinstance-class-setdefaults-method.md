---
description: CInstance クラス - SetDefaults メソッド
title: SetDefaults メソッド (CInstance)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (CInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: ed9e99c2-3e28-4ee8-bc20-61ca05984973
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 99771d12be4c10d8d4b823ceb788e9722d417fca
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890982"
---
# <a name="cinstance-class---setdefaults-method"></a>CInstance クラス - SetDefaults メソッド
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 既存のデータを上書きするオプションを使用して、クライアントのインスタンスのすべての既定値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>指定項目  
 *object*  
 [クライアント インスタンスを表す](../../relational-databases/wmi-provider-configuration-classes/cinstance-class.md) CInstance クラス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクト。  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*OverwriteAll*|クライアントのインスタンス上の既存の値を上書きするかどうかを指定するブール値 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。既存のデータを上書きする場合は **true** 、既存のデータを上書きしない場合は **false** を指定します。|  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 **uint32** 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [クライアント プロトコルの構成](../../database-engine/configure-windows/configure-client-protocols.md)  
  
