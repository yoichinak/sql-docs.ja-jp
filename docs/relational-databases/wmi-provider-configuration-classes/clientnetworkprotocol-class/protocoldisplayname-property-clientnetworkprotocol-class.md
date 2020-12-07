---
description: ProtocolDisplayName プロパティ (ClientNetworkProtocol クラス)
title: ProtocolDisplayName プロパティ (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolDisplayName Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDisplayName property
ms.assetid: af194304-5600-48b5-9e93-c2fa95594909
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e0779c737456a9b898895cab2b187fa090b0a6fc
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91889035"
---
# <a name="protocoldisplayname-property-clientnetworkprotocol-class"></a>ProtocolDisplayName プロパティ (ClientNetworkProtocol クラス)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [クライアントプロトコルの構成](../../../database-engine/configure-windows/configure-client-protocols.md)によって指定されたクライアントネットワークプロトコルの表示名を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.ProtocolDisplayName [= value]  
```  
  
## <a name="parts"></a>指定項目  
 *object*  
 クライアントによって使用されるネットワークプロトコルを表す [Clientnetworkprotocol クラス](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) オブジェクト [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 クライアント ネットワーク プロトコルの表示名を指定する文字列値。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [クライアントのネットワーク プロトコルと Net-Library の構成](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
