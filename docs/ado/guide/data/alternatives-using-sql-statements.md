---
description: '代替: SQL ステートメントの使用'
title: '代替手段: SQL ステートメントの使用 |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
author: rothja
ms.author: jroth
ms.openlocfilehash: 91111602587b7857559a633a816d7fbb6b125dcb
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100028056"
---
# <a name="alternatives-using-sql-statements"></a>代替: SQL ステートメントの使用
ADO では、データを編集するための組み込みプロパティやメソッドの代わりにコマンドを使用することもできます。 プロバイダーによっては、このセクションに記載されているすべての操作を、データソースにコマンドを渡すことによって実現することもできます。 たとえば、SQL UPDATE ステートメントを使用して、**フィールド** の **Value** プロパティを使用せずにデータを変更できます。 SQL INSERT ステートメントは、ADO メソッド **AddNew** ではなく、データソースに新しいレコードを追加するために使用できます。 プロバイダーの SQL またはデータ操作言語の詳細については、データソースのドキュメントを参照してください。  
  
 たとえば、次のコードに示すように、DELETE ステートメントを含む SQL 文字列をデータベースに渡すことができます。  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
