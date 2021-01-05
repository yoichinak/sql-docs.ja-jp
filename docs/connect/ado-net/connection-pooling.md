---
title: 接続のプール
description: データ ソースへの接続を開くコストを最小限にするために ADO.NET で使用される、接続プールと呼ばれる最適化の手法について説明します。
ms.date: 11/13/2020
ms.assetid: 955c057f-aea8-4ba8-aa6d-e3dfa18ba8d5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 783fad79522c52685349defca93360c4ea8c80c9
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771647"
---
# <a name="connection-pooling"></a>接続のプール

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

データ ソースへの接続は時間のかかる処理です。 接続を開くコストを最小限にするため、ADO.NET では、"*接続プール*" と呼ばれる最適化の手法が使われています。接続プールを使うことで、接続を開いて閉じるという処理の繰り返しによって生じるコストを、最小限に抑えることができます。

## <a name="in-this-section"></a>このセクションの内容  

[SQL Server の接続プール (ADO.NET)](sql-server-connection-pooling.md)  
接続プールの概要および SQL Server における接続プールの動作を説明します。

## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得と変更](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
