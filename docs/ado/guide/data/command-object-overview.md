---
description: Command オブジェクトの概要
title: Command オブジェクトの概要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
author: rothja
ms.author: jroth
ms.openlocfilehash: c23ce0b24fcd5fb82f306c1746f7a277bed293ed
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100033309"
---
# <a name="command-object-overview"></a>Command オブジェクトの概要
**Command** オブジェクトを使用すると、次の操作を実行できます。  
  
-   **CommandText** プロパティを使用して、コマンドの実行可能テキスト (SQL ステートメントやストアドプロシージャなど) を定義します。  
  
-   **パラメーター** オブジェクトと **Parameters** コレクションを使用して、パラメーター化クエリまたはストアドプロシージャの引数を定義します。  
  
-   **Execute** メソッドを使用して、コマンドを実行し、必要に応じて **レコードセット** オブジェクトを返します。  
  
-   実行前に **CommandType** プロパティを使用してコマンドの種類を指定し、パフォーマンスを最適化します。  
  
-   **Command オブジェクトの** **Dialect** プロパティを使用して、コマンドテキストに関する特定の情報を指定します。  
  
-   **準備されたプロパティを** 使用して、準備済み (またはコンパイル済み) のコマンドを実行前にプロバイダーが保存するかどうかを制御します。  
  
-   **CommandTimeout** プロパティを使用して、プロバイダーがコマンドの実行を待機する秒数を設定します。  
  
-   **ActiveConnection** プロパティを設定して、開いている接続を **Command** オブジェクトに関連付けます。  
  
-   **Name** プロパティを設定して、関連付けられている **接続** オブジェクトのメソッドとして **コマンド** オブジェクトを識別します。  
  
-   データを取得するために、**レコードセット** の **Source** プロパティに **Command** オブジェクトを渡します。  
  
-   コマンドを含む **ストリーム** オブジェクト (XML コマンドなど) を、それをサポートするプロバイダーに渡します。
