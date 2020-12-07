---
description: MSSQLSERVER_41396
title: MSSQLSERVER_41396 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41396 (Database Engine error)
ms.assetid: 4ff04042-8367-46f3-8a16-c94682d6eedb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d34ffc55e78426d82ed3b9d0e9e65aab7943e7af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471100"
---
# <a name="mssqlserver_41396"></a>MSSQLSERVER_41396
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|41396|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|MAX_SORT_ROWS_EXCEEDED|  
|メッセージ テキスト|並べ替え操作がバッファーの制限を超えました。 ストアド プロシージャの実行は中断されました。 詳細については、SQL Server オンライン ブックを参照してください。|  
  
## <a name="explanation"></a>説明  
ネイティブ コンパイル ストアド プロシージャは、メモリ内で並べ替え操作を実行します。 並べ替えバッファーのサイズには制限があります。 このエラーは、並べ替えバッファーのサイズがこの制限を超えることを意味します。 並べ替え操作およびストアド プロシージャの実行は中断されます。  
  
並べ替えバッファー内の各行またはエントリのサイズは、並べ替えられる行の数に加え、結合の数、およびクエリ内の集計関数の数と種類によって決まります。 クエリを単純化することで、各行のサイズを小さくできるため、並べ替えバッファー内にはより多くの行が収まります。 ベース テーブル内の行のサイズは、並べ替えバッファー内の各行またはエントリのサイズに影響しません。  
  
## <a name="user-action"></a>ユーザーの操作  
選択する行を減らすか、結合または集計関数を削除してクエリの複雑さを軽減してください。  
  
## <a name="see-also"></a>参照  
[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
