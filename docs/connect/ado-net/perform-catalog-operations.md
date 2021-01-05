---
title: カタログ操作の実行
description: データベース スキーマを変更するコマンドを実行する方法について説明します。
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: e60f542f-6271-495b-a9e4-48553481c2a3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 79eef694b3c6294eb12630f27c4b3688823581c7
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771553"
---
# <a name="performing-catalog-operations"></a>カタログ操作の実行

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

データベースまたはカタログを変更するコマンド (CREATE TABLE ステートメント、CREATE PROCEDURE ステートメントなど) を実行するには、適切な SQL ステートメントと **Connection** オブジェクトを使用して、**Command** オブジェクトを作成します。 <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> メソッドでコマンドを実行します。

## <a name="example"></a>例

Microsoft SQL Server データベースにストアド プロシージャを作成するコード サンプルを次に示します。

[!code-csharp[DataWorks SqlCommand.ExecuteNonQuery#3](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery_SP_DML.cs#3)]

## <a name="see-also"></a>関連項目

- [コマンドを使用したデータ変更](use-commands-to-modify-data.md)
- [コマンドとパラメーター](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
