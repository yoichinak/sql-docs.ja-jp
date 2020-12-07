---
description: 準備とコマンドの実行
title: コマンドの準備と実行 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a4265124c2f86870d84ee703d228d5a760c4735
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979993"
---
# <a name="preparing-and-executing-commands"></a>準備とコマンドの実行
コマンドは、基になるデータソースに対して何らかの操作を実行するためにプロバイダーに発行される命令です。 たとえば、SQL ステートメントは Microsoft SQL Data Provider のコマンドです。 ADO では、コマンドは通常、 **コマンド** オブジェクトによって表されますが、 **接続** または **レコードセット** オブジェクトを使用して簡単なコマンドを発行することもできます。  
  
 **コマンド**オブジェクトを使用して、プロバイダーがコマンド文字列を正しく解釈できると仮定して、サポートされている任意の種類の操作をプロバイダーから要求できます。 データプロバイダーの一般的な操作では、データベースに対してクエリを実行し、レコード **セット** オブジェクトのレコードを返します。これは、結果を保持するコンテナーと考えることができ、結果を表示するためのツールです。 多くの ADO オブジェクトと同様に、 **コマンド** オブジェクトのコレクション、メソッド、またはプロパティによっては、プロバイダーの機能に応じて、参照時にエラーが発生することがあります。  
  
 **Command**オブジェクトを使用するだけでなく、 **Connection**オブジェクトの**Execute**メソッド、または**Recordset**オブジェクトの**Open**メソッドを使用して、コマンドを発行し、実行することもできます。 ただし、コードでコマンドを再利用する必要がある場合や、コマンドで詳細なパラメーター情報を渡す必要がある場合は、 **command** オブジェクトを使用する必要があります。 これらのシナリオについては、このセクションの後半で詳しく説明します。  
  
> [!NOTE]
>  特定の**コマンド**では、プロバイダーでサポートされている場合、バイナリストリームとして、またはレコード**セット**としてではなく1つの**レコード**として結果セットを返すことができます。 また、一部の **コマンド**は、結果セットを返さないようにするためのものではありません (たとえば、SQL Update クエリ)。 ここでは、最も一般的なシナリオについて説明します。ただし、結果を**レコードセット**オブジェクトとして返す**コマンド**を実行します。 結果を **Record**s または **Stream**s に返す方法の詳細については、「 [レコードとストリーム](../../../ado/guide/data/records-and-streams.md)」を参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Command オブジェクトの概要](../../../ado/guide/data/command-object-overview.md)  
  
-   [簡単なコマンドの作成と実行](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command オブジェクトのパラメーター](../../../ado/guide/data/command-object-parameters.md)  
  
-   [Command を使用してストアド プロシージャを呼び出す](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [接続オブジェクトのメソッドとしてのストアドプロシージャの呼び出し](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [名前付きコマンド](../../../ado/guide/data/named-commands.md)  
  
-   [名前付きコマンドにパラメーターを渡す](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
