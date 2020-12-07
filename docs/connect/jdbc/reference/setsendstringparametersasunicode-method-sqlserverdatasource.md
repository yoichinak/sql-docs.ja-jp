---
description: setSendStringParametersAsUnicode メソッド (SQLServerDataSource)
title: setSendStringParametersAsUnicode メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49198d63-76cb-4843-8d04-e49b1fbb6916
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8957b431a3aabce4ed4564867c052ef63502350
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458354"
---
# <a name="setsendstringparametersasunicode-method-sqlserverdatasource"></a>setSendStringParametersAsUnicode メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  サーバーへの文字列パラメーターの UNICODE 形式による送信が有効になっているかどうかを示す **boolean** 値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setSendStringParametersAsUnicode(boolean sendStringParametersAsUnicode)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sendStringParametersAsUnicode*  
  
 サーバーに文字列パラメーターが UNICODE 形式で送信される場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>解説  
 sendStringParametersAsUnicode プロパティが **true** (既定値) に設定されている場合、文字列パラメーターは、UNICODE 形式でサーバーに送信されます。 sendStringParametersAsUnicode が **false** に設定されている場合、UNICODE ではなく ASCII/MBCS 形式で、文字列パラメーターがサーバーに送信されます。 sendStringParametersAsUnicode が設定されていない場合、[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md) は既定値の **true** を返します。  
  
 sendStringParametersAsUnicode 接続プロパティについて詳しくは、「[接続プロパティの設定](../../../connect/jdbc/setting-the-connection-properties.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
