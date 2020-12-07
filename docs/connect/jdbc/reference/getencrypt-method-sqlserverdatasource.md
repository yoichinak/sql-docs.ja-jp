---
description: getEncrypt メソッド (SQLServerDataSource)
title: getEncrypt メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getEncrypt Method (SQLServerDataSource)
apilocation:
- getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09beeea5d623e50d5fcdbf562151631cbc67124d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436134"
---
# <a name="getencrypt-method-sqlserverdatasource"></a>getEncrypt メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  encrypt プロパティが有効であるかどうかを示す **Boolean** 値が返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>戻り値  
 encrypt プロパティが有効である場合は、**true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>解説  
 encrypt プロパティが **true** に設定されている場合、サーバーに証明書がインストールされていれば、サーバーとクライアント間で送信されるすべてのデータで TLS 暗号化が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で確実に使用されることを [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] は保証します。  
  
 encrypt プロパティが指定されていないか、または **false** に設定されている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がドライバーによって TLS 暗号化のサポートを強制されることはありません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが TLS 暗号化を強制的に使用するように構成されていない場合、接続は暗号化なしで確立します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが TLS 暗号化を強制的に使用するように構成されている場合は、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では使用中の Java 仮想マシン (JVM) が正常に構成されていれば自動的に TLS 暗号化が有効になり、そうでなければ接続が終了してエラーが生成されます。 暗号化プロパティが設定されていない場合、[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) メソッドは既定値の **false** が返されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
