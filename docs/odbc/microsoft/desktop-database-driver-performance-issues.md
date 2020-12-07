---
description: デスクトップ データベース ドライバー パフォーマンスの問題
title: デスクトップデータベースドライバーのパフォーマンスに関する問題 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20c21c493d81df6afb4a338675f86ad96ccfab68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449554"
---
# <a name="desktop-database-driver-performance-issues"></a>デスクトップ データベース ドライバー パフォーマンスの問題
既存の ANSI アプリケーションとの互換性を確保するために、SQL_WCHAR、SQL_WVARCHAR、および SQL_WLONGVARCHAR のデータ型は、Microsoft Access 4.0 以降のデータソースの SQL_CHAR、SQL_VARCHAR、および SQL_LONGVARCHAR として公開されています。 データソースはワイド文字データ型を返しませんが、データはワイド Char 形式で Jet に送信される必要があります。 SQL_C_CHAR パラメーターまたは結果列が ANSI アプリケーションの SQL_CHAR データ型にバインドされている場合は、変換が行われることを理解しておくことが重要です。  
  
 SQL_C_CHAR 型が LONGVARCHAR 型のパラメーターにバインドされている場合、この変換はメモリの観点から特に非効率的です。 Jet 4.0 エンジンは LONGTEXT パラメーターのデータをストリームできないため、SQL_C_CHAR ANSI バッファーの2倍のサイズの UNICODE 変換バッファーを割り当てる必要があります。 最も効率的なメカニズムは、アプリケーションが UNICODE 変換を実行し、パラメーターを SQL_C_WCHAR 型としてバインドすることです。 パラメーターが実行時データとしてマークされていて、データが SQLPutData の複数の呼び出しで提供されている場合、longtext データバッファーが拡張されます。 この "Put Data" バッファーが大きくなるのを防ぐ方法の1つとして、SQL_DATA_AT_EXEC_LEN (x) を使用してオプションの長さを指定する方法があります。 *x* は想定されているバイト長です。 これにより、内部の PutData バッファーのサイズが *x* バイトに初期化されます。  
  
> [!NOTE]  
>  長いデータを挿入または更新する効率的な方法は、 **Sqlbulkoperations ()** または **SQLSetPos ()** を使用して、長いデータを SQL_DATA_AT_EXEC に設定することです。 (この場合、EXEC_LEN は無視されます)。データをチャンク単位でストリーム配信するには、 **Sqlputdata** を複数回呼び出します。これにより、データが実質的にテーブルに追加されます。  
  
 Microsoft ODBC Desktop データベースドライバを介して Jet 3.5 データベースを使用しているアプリケーションをバージョン4.0 にアップグレードすると、パフォーマンスが低下し、ワーキングセットサイズが増加する可能性があります。 これは、バージョン3の場合に行われます。*x* データベースは、新しいバージョン4.0 ドライバーを使用して開かれ、Jet 4.0 を読み込みます。 Jet 4.0 がデータベースを開いたときに、データベースが3であることを確認します。*x* バージョンでは、インストール可能な ISAM ドライバーも読み込まれます。これは、Jet 3.5 エンジンの読み込みに相当します。 パフォーマンスとサイズのペナルティを削除するには、Jet 3 を行います。*x* データベースは、Jet 4.0 形式のデータベースに圧縮する必要があります。 これにより、2つの Jet エンジンが読み込まれなくなり、データへのコードパスが最小化されます。  
  
 また、Jet 4.0 エンジンは Unicode エンジンです。 すべての文字列は、Unicode で格納および操作されます。 ANSI アプリケーションが Jet 3 にアクセスする場合。*x* データベース Jet 4.0 エンジンを使用して、データを Ansi から Unicode に変換し、ansi に戻します。 データベースがバージョン4.0 形式に更新された場合、文字列は Unicode に変換され、1レベルの文字列変換が削除されるだけでなく、1つの Jet エンジンのみを通過することによってデータへのコードパスが最小化されます。
