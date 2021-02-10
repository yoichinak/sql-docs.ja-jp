---
description: データ プロバイダー
title: データプロバイダー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: rothja
ms.author: jroth
ms.openlocfilehash: 67abe2bd8d2af4e43b1f6d14aed6588b9ddd7a2e
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100033308"
---
# <a name="data-providers"></a>データ プロバイダー
データプロバイダーは、SQL データベース、インデックス付きシーケンシャルファイル、スプレッドシート、ドキュメントストア、メールファイルなど、さまざまなデータソースを表します。 プロバイダーは、行セットと呼ばれる共通の抽象化を使用して、一様にデータを公開します。  
  
 ADO は、さまざまなデータプロバイダーのいずれかに接続でき、特定のプロバイダーの特定の機能に関係なく同じプログラミングモデルを公開できるため、強力で柔軟性があります。 ただし、各データプロバイダーは一意であるため、アプリケーションと ADO の対話方法はデータプロバイダーによって異なります。  
  
 たとえば、Microsoft SQL Server データベースへのアクセスに使用される、SQL Server の OLE DB プロバイダーの機能は、Web サーバー上のファイルストアにアクセスするために使用される Microsoft OLE DB Provider for Internet Publishing とは大きく異なります。
