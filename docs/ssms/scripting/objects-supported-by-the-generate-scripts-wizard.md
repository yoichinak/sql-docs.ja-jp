---
title: スクリプト生成ウィザードでサポートされるオブジェクト
description: スクリプトの生成とパブリッシュ ウィザードでパブリッシュするのに役立つ可能性があるオブジェクトの種類を確認します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5b078e1b5e0f76a565aa0bd2d686836d24d5ba98
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100270871"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>スクリプト生成ウィザードでサポートされるオブジェクト
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  スクリプトの生成とパブリッシュ ウィザードは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]によってサポートされるオブジェクトのサブセットをサポートします。  
  
## <a name="supported-objects"></a>サポート対象のオブジェクト  
 次の表は、スクリプトの生成とパブリッシュ ウィザードでサポートされる、パブリッシュできるオブジェクトの一覧です。  
  
:::row:::
    :::column:::
        アプリケーション ロール
    :::column-end:::
    :::column:::
        データベース ロール
    :::column-end:::
    :::column:::
        スキーマ
    :::column-end:::
    :::column:::
        ユーザー定義集計
    :::column-end:::
    :::column:::
        ビュー*
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        アセンブリ
    :::column-end:::
    :::column:::
        DEFAULT 制約
    :::column-end:::
    :::column:::
        ストアド プロシージャ*
    :::column-end:::
    :::column:::
        ユーザー定義データ型
    :::column-end:::
    :::column:::
        XML スキーマ コレクション
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CHECK 制約
    :::column-end:::
    :::column:::
        フルテキスト カタログ
    :::column-end:::
    :::column:::
        シノニム
    :::column-end:::
    :::column:::
        ユーザー定義関数
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CLR (共通言語ランタイム) ストアド プロシージャ*
    :::column-end:::
    :::column:::
        インデックス
    :::column-end:::
    :::column:::
        テーブル
    :::column-end:::
    :::column:::
        ユーザー定義テーブル
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CLR ユーザー定義関数
    :::column-end:::
    :::column:::
        ルール
    :::column-end:::
    :::column:::
        ユーザー**
    :::column-end:::
    :::column:::
        ユーザー定義型
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

 \* 暗号化されずにパブリッシュされます。  
  
 ** データベースに存在するシステム ユーザー以外のユーザーはすべてロールとしてパブリッシュされます。  
  
  
