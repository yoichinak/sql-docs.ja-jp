---
description: XML でのレコードセットの動的プロパティ
title: XML | のレコードセットの動的プロパティMicrosoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e966c3570ce8f9589ede5f60fca1fc0fa70bbac
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037092"
---
# <a name="recordset-dynamic-properties-in-xml"></a>XML でのレコードセットの動的プロパティ
次のレコードセットプロバイダー固有のプロパティ (クライアントカーソルエンジンから) は現在、XML 形式で保存されています。  
  
-   再同期の更新  
  
-   Unique Table  
  
-   一意のスキーマ  
  
-   一意のカタログ  
  
-   再同期コマンド  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeOut  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   名前のリシェイプ  
  
-   AutoRecalc  
  
 これらのプロパティは、永続化されるレコードセットの要素定義の属性として、スキーマセクションに保存されます。 これらの属性は、行セットスキーマ名前空間で定義され、プレフィックス "rs:" を持つ必要があります。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
