---
description: ODBC と標準の CLI
title: ODBC と標準 CLI |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 844ca219bf912421cf859e0fc459b78d755fe159
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487385"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC と標準の CLI
ODBC は、呼び出しレベルのインターフェイス (CLI) を処理する次の仕様と標準に沿っています。 (ODBC 機能は、これらの各標準のスーパーセットです)。  
  
-   Open Group CAE Specification "データ管理: SQL 呼び出しレベルインターフェイス (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) 呼び出しレベルインターフェイス (SQL/CLI)  
  
 この配置の結果、次のようになります。  
  
-   Open Group および ISO CLI 仕様に書き込まれるアプリケーションは、odbc *3.x ドライバーまた* は標準に準拠しているドライバーを使用してコンパイルされ、odbc *3. x ヘッダーファイル* を使用してコンパイルされ、odbc *3* . x ライブラリにリンクされている場合は *、odbc 3.x ドライバーマネージャー* を使用してドライバーへのアクセスを取得します。  
  
-   Open Group および ISO CLI 仕様に書き込まれるドライバーは *、odbc 3.x アプリケーションまた* は標準に準拠しているアプリケーションで動作します。 odbc *3. x ヘッダーファイル* を使用してコンパイルし、odbc *3* . x ライブラリにリンクし、アプリケーションが odbc *3. x* ドライバーマネージャーを使用してドライバーへのアクセスを取得したときに使用します。 (詳細については、「 [標準に準拠したアプリケーションとドライバー](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)」を参照してください。  
  
 コアインターフェイスの準拠レベルには、ISO CLI のすべての機能と、Open Group CLI のオプション以外のすべての機能が含まれています。 Open Group CLI のオプション機能は、より高いインターフェイス準拠レベルで表示されます。 コアインターフェイスの準拠レベルの機能をサポートするには、すべて *の ODBC 3.x* ドライバーが必要であるため、次のことが当てはまります。  
  
-   ODBC 3.x ドライバーでは、標準に準拠しているアプリケーションで使用されるすべての機能がサポートされ*ます。*  
  
-   ISO CLI の機能だけを使用する ODBC 3.x アプリケーションと、Open Group CLI の非オプション機能は、標準に準拠しているドライバーで動作*します。*  
  
 ODBC では、ISO/IEC および Open Group CLI 標準に含まれる呼び出しレベルのインターフェイスの仕様に加えて、次の機能が実装されています。 (これらの機能の一部は、odbc 3.x より前のバージョンの ODBC でも *存在して*いました)。  
  
-   単一の関数呼び出しによる複数行のフェッチ  
  
-   パラメーターの配列へのバインド  
  
-   ブックマークによるフェッチ、可変長のブックマーク、および連続していない行に対するブックマーク操作による一括更新と delete を含むブックマークサポート  
  
-   行方向のバインド  
  
-   バインド (オフセットを)  
  
-   ストアドプロシージャ内または**Sqlexecute**または**SQLExecDirect**を使用して実行される sql ステートメントのシーケンスとしての sql ステートメントのバッチのサポート  
  
-   正確または概数のカーソルの行数  
  
-   関数呼び出し (**SQLSetPos**) による更新および削除操作の位置指定とバッチ更新と削除  
  
-   情報スキーマビューをサポートせずに情報スキーマから情報を抽出するカタログ関数  
  
-   外部結合、スカラー関数、datetime リテラル、間隔リテラル、およびストアドプロシージャのエスケープシーケンス  
  
-   コードページ変換ライブラリ  
  
-   ドライバーの ANSI 準拠レベルと SQL サポートのレポート  
  
-   実装パラメーター記述子のオンデマンド自動作成  
  
-   強化された診断と行とパラメーターの状態の配列  
  
-   Datetime、interval、numeric/decimal、および64ビット整数のアプリケーションバッファーの種類  
  
-   非同期実行  
  
-   ストアドプロシージャのサポート (エスケープシーケンス、出力パラメーターのバインディング機構、カタログ関数など)  
  
-   接続属性と属性の参照のサポートを含む接続の機能強化
