---
title: インライン ワークロードを使用した XML 入力ファイルのサンプル
description: この記事には、データベース エンジン チューニング アドバイザーでワークロードをチューニングするために使用するインラインワークロードがあるサンプル XML 入力ファイルが含まれています。
titleSuffix: DTA
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 20c8bfa5bb73c8b52e7637c65d9822498a96e4ae
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100339963"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>インライン ワークロードを使用した XML 入力ファイルのサンプル (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この XML 入力ファイルのサンプルでは、ワークロードを **EventString** 要素を使用して指定しています。このサンプルをコピーして、お使いの XML エディターやテキスト エディターに貼り付けてください。 個別のワークロード ファイルを使用する代わりに、 **EventString** 要素を使用して XML 入力ファイル内の [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ワークロードを指定することができます。 このサンプルを編集ツールにコピーした後に、 **Server**、 **Database**、 **Schema**、 **Table**、 **Workload**、 **EventString**、および **TuningOptions** 要素で指定する値を、特定のチューニング セッションの値に置き換えてください。 これらの要素で使用できるすべての属性および子要素の詳細については、「 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)」を参照してください。 以下のサンプルでは、使用できる属性や子要素の一部だけを使用しています。

## <a name="code"></a>コード

[!code-xml[InputFileSamples#InlineWorkloadInputFile](../../tools/dta/codesnippet/xml/xml-input-file-sample-wi_1.xml)]

## <a name="comments"></a>説明

`USE database_name` ステートメントは、 **EventString** 要素に含まれるインライン ワークロードで指定できます。

## <a name="see-also"></a>参照

- [データベース エンジン チューニング アドバイザーの起動および使用](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)
- [データベース エンジン チューニング アドバイザーからの出力の表示および操作](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)
- [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)