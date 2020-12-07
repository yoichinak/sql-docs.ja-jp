---
title: SQLServerConnection クラス
description: JDBC Driver for SQL Server の SQLServerConnection クラスのパブリック API 詳細について説明します。
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6827b79b4d1cc7b3f66db3c53c338614ec49fc3
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411478"
---
# <a name="sqlserverconnection-class"></a>SQLServerConnection クラス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースへの JDBC 接続を表します。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **実装:** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md)、java.io.Serializable  
  
## <a name="syntax"></a>構文  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>解説  
 SQLServerConnection では、JDBC 接続プールがサポートされており、JDBC の物理接続または JDBC の論理接続のいずれかを使用できます。 SQLServerConnection は、それから作成されたすべてのステートメントのトランザクション制御を管理し、XAResource アダプター経由で管理される XA の分散トランザクションに参加できます。  
  
 SQLServerConnection により、準備されたステートメント ハンドルのプールが管理されます。 ステートメントは 1 回だけ準備され、通常はパラメーターに対して異なるデータ値を指定し、何度も実行されます。 準備されたステートメントは、論理 (プール) 接続の終了後も維持されます。  
  
> [!NOTE]  
>  SQLServerConnection はスレッド セーフではありません。 ただし、単一の接続から作成された複数のステートメントは、同時スレッドで同時に処理することができます。  
  
 このクラスでは、SQLServerConnection クラス、java.sql.connection インターフェイス、および ISQLServerConnection インターフェイスへのラップ解除がサポートされます。 詳細については、「[ラッパーとインターフェイス](../../../connect/jdbc/wrappers-and-interfaces.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
