---
description: setPacketSize メソッド (SQLServerDataSource)
title: setPacketSize メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c178e8412de5bc59072fa9f6734fd79dad61ba52
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178738"
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>setPacketSize メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との通信に使用される現在のネットワーク パケット サイズが設定されます (バイトで指定します)。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *packetSize*  
  
 ネットワーク パケット サイズを含む **int** 値です。  
  
## <a name="remarks"></a>解説  
 このプロパティの値の許容範囲は、[-1 | 0 | 512..32767] です。 このプロパティが許容範囲外の値に設定されている場合は、例外が発生します。  
  
 TLS (トランスポート層セキュリティ) (以前の SSL (Secure Sockets Layer)) 暗号化を使用して接続しているときに、アプリケーションで packetSize プロパティを設定する場合があります。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、パケット サイズがサーバーとの間でネゴシエートされます。 encrypt プロパティが "**true**" に設定されている場合に、ネゴシエートされたパケット サイズが Java 仮想マシン (JVM) の既定のセキュリティ プロバイダーの TLS レコード サイズを超えるときは、ドライバーでエラーが発生して接続が終了します。  
  
 また、TLS 暗号化を要求せずにアプリケーションで packetSize プロパティが設定される場合もあります。 この場合、クライアントによる TLS 暗号化のサポートをサーバーが求めている場合は、JVM の既定のセキュリティ プロバイダーの TLS レコード サイズが、ドライバーによってチェックされます。 packetSize プロパティが JVM の既定のセキュリティ プロバイダーの TLS レコード サイズを超えるときは、ドライバーでエラーが発生して接続が終了します。  
  
 TLS の使用方法の詳細については、[暗号化の使用](../../../connect/jdbc/using-ssl-encryption.md)に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
