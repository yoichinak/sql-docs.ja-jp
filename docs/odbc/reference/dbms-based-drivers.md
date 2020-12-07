---
description: DBMS ベースのドライバー
title: DBMS ベースのドライバー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 844c25ca32bdf302312df6d23ca8e1d85fe198c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476914"
---
# <a name="dbms-based-drivers"></a>DBMS ベースのドライバー
DBMS ベースのドライバーは、ドライバーが使用するスタンドアロンデータベースエンジンを提供する Oracle や SQL Server などのデータソースと共に使用されます。 これらのドライバーは、スタンドアロンエンジンを使用して物理データにアクセスします。つまり、エンジンに対して SQL ステートメントを送信し、結果を取得します。  
  
 DBMS ベースのドライバーは既存のデータベースエンジンを使用するため、通常はファイルベースのドライバーよりも書き込みが簡単です。 DBMS ベースのドライバーは、ODBC 呼び出しをネイティブ API 呼び出しに変換することによって簡単に実装できますが、その結果、ドライバーが低速になります。 DBMS ベースのドライバーを実装する方法としては、基になるデータストリームプロトコルを使用することをお勧めします。通常は、ネイティブ API の機能です。 たとえば、SQL Server ドライバーでは、DB ライブラリ (SQL Server のネイティブ API) ではなく、TDS (SQL Server のデータストリームプロトコル) を使用する必要があります。 このルールの例外は、ODBC がネイティブ API である場合です。 たとえば、Watcom SQL は、アプリケーションと同じコンピューター上に存在し、ドライバーとして直接読み込まれるスタンドアロンエンジンです。  
  
 DBMS ベースのドライバーは、データソースがサーバーとして機能するクライアント/サーバー構成のクライアントとして機能します。 ほとんどの場合、クライアント (ドライバー) とサーバー (データソース) は異なるコンピューター上に存在しますが、マルチタスクオペレーティングシステムを実行しているコンピューター上に存在することもあります。 3番目の可能性は、ドライバーとデータソースの間にある *ゲートウェイ* です。 ゲートウェイとは、ある DBMS を別の DBMS のように表示するソフトウェアのことです。 たとえば、SQL Server を使用するように記述されたアプリケーションは、マイクロ Decisionware DB2 ゲートウェイを介して DB2 データにアクセスすることもできます。この製品を使うと、DB2 は SQL Server のようになります。  
  
 次の図は、DBMS ベースのドライバーの3つの異なる構成を示しています。 最初の構成では、ドライバーとデータソースは同じコンピューター上に存在します。 2つ目の方法では、ドライバーとデータソースが異なるコンピューター上に存在します。 3番目の方法では、ドライバーとデータソースは異なるコンピューター上に存在し、ゲートウェイは、別のコンピューター上に存在しています。  
  
 ![DBMS&#45;ベースのドライバーの3つの構成](../../odbc/reference/media/pr07.gif "pr07")
