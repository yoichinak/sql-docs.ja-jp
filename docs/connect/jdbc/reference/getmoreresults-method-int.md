---
description: getMoreResults (int) メソッド
title: getMoreResults メソッド (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73d18f6319d0ddfbe362a21742e99c27e3637691
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435404"
---
# <a name="getmoreresults-method-int"></a>getMoreResults (int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの次の結果に移動し、渡されたモードで指定された指示に従って、現在開いているすべての結果セット オブジェクトを処理します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *mode*  
  
 現在開いている結果セット オブジェクトの処理方法を示す **int** です。 次のいずれかの定数を指定する必要があります。  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT (JDBC ドライバーではサポートされていません)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>戻り値  
 返された結果が結果セットである場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getMoreResults メソッドは、java.sql.Statement インターフェイスの getMoreResults メソッドで指定されています。  
  
 結果を取得する前に getMoreResults メソッドを呼び出した場合、このメソッドは引数 *mode* で指定されたとおりに動作し、次の結果に移動します。  
  
> [!NOTE]  
>  JDBC ドライバーは、定数 KEEP_CURRENT_RESULT の使用をサポートしていません。 この定数を使用すると、例外がスローされます。  
  
## <a name="see-also"></a>参照  
 [getMoreResults メソッド &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
