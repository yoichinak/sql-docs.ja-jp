---
description: ソリューション エクスプローラー
title: データ ソース | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b9f980ad9ccd1fa38b6fce863703ec706e21a76
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386058"
---
# <a name="data-sources"></a>ソリューション エクスプローラー
*データソース*は、単にデータのソースです。 ファイル、DBMS 上の特定のデータベース、またはライブデータフィードを使用できます。 データが、プログラムと同じコンピューター、またはネットワーク上の別のコンピューターに配置されている可能性があります。 たとえば、データソースは、Novell® Netware によってアクセスされる OS/2®オペレーティングシステムで実行されている Oracle DBMS である場合があります。ゲートウェイ経由でアクセスされる IBM DB2 DBMS。サーバーディレクトリ内の Xbase ファイルのコレクション。または、ローカルの Microsoft® Access データベースファイル。  
  
 データソースの目的は、データにアクセスするために必要なすべての技術情報 (ドライバー名、ネットワークアドレス、ネットワークソフトウェアなど) を1つの場所に収集し、ユーザーに対して非表示にすることです。 ユーザーは、給与、在庫、および担当者を含む一覧を確認し、一覧から Payroll を選択して、アプリケーションが給与データに接続できるようにする必要があります。この場合、給与データが存在する場所や、アプリケーションがどのように取得されたかわからなくなります。  
  
 *データソース*という用語は、同様の用語と混同しないようにしてください。 この手動では、 *DBMS* または *データベース* はデータベースプログラムまたはエンジンを参照します。 *デスクトップデータベース*間では、パーソナルコンピューター上で実行するように設計されていて、完全な sql とトランザクションのサポートや*サーバーデータベース*がないことがよくあります。これは、クライアント/サーバーの状況で実行するように設計され、スタンドアロンのデータベースエンジンと豊富な sql とトランザクションのサポートによって特徴付けられています。 また、*データベース*は、ディレクトリ内の Xbase ファイルのコレクションや SQL Server のデータベースなど、特定のデータのコレクションも指します。 これは、一般に、 *カタログ* として、このマニュアルの他の場所で使用されるか、以前のバージョンの ODBC では *修飾子* と呼ばれます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [データソースの種類](../../odbc/reference/types-of-data-sources.md)  
  
-   [データ ソースの使用](../../odbc/reference/using-data-sources.md)  
  
-   [データ ソースの例](../../odbc/reference/data-source-example.md)
