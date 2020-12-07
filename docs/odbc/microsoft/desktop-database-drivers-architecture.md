---
description: デスクトップ データベース ドライバーのアーキテクチャ
title: デスクトップデータベースドライバーのアーキテクチャ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d330392424b683e24f17bd959d0a29e76eedbd36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449574"
---
# <a name="desktop-database-drivers-architecture"></a>デスクトップ データベース ドライバーのアーキテクチャ
これらのドライバーは、Microsoft Windows 95 以降、または Windows NT 4.0 と Windows 2000 で使用するように設計されています。 Windows 95 以降では、32ビットアプリケーションのみがサポートされています。16ビットおよび32ビットのアプリケーションは、Windows NT 4.0 と Windows 2000 でサポートされています。  
  
> [!NOTE]  
>  これらのドライバーで使用する ODBC のバージョンの詳細については、 *Odbc プログラマーズリファレンス*、および過去と現行のリリースノートを参照してください。 記載されている領域を除き、これらのドライバーは *ODBC プログラマーズリファレンス*に準拠しています。  
  
 ODBC デスクトップデータベースドライバーには、Microsoft Access、dBASE、Microsoft Excel、Paradox、およびテキスト用の32ビットドライバーが含まれています。 16ビットドライバーは含まれません。 (Microsoft FoxPro 用ドライバーは別途提供されています。)  
  
 Windows 95 以降のアプリケーション/ドライバーアーキテクチャは次のとおりです。  
  
 ![アプリ&#47;ドライバーのアーキテクチャ: Windows 95 以降](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Windows 95 では、16ビットアプリケーションによるこれらのドライバーの使用はサポートされていません。  
  
 Windows NT 4.0 および Windows 2000 のアプリケーション/ドライバーアーキテクチャは次のとおりです。  
  
 ![アプリ&#47;ドライバーのアーキテクチャ: NT 4.0 および Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 デスクトップデータベースドライバーは2層ドライバーです。 2層構成では、ドライバーはクエリの解析、検証、最適化、および実行のプロセスを実行しません。 代わりに、Microsoft Jet はこれらのタスクを実行します。 ODBC API 呼び出しを処理し、SQL エンジンとして機能します。 Microsoft Jet は、ドライバーの一部ではなく、コンピューター上の他のアプリケーションがそれを使用していない場合でも、ドライバーに付属しており、ドライバーと共に存在します。  
  
 デスクトップデータベースドライバーは、6つの異なるドライバー (または、より正確には、ODBC [ドライバーマネージャー](../../odbc/reference/the-driver-manager.md) が6つの異なる方法で使用するドライバーファイル (Odbcjt32.dll) で構成されます。 データソースのレジストリエントリにある DRIVERID フラグによって、ドライバーマネージャーが使用 Odbcjt32.dll ドライバーが決まります。 アプリケーションは、 **SQLDriverConnect**の呼び出しに含まれる接続文字列にこのフラグを渡します。 既定では、フラグは Microsoft Access ドライバーの ID です。  
  
 ドライバーセットアップファイルは、セットアップ時に DRIVERID フラグを変更します。 Microsoft Access ドライバー以外のすべてのドライバーには、セットアップ DLL が関連付けられています。 データソースの[MICROSOFT Odbc データソースアドミニストレーター](../../odbc/admin/odbc-data-source-administrator.md)で [**セットアップ**] をクリックすると、odbc インストーラー dll (Odbcinst.dll) によってセットアップ dll が読み込まれます。 セットアップ DLL により、ODBC インストーラー関数 **Sqlconfigdatasource**がエクスポートされます。 ウィンドウハンドルが **Sqlconfigdatasource**に渡されると、この関数はセットアップウィンドウを表示し、ユーザーインターフェイスから選択されたドライバーに従って driverid フラグを変更します。  
  
 プログラムによってファイルが作成されると、 **Sqlconfigdatasource**に NULL ウィンドウハンドルが渡されます。この関数は、関数呼び出しの *lpszdriver* 引数に従って driverid フラグを変更して、データソースを動的に作成します。  
  
 Odbcjt32.dll は、Microsoft Jet API 上に ODBC 関数を実装します。 ただし、ODBC と Microsoft Jet の関数の間に直接のマッピングはありません。 カーソルモデルや SQL マッピングなどの多くの要因により、関数を直接相関させることができません。  
  
 ODBC ドライバーは、Microsoft Jet エンジンと ODBC ドライバーマネージャーの間に存在します。 アプリケーションによって呼び出される一部の ODBC 関数は、ドライバーマネージャーによって処理され、ドライバーに渡されません。 これらの関数では、ドライバーマネージャーに直接接続されていないため、Microsoft Jet は関数呼び出しを認識しません。
