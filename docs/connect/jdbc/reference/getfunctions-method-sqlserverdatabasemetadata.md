---
description: getFunctions メソッド (SQLServerDatabaseMetaData)
title: getFunctions メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ede94f4024fc5c99dc120d4ad4137d8fe9df716
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99162981"
---
# <a name="getfunctions-method-sqlserverdatabasemetadata"></a>getFunctions メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  システム関数およびユーザー関数の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public ResultSet getFunctions(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *catalog*  
  
 データベース内のカタログの名前です。 空の文字列 "" の場合、結果にはカタログのない関数が含まれます。 **null** の場合、カタログ名は検索に使用されません。  
  
 *schemaPattern*  
  
 スキーマの名前です。 空の文字列 "" の場合、結果にはスキーマのない関数が含まれます。 **null** の場合、スキーマ名は検索に使用されません。  
  
 *functionNamePattern*  
  
 関数の名前です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getFunctions メソッドは、java.sql.DatabaseMetaData インターフェイスの getFunctions メソッドで規定されています。  
  
 このメソッドは、指定されたスキーマ名および関数名に一致するシステム関数およびユーザー関数だけを返します。  
  
> [!IMPORTANT]  
>  返される結果セットには、呼び出し元のユーザーに、実行するためのアクセス許可がない関数が含まれることがあります。  
  
 各関数の記述には、次の列が含まれます。  
  
|名前|Type|説明|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|関数が存在するデータベースの名前です。|  
|FUNCTION_SCHEM|**String**|関数が存在するスキーマの名前です。|  
|FUNCTION_NAME|**String**|関数の名前です。|  
|NUM_INPUT_PARAMS|**int**|今後の使用のために予約されています。現在は -1 の値を返します。|  
|NUM_OUTPUT_PARAMS|**int**|今後の使用のために予約されています。現在は -1 の値を返します。|  
|NUM_RESULT_SETS|**int**|今後の使用のために予約されています。現在は -1 の値を返します。|  
|REMARKS|**String**|関数についてのコメントです。|  
|FUNCTION_TYPE|**short**|関数の種類です。 次のいずれかの値を指定できます。<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
 返される結果セット内のすべての記述は、FUNCTION_CAT、FUNCTION_SCHEM、FUNCTION_NAME、および SPECIFIC_NAME で順序付けされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
