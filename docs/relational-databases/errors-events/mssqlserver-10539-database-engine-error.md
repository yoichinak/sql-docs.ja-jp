---
description: MSSQLSERVER_10539
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9f1f36f5b8721a94b7badb3316f30f9b3d4e059d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338208"
---
# <a name="mssqlserver_10539"></a>MSSQLSERVER_10539
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|10539|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_NO_PLAN_FOR_STMT|  
|メッセージ テキスト|プラン ガイド '%.*ls' をキャッシュから作成できません。開始オフセット %d のステートメントのクエリ プランを使用できません。 この問題は、存在しないデータベース オブジェクトにステートメントが依存している場合に発生することがあります。 必要なデータベース オブジェクトがすべて存在することを確認し、プラン ガイドを作成する前にステートメントを実行します。|  
  
## <a name="explanation"></a>説明  
指定した開始オフセットを持つステートメントのクエリ プランがプラン キャッシュ内にありません。  
  
## <a name="user-action"></a>ユーザーの操作  
必要なデータベース オブジェクトがすべて存在することを確認し、プラン ガイドを作成する前にステートメントを実行します。  
  
## <a name="see-also"></a>参照  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
