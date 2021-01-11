---
title: バイナリ データの取得
description: '`CommandBehavior`.`SequentialAccess` を使用してバイナリ データまたは大きなデータ構造を取得し、 `DataReader` の既定の動作を変更する方法について説明します。'
ms.date: 12/04/2020
dev_langs:
- csharp
ms.assetid: 56c5a9e3-31f1-482f-bce0-ff1c41a658d0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 1033a6b5394d92a45cd19d70f4dd6c250ec37b62
ms.sourcegitcommit: 4419e99d77ee2c73f9da1559c7944f7702f2de30
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/23/2020
ms.locfileid: "97744432"
---
# <a name="retrieve-binary-data"></a>バイナリ データの取得

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

既定では、データの行全体が使用可能になるとすぐに、**DataReader** によって受信データが行として読み込まれます。 バイナリ ラージ オブジェクト (BLOB) には、1 行に収まらない数ギガバイトのデータが含まれる場合があるため、別の処理が必要です。 **Command.ExecuteReader** メソッドには、<xref:System.Data.CommandBehavior> 引数を受け取って **DataReader** の既定の動作を変更するオーバーロードがあります。 **ExecuteReader** メソッドに <xref:System.Data.CommandBehavior.SequentialAccess> を渡すと、データの行を読み込む代わりに、データを受け取った時点で順次読み込むように、**DataReader** の既定の動作を変更できます。 これは BLOB やその他の大きなデータ構造を読み込む場合に理想的な処理です。

> [!NOTE]
> **SequentialAccess** を使用するように **DataReader** を設定するときは、返されたフィールドにアクセスする順序に注意してください。 使用可能になるとすぐに行全体を読み込む **DataReader** の既定の動作では、次の行が読み取られるまでは、返されたフィールドに任意の順序でアクセスできます。 しかし、**SequentialAccess** を使用しているときは、**DataReader** によって返された各フィールドに順番にアクセスする必要があります。 たとえば、クエリが 3 つの列 (3 番目の列は BLOB) を返す場合、最初のフィールドおよび 2 番目のフィールドの値は、3 番目のフィールドの BLOB データにアクセスする前に返す必要があります。 最初のフィールドまたは 2 番目のフィールドの前に 3 番目のフィールドにアクセスした場合は、最初のフィールドと 2 番目のフィールドの値は使用できなくなります。 これは、**SequentialAccess** によって、**DataReader** はデータを順番に返すように変更されており、**DataReader** による読み取りが通過した後のデータは使用できなくなるためです。

BLOB フィールドのデータにアクセスするときは、**DataReader** の **GetBytes** 型または **GetChars** 型のアクセサーを使用します。これらのアクセサーでは、データは配列に設定されます。 文字データ用の **GetString** を使用することもできますが、システム リソースを節約するためには、BLOB 値全体を 1 つの文字列変数に読み込むことは望ましくありません。 特定のバッファー サイズのデータを返すように指定する代わりに、返されたデータから読み込む先頭バイトまたは先頭文字の開始位置を指定できます。 **GetBytes** と **GetChars** では、返されたバイト数または文字数を表す `long` 値が返されます。 **GetBytes** または **GetChars** に null 配列を渡した場合、返される long 値は BLOB の総バイト数または総文字数になります。 オプションで、データ読み込みの開始位置を示す、配列内のインデックスを指定できます。

## <a name="example"></a>例

次の例は、[**pubs** サンプル データベース](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)から発行者 ID とロゴを取得します。 発行者 ID (`pub_id`) は文字フィールドであり、ロゴはイメージ、つまり、BLOB です。 **logo** フィールドはビットマップなので、この例では、**GetBytes** を使用してバイナリ データを返します。 フィールドには順番にアクセスする必要があるため、現在の行のデータに対して発行者 ID はロゴの前にアクセスされることに注意してください。

[!code-csharp[SqlCommand_ExecuteReader_SequentialAccess#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteReader_SequentialAccess.cs#1)]

## <a name="see-also"></a>関連項目

- [SQL Server のバイナリ データと大きな値のデータ](./sql/sql-server-binary-large-value-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
