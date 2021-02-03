---
description: MSSQLSERVER_1101
title: MSSQLSERVER_1101 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4927e306ff355413dd81c72420a760102ea1043f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197216"
---
# <a name="mssqlserver_1101"></a>MSSQLSERVER_1101
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|1101|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|NOALLOCPG|  
|メッセージ テキスト|データベース '%.*ls' の新しいページを割り当てられませんでした。ファイル グループ '%.\*ls' のディスク領域が不足しています。 ファイル グループ内のオブジェクトの削除、ファイル グループへの新しいファイルの追加、またはファイル グループの既存のファイルの自動拡張の設定のいずれかを行って、必要な領域を作成してください。|  
  
## <a name="explanation"></a>説明  
ファイル グループでディスク領域が不足しています。  
  
## <a name="user-action"></a>ユーザーの操作  
次の操作により、ファイル グループで領域を使用できるようになることがあります。  
  
-   AUTOGROW をオンにする。  
  
-   ファイル グループにファイルをさらに追加する。  
  
-   ファイル グループ内の不要なインデックスやテーブルを削除することにより、ディスク領域を解放する。  
  
