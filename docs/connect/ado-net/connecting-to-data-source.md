---
title: データ ソースへの接続
description: ADO.NET のデータ ソースへの接続に使用される Connection オブジェクトについて説明します。 どの Connection オブジェクトを選択するかは、データ ソースの種類によって異なります。
ms.date: 11/13/2020
ms.assetid: 9abc3f92-1be3-4e1a-b360-762dc689650e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: ab6edc2a7090de85e970445cdb2b86d6ed5cb8f2
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126532"
---
# <a name="connecting-to-a-data-source-in-adonet"></a>ADO.NET のデータ ソースへの接続

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient データ プロバイダーでは、**Connection** オブジェクトを使用して、接続文字列に必要な認証情報を指定することにより、特定のデータ ソースに接続します。 どの **Connection** オブジェクトを使用するかは、データ ソースの種類によって異なります。

Microsoft SqlClient Data Provider for SQL Server には、<xref:System.Data.Common.DbConnection> クラスから派生した <xref:Microsoft.Data.SqlClient.SqlConnection> 型が含まれています。

## <a name="in-this-section"></a>このセクションの内容  

[接続の確立](establishing-connection.md)\
**Connection** オブジェクトを使用して、データ ソースとの接続を確立する方法について説明します。

[接続イベント](connection-events.md)\
**InfoMessage** イベントを使用してデータ ソースから情報メッセージを取得する方法について説明します。

## <a name="see-also"></a>関連項目

- [接続文字列](connection-strings.md)
- [接続プール](connection-pooling.md)
