---
description: ProtocolName プロパティ (ClientNetworkProtocol クラス)
title: ProtocolName プロパティ (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolName Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolName property
ms.assetid: f8527121-fbcd-4d30-9b4a-1461149cb5a8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1323d4c47555bfebb717ba1627e6b4fc7c22c94b
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91889019"
---
# <a name="protocolname-property-clientnetworkprotocol-class"></a>ProtocolName プロパティ (ClientNetworkProtocol クラス)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [クライアントプロトコルの構成](../../../database-engine/configure-windows/configure-client-protocols.md)によって指定された現在のネットワークプロトコルの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.ProtocolName [= value]  
```  
  
## <a name="parts"></a>指定項目  
 *object*  
 クライアントによって使用されるネットワークプロトコルを表す [Clientnetworkprotocol クラス](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) オブジェクト [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 [Setordervalue メソッド (ClientNetworkProtocol クラス)](./setordervalue-method-clientnetworkprotocol-class.md)によって参照される現在のクライアントネットワークプロトコルの名前を指定する文字列値。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [クライアントのネットワーク プロトコルと Net-Library の構成](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
