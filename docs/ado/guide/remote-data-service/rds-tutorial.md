---
description: RDS チュートリアル
title: RDS チュートリアル |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: rothja
ms.author: jroth
ms.openlocfilehash: 70f91e85010abb784291c3c9eca52b9a74ed6286
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721393"
---
# <a name="rds-tutorial"></a>RDS チュートリアル
このチュートリアルでは、RDS プログラミングモデルを使用してデータソースを照会および更新する方法について説明します。 まず、このタスクを実行するために必要な手順について説明します。 このチュートリアルは、Microsoft® Visual Basic Scripting Edition (Windows Foundation クラス (ADO/WFC) 用の ADO を使用) で繰り返されています。  
  
 このチュートリアルは、次の2つの理由で異なる言語でコーディングされています。  
  
-   RDS のドキュメントでは、Visual Basic のリーダーコードを前提としています。 これにより、Visual Basic プログラマーにとって便利なドキュメントになりますが、他の言語を使用するプログラマにとってはあまり役に立ちません。  
  
-   特定の RDS 機能が不明で、別の言語が少しわからない場合は、別の言語で表現された同じ機能を検索することで、質問を解決できる可能性があります。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="how-the-tutorial-is-presented"></a>チュートリアルの表示方法  
 このチュートリアルは、RDS プログラミングモデルに基づいています。 プログラミングモデルの各ステップについて個別に説明します。 また、Visual Basic コードのフラグメントを使用した各手順についても説明します。  
  
 このコード例は、他の言語では最小限の説明で繰り返されています。 特定のプログラミング言語のチュートリアルの各手順は、プログラミングモデルと説明のチュートリアルの対応する手順でマークされています。 手順の番号を使用して、説明用のチュートリアルの説明を参照してください。  
  
 RDS プログラミングモデルについては、次のセクションで説明します。 このチュートリアルを進めながら、ロードマップとして使用してください。  
  
## <a name="rds-programming-model-with-objects"></a>RDS のプログラミング モデルとオブジェクト  
  
-   サーバーで呼び出されるプログラムを指定し、クライアントから参照する方法 (プロキシ) を取得します。  
  
-   サーバープログラムを起動します。 データソースと発行するコマンドを識別するパラメーターをサーバープログラムに渡します。  
  
-   サーバープログラムは、通常は ADO を使用して、データソースから [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトを取得します。 必要に応じて、 **レコードセット** オブジェクトがサーバー上で処理されます。  
  
-   サーバープログラムによって、最終的な **レコードセット** オブジェクトがクライアントアプリケーションに返されます。  
  
-   クライアントでは、必要に応じて、 **レコードセット** オブジェクトを、ビジュアルコントロールで簡単に使用できる形式にすることができます。  
  
-   **Recordset**オブジェクトへの変更は、サーバーに返され、データソースの更新に使用されます。  
  
 このチュートリアルには、次のトピックが含まれています。  
  
-   [手順 1:サーバー プログラムを指定する (RDS チュートリアル)](./step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [手順 2:サーバー プログラムを呼び出す (RDS チュートリアル)](./step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [手順 3:サーバーがレコード セットを取得する (RDS チュートリアル)](./step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [手順 4:サーバーがレコード セットを返す (RDS チュートリアル)](./step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [手順 5:DataControl が使用可能になる (RDS チュートリアル)](./step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [手順 6:変更がサーバーに送信される (RDS チュートリアル)](./step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS のチュートリアル (VBScript)](./rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>参照  
 [手順 1: サーバープログラムを指定する (RDS チュートリアル)](./step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS のチュートリアル (VBScript)](./rds-tutorial-vbscript.md)