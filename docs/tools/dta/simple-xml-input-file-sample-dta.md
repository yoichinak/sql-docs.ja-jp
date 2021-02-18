---
title: XML 入力ファイルの簡単なサンプル (DTA)
description: この記事には、データベース エンジン チューニング アドバイザーでワークロードをチューニングするために使用するサンプル XML 入力ファイルのサンプルが含まれています。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 5b00e4eb-1742-43ec-98d8-d84216b6b840
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 1b475ce68b38283903ecd7295a89b18fce6b9636
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100354415"
---
# <a name="simple-xml-input-file-sample-dta"></a>XML 入力ファイルの簡単なサンプル (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この簡単な XML 入力ファイルのサンプルをコピーして、お使いの XML エディターやテキスト エディターに貼り付け、ワークロードのチューニングのために使用することができます。 サンプルを貼り付けた後に、 **Server**、 **Database**、 **Schema**、 **Table**、 **Workload**、および **TuningOptions** 要素で指定する値を、特定のチューニング セッションの値に置き換えてください。 これらの要素で使用できる属性および子要素の詳細については、「 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)」を参照してください。 以下のサンプルでは、使用できる属性や子要素の一部だけを使用しています。  
  
## <a name="code"></a>コード  
 [!code-xml[InputFileSamples#SimpleXMLInputFile](../../tools/dta/codesnippet/xml/simple-xml-input-file-sa_1.xml)]  
  
## <a name="see-also"></a>参照  
 [データベース エンジン チューニング アドバイザーの起動および使用](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
