---
description: ErrorControl プロパティ (SqlService クラス)
title: ErrorControl プロパティ (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ErrorControl Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6c0c802c236495a5de48c2617a76f4422e608fca
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545247"
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl プロパティ (SqlService クラス)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  起動時にサービスを開始できなかった場合のエラーの重大度を取得または設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>指定項目  
 *object*  
 サービスを表す [SqlService クラス](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 起動時にサービスが失敗した場合にレポートされるエラーの重大度を指定する文字列値。 次の表に、それぞれの値を示します。  
  
 無視  
 ユーザーへの通知が行われません。  
  
 標準  
 ユーザーへの通知が行われます。  
  
 Severe  
 システムは最後の正しい構成で再起動されます。  
  
 Critical  
 正しい構成でシステムの再起動が試行されます。  
  
 Unknown  
 重大度が不明です。  
  
## <a name="remarks"></a>解説  
 値は、失敗が発生した場合に、起動プログラムによって行われるアクションを示しています。 すべてのエラーは、コンピューター システムによって記録されます。  
  
## <a name="see-also"></a>参照  
 [サービスの開始および停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
