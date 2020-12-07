---
description: Context プロパティ (SecurityCertificate クラス)
title: Context プロパティ (SecurityCertificate)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Context Property (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Context property
ms.assetid: 65dd737f-81ce-479e-8219-7b1b4d8f57c7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7e6c2c0d42e7b6d38e5a252cb8a1052fc87ed47b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545292"
---
# <a name="context-property-securitycertificate-class"></a>Context プロパティ (SecurityCertificate クラス)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  セキュリティ証明書のコンテキストを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Context [= value]  
```  
  
## <a name="parts"></a>指定項目  
 *object*  
 セキュリティ証明書を表す [SecurityCertificate クラス](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 セキュリティ証明書のコンテキストを指定する **sint32** 配列値。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [サーバーのネットワーク プロトコルと Net-Library の構成](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
