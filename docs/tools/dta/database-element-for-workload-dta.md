---
title: Workload の Database 要素 (DTA)
description: dta ユーティリティでは、Workload の Database 要素により、ワークロード トレース テーブルのあるデータベースを指定します。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: c772a91b39917acd3e009009c44123fc31510eca
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100342009"
---
# <a name="database-element-for-workload-dta"></a>Workload の Database 要素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

ワークロード トレース テーブルのあるデータベースを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Workload>  
  <Database>  
   ...code removed here...  
  </Database>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特徴|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|他の種類のワークロードが指定されていない場合は、1 回の出現が必要です。 **EventString** 親要素に対しては、 **File**、 **Database** 、または **Workload** 子要素を指定する必要がありますが、使用できるのは 1 種類だけです。 たとえば、ワークロードを **Database** 要素で指定した場合、同じ XML 入力ファイル内でワークロードを **File** 要素で指定することはできません。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Workload 要素 &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)|  
|**子要素**|[Database の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Database の Schema 要素 &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>解説  
 この要素は、データベース エンジン チューニング アドバイザー XML スキーマの **DatabaseDetailsTypecomplexType** の名前です。 この **Database** 要素を、ルートの親要素が **Configuration** 要素である他の要素と混同しないでください (「[Configuration の Database 要素 &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)」を参照)。  
  
## <a name="example"></a>例  
 この **Database** 要素の使用例については、「 [Workload 要素 &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)」のコード例をご覧ください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
