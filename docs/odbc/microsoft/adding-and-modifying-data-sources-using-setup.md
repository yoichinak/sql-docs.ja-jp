---
description: セットアップを使用してデータ ソースを追加および変更する
title: Setup | を使用してデータソースを追加および変更するMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8592c01897e691cdb6702c4efdfca6054655a793
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494742"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>セットアップを使用してデータ ソースを追加および変更する
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 データソースは、ネットワークライブラリ、サーバー、データベース、およびその他の属性を含めることができるデータへのパスを識別します。この場合、データソースは Oracle データベースへのパスです。 ドライバーマネージャーは、データソースに接続するために、Windows レジストリで特定の接続情報を確認します。  
  
 Odbc データソースアドミニストレーターによって作成されたレジストリエントリは、ODBC ドライバーマネージャーおよび ODBC ドライバーによって使用されます。 このエントリには、各データソースとそれに関連付けられているドライバーに関する情報が含まれています。 データソースに接続するには、その接続情報がレジストリに追加されている必要があります。  
  
 データソースを追加して構成するには、 [ODBC データソースアドミニストレーター](../../odbc/admin/odbc-data-source-administrator.md)を使用します。 ODBC 管理者は、データソースの接続情報を更新します。 データソースを追加すると、ODBC 管理者がレジストリ情報を更新します。  
  
### <a name="to-add-a-data-source-for-windows"></a>Windows のデータソースを追加するには  
  
1.  ODBC データソースアドミニストレーターを開きます。  
  
2.  [ODBC データソースアドミニストレーター] ダイアログボックスで、[追加] をクリックします。 [新しいデータソースを作成しています] ダイアログボックスが表示されます。  
  
3.  [Microsoft ODBC for Oracle] を選択し、[完了] をクリックします。 [Microsoft ODBC for Oracle セットアップ] ダイアログボックスが表示されます。  
  
4.  [データソース名] ボックスに、アクセスするデータソースの名前を入力します。 任意の名前を指定できます。  
  
5.  [説明] ボックスに、ドライバーの説明を入力します。 このオプションのフィールドは、データソースの接続先のデータベースドライバーを示します。 任意の名前を指定できます。  
  
6.  [ユーザー名] ボックスに、データベースのユーザー名 (ユーザー ID) を入力します。  
  
7.  [サーバー] ボックスに、アクセスする Oracle Server エンジンのデータベースエイリアスまたは接続文字列を入力します。  
  
8.  [OK] をクリックして、このデータソースを追加します。  
  
> [!NOTE]  
>  [データソース] ダイアログボックスが表示され、ODBC 管理者がレジストリ情報を更新します。 入力したユーザー名と接続文字列は、接続時にこのデータソースの既定の接続値になります。  
  
1.  [オプション] をクリックして、ODBC Driver for Oracle セットアップに関するより多くの仕様を作成します。  
  
    -   [**翻訳**]-[選択] をクリックして、読み込まれたデータ変換プログラムを選択します。 既定値は、\<No Translator> です。  
  
    -   **パフォーマンス** -[カタログ関数に注釈を含める] チェックボックスは、ドライバーが [sqlcolumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 結果セットの解説列を返すかどうかを指定します。 ODBC Driver for Oracle では、この値が設定されていない場合にアクセスが高速になります。  
  
         [SQL 列にシノニムを含める] チェックボックスは、ドライバーが列情報を返すかどうかを指定します。 [**バッファーサイズ**] フェッチされたデータを受信するために割り当てられたサイズ (バイト単位) を指定します。 ドライバーは、Oracle サーバーからの1つのフェッチが、指定されたサイズのバッファーを格納するのに十分な行数を返すように、フェッチを最適化します。 値が大きいほど、大量のデータをフェッチするときにパフォーマンスが向上する傾向があります。  
  
    -   **カスタマイズ** -[Odbc DayOfWeek 標準を適用する] チェックボックスで、結果セットが odbc 指定の曜日形式に準拠するかどうかを指定します (日曜日 = 1、土曜日 = 7)。 このチェックボックスがオフの場合、ロケール固有の Oracle 値が返されます。  
  
         SQLDescribeCol は**常に [有効桁数の値を返し**ます] チェックボックスを使用して、ドライバーが**SQLDescribeCol**の*cbcoldef*引数に対して0以外の値を返すかどうかを指定します。 この接続文字列属性は、計算された数値列や、有効桁数や小数点以下桁数のない数値として定義された列など、Oracle によって定義された小数点以下桁数がない列にのみ適用されます。 Oracle がその情報を提供していない場合、 **SQLDescribeCol** の呼び出しでは、有効桁数として130が返されます。 このチェックボックスがオフの場合、ドライバーは、これらの種類の列に対して0を返します。  
  
2.  [追加] をクリックして別のデータソースを追加するか、[閉じる] をクリックして終了します。  
  
### <a name="to-modify-a-data-source-for-windows"></a>Windows のデータソースを変更するには  
  
1.  ODBC データソースアドミニストレーターを開きます。 適切な [DSN] タブをクリックします。  
  
2.  変更する Oracle データソースを選択し、[構成] をクリックします。 [Microsoft ODBC for Oracle セットアップ] ダイアログボックスが表示されます。  
  
3.  該当するデータソースフィールドを変更し、[OK] をクリックします。  
  
 このダイアログボックスの情報の変更が完了すると、ODBC 管理者がレジストリ情報を更新します。
