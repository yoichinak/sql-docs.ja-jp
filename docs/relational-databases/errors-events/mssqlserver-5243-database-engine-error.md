---
description: MSSQLSERVER_5243
title: MSSQLSERVER_5243 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5243 (Database Engine error)
ms.assetid: e04a1934-e57d-420e-ac79-97071745824e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2575d81f09ccb3ac4aceb2396f5db0f8d9bee451
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471001"
---
# <a name="mssqlserver_5243"></a>MSSQLSERVER_5243
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|5243|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|内部操作中に一貫性が損なわれていることが検出されました。 テクニカル サポートにお問い合わせください。 参照番号 %ld。|  
  
## <a name="explanation"></a>説明  
メモリ内ストレージ エンジン構造の一貫性が損なわれていることが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により検出されました。  
  
## <a name="user-action"></a>ユーザーの操作  
ハードウェア障害を調査します。 ハードウェアの診断を実行し、問題があれば修正します。 また、Windows のシステム ログとアプリケーション ログ、および SQL Server エラー ログを調査し、ハードウェア障害の結果としてエラーが発生しているかどうかを確認します。 ログに記録されているハードウェア\-に関する問題があれば、それを修正します。

データ破損の問題が解決しない場合は、ハードウェア コンポーネントを他のものと交換し、問題の原因を特定するようにしてください。 システムで、ディスク コントローラーの書き込み\-キャッシュが有効になっていないことを確認します。 書き込み\-キャッシュが問題と思われる場合は、ハードウェア ベンダーにお問い合わせください。

それでも問題が解決しない場合は、新しいハードウェア システムの導入をご検討ください。 導入の際には、ディスク ドライブの再フォーマットとオペレーティング システムの再インストールが必要になる場合があります。

バックアップからの復元 問題がハードウェアに関するものではなく、また既知のクリーン バックアップがある場合は、そのバックアップを使用してデータベースを復元します。

DBCC CHECKDB の実行 クリーン バックアップがない場合には、REPAIR 句を付けずに DBCC CHECKDB を実行して破損の程度を調べます。 DBCC CHECKDB によって使用が推奨される REPAIR 句が表示されたら、 適切な REPAIR 句を付けて DBCC CHECKDB を実行し、破損を修復します。

> **アラート タグはサポートされていません!!!** 
> **tr タグはサポートされていません!!!** 
> **tr タグはサポートされていません!!!**

いずれかの REPAIR 句を付けて DBCC CHECKDB を実行しても問題が解決しない場合は、購入元にお問い合わせください。
  
## <a name="see-also"></a>参照  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[データベース ファイルとファイル グループ](~/relational-databases/databases/database-files-and-filegroups.md)  
  
