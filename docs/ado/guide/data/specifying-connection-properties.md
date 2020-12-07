---
description: 接続プロパティの指定
title: 接続プロパティの指定 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c4d3a70388415402db3ecf8bdb21bd717a66aa6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979563"
---
# <a name="specifying-connection-properties"></a>接続プロパティの指定
接続 [文字列](../../../ado/guide/data/creating-a-connection-string.md) によって指定された情報の大部分は、接続を開く前に **接続** オブジェクトのプロパティを設定することによって指定できます。 たとえば、次のコードを使用した [接続文字列の作成](../../../ado/guide/data/creating-a-connection-string.md) に関するセクションで説明した接続文字列と同じ効果を得ることができます。  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase は、接続を開いた後にのみ設定されます。  
  
> [!NOTE]
>  ADO では、パスワードが単一引用符で囲まれている場合を除き、セミコロン (";") を含むパスワードは使用しないでください。
