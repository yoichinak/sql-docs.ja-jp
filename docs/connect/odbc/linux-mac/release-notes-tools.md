---
title: Linux および macOS の mssql-tools のリリース ノート
description: Microsoft SQL Server ツールのリリース済みバージョンにおける新機能と変更内容について説明します。
ms.custom: ''
ms.date: 01/29/2021
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-daenge
ms.technology: connectivity
ms.topic: conceptual
author: v-zhangw
ms.author: v-zhangw
manager: kenvh
ms.openlocfilehash: 75f1144e84792b3c9361dcab74dcdbcb7b072268
ms.sourcegitcommit: f30b5f61c514437ea58acc5769359c33255b85b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2021
ms.locfileid: "99075924"
---
# <a name="release-notes-for-the-microsoft-sql-server-tools-on-linux-and-macos"></a>Linux および macOS の Microsoft SQL Server ツールのリリース ノート

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

この記事では、Linux および macOS の [!INCLUDE[msCoName](../../../includes/msconame_md.md)] SQL Server ツールのバージョン管理されたリリースの新機能を一覧で説明します。

## <a name="17711-january-2021"></a>17.7.1.1 - 2021 年 1 月

| 追加された機能 | 詳細 |
| :------------ | :------ |
| Sqlcmd バグ修正 | 実行の繰り返しを引き起こす、入力リダイレクトのバグと空の行を修正しました。 |
| Sqlcmd バグ修正 | 特定の書式設定で r、p、X、k オプションについて間違ったエラーが報告される現象を解消しました。 |
| Sqlcmd -z/-Z "Password" オプション | サポートされるようになりました。 |
| &nbsp; | &nbsp; |

## <a name="17611-july-2020"></a>17.6.1.1、2020 年 7 月

| 追加された機能 | 詳細 |
| :------------ | :------ |
| Sqlcmd コマンド ライン パーサーが更新されました | 特定のオプションの使用順序が異なると予期しない動作が発生するバグを修正しました。 |
| Sqlcmd エラー メッセージが更新されました | sqlcmd でエラーが返されるときのさまざまな不整合を修正しました。 |
| Sqlcmd -Y オプションを修正しました | -Y オプションが無効になる問題を修正しました |
| Sqlcmd 列名の切り捨てを修正しました | 列名が誤って切り捨てられる問題を修正しました |
| Sqlcmd Linux 終了コード | Linux でプロセス終了コードが見つからない問題を修正しました |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>次のステップ

[BCP](connecting-with-bcp.md) と [SQLCMD](connecting-with-sqlcmd.md) による接続について学習してください。
