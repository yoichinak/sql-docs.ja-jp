---
description: デスクトップ データベース ドライバーの履歴
title: デスクトップデータベースドライバーの履歴 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80e8f1b52abac92ba09b97d35d45dfe0506963ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500325"
---
# <a name="history-of-the-desktop-database-drivers"></a>デスクトップ データベース ドライバーの履歴
次の表は、デスクトップデータベースドライバーのバージョン履歴を示しています。  
  
|Version|リリース日|説明|  
|-------------|------------------|-----------------|  
|1.0|1993年8月|PageAhead ソフトウェアによって生成された SIMBA クエリプロセッサを使用しました。 SIMBA は、ODBC 呼び出しと SQL ステートメントを受信し、それらを Microsoft Jet インストール可能な ISAM 呼び出しに処理した後、Microsoft Jet ISAM ディスパッチレイヤーを呼び出して適切なインストール可能な ISAM ドライバーを読み込んで呼び出します。|  
|2.0|1994年12月|Odbc 2.0 で使用します。 ODBC の機能が大幅に拡張されています。 バージョン2.0 の主な変更は、Microsoft Jet データベースエンジンによって SIMBA クエリプロセッサが置き換えられたことでした。 Microsoft Jet データベースエンジンを使用すると、デスクトップデータベースドライバーは、Microsoft Jet のインストール可能な ISAM ドライバーおよび Microsoft Access テクノロジと密接に統合されています。 大幅な機能強化は次のとおりです。<br /><br /> -スクロール可能なカーソルのネイティブサポート。<br />-外部結合、更新可能な異種結合、およびトランザクションのネイティブサポート。<br />-32-Microsoft Windows NT 用ドライバーのビット版。|  
|3.0|1995年10月|Windows 95 および Windows NT Workstation または NT Server 3.51 がサポートされています。 このリリースには、32ビットのドライバーのみが含まれていました。Windows バージョン3.1 用の16ビットドライバーが削除されました。|  
|3.5|1996年10月|これらのドライバーは2バイト文字セット (DBCS) を有効にしたものであり、以前のバージョンよりもインターネットアプリケーションでの使用に適していました。また、ファイルデータソース名 (Dsn) の使用に適していました。 Microsoft Access ドライバーは、Windows 95/98 および Windows NT 3.51 以降のオペレーティングシステムで Alpha プラットフォームで使用するために、RISC バージョンでリリースされました。|  
|4.0|遅延1998|では、以前のバージョンの ANSI 形式との互換性に加えて、Microsoft Jet Engine Unicode 形式がサポートされています。|  
  
> [!NOTE]  
>  バージョン3.5 のドライバーは、ODBC2 で動作するように設計されています。*x*。 ODBC 3.0 でも使用できますが、ODBC 3.0 のすべての機能をサポートしているわけではありません。 これらのドライバーが ODBC 3.0 で動作する方法の詳細については、「 [旧バージョンとの互換性と標準の準拠](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)」を参照してください。
