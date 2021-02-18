---
title: Server 要素 (DTA)
description: dta ユーティリティでは、Server 要素に、チューニングするデータベースが置かれているサーバーの識別情報が含まれます。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: ea5ebbbd957f509ff834f1cc966f5cf5020dc2ac
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345842"
---
# <a name="server-element-dta"></a>Server 要素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

チューニングするデータベースが置かれているサーバーの識別情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DTAInput>  
    <Server>  
    ...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特徴|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|**DTAInput** 要素につき 1 回の出現が必要です。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[DTAInput 要素 &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**子要素**|[Server の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Server の Database 要素 &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)|  
  
## <a name="remarks"></a>解説  
 **Server** 要素は、 **DTAInput** 要素に 1 個だけ指定できます。 この要素は、DTA XML スキーマの **ServerDetailsTypecomplexType** の名前です。 この **Server** 要素を **Configuration** 要素の子要素と混同しないでください。 詳細については、「[Configuration のサーバー要素 &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例は、SERVER001 上の **AdventureWorks** データベースの **Sales.SalesPerson** テーブルを指定する方法を示しています:  
  
```xml  
<Server>  
  <Name>SERVER001</Name>  
  <Database>  
    <Name>AdventureWorks</Name>  
    <Schema>  
      <Name>Sales</Name>  
      <Table>  
        <Name>SalesPerson</Name>  
      </Table>  
    </Schema>  
  </Database>  
</Server  
```  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
