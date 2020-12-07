---
description: setIntegratedSecurity メソッド (SQLServerDataSource)
title: setIntegratedSecurity メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b172631e774f5ea9da15873a1e8a00121ab46faf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431854"
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>setIntegratedSecurity メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  integratedSecurity プロパティが有効であるかどうかを示す **Boolean** 値が設定されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *enable*  
  
 integratedSecurity が有効である場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>解説  
 アプリケーションのユーザーを認証するために [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって Windows 資格情報が使用されることを示す場合は、"**true**" に設定します。 "**true**" の場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、コンピューターまたはネットワーク ログオン時に提供された資格情報を見つけるために、ローカル コンピューターの資格情報のキャッシュが検索されます。 "**false**" の場合は、ユーザー名とパスワードを指定する必要があります。  
  
> [!NOTE]  
>  このプロパティは、[!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows オペレーティング システムのみでサポートされています。  
  
 統合認証の使用方法の詳細については、「[接続 URL の構築](../../../connect/jdbc/building-the-connection-url.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
