---
title: File 要素 (DTA)
description: dta ユーティリティでは、File 要素により、ワークロード ファイルを指定します。これには、チューニングするデータベースに対して実行する Transact-SQL ステートメントが含まれています。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- File element
ms.assetid: 73dce835-9a80-4aef-8e0f-9dcf07dd5b80
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: bb7d075fba09db4de518018f29190cb0c351bf27
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100335975"
---
# <a name="file-element-dta"></a>File 要素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

ワークロード ファイルを指定します。 ワークロードとは、チューニングするデータベースに対して実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのセットです。 ワークロード ファイルには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト (.sql) またはトレース ファイル (.trc) を指定できます。 詳細については、「[データベース エンジン チューニング アドバイザーの起動および使用](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DTAInput>  
  <Server>...</Server>  
  <Workload>  
    <File>...</File>  
  </Workload>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特徴|説明|  
|--------------------|-----------------|  
|**データ型と長さ**|**string** データ型を使用して、ワークロード ファイルのあるディレクトリへのパスを指定します。 次に例を示します。<br /><br /> `<File>C:\Tuning\tun.sql</File>`<br /><br /> 長さの制限はサーバーによって決まることに注意してください。|  
|**既定値**|[なし] :|  
|**個数**|他の種類のワークロードが指定されていない場合は、1 回の出現が必要です。 **EventString** 親要素に対しては、 **File**、 **Database** 、または **Workload** 子要素を指定する必要がありますが、使用できるのは 1 種類だけです。 たとえば、 **File** 要素を使用してワークロードを指定した場合は、同じ XML 入力ファイル内で **Database** 要素を使用してワークロードを指定することはできません。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Workload 要素 &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)|  
|**子要素**|[なし] :|  
  
## <a name="example"></a>例  
 この要素の使用例については、「[XML 入力ファイルの簡単なサンプル &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
