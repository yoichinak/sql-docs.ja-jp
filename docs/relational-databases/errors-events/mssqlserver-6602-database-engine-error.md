---
description: MSSQLSERVER_6602
title: MSSQLSERVER_6602
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 6602 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 594898082fb21f712cfb99abfb535aea46b5164d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100348718"
---
# <a name="mssqlserver_6602"></a>MSSQLSERVER_6602
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|6602|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|XMLERR_PARSEERR2|
|メッセージ テキスト|エラーの説明は '%.*ls' です。|
||

## <a name="explanation"></a>説明

このエラーは、`xmltext` パラメーターのコンテンツが複雑な XML ドキュメントである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で `sp_xml_preparedocument` ストアド プロシージャを実行しようとすると発生します。次のようなエラー メッセージがユーザーに報告されます。

> 行番号 1、XML テキスト "\<XML document sample>" 付近で、XML 解析エラー 0x80004005 が発生しました。  
メッセージ 6602、レベル 16、状態 2、プロシージャ sp_xml_preparedocument、行 1  
エラーの説明は '未指定のエラー' です。

## <a name="cause"></a>原因

この問題は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用される MSXML パーサー (Msxmlsql.dll) の設計上の制限のために発生します。

この問題は、XML ドキュメントのサイズは厳密には関与せず、その複雑な構造が関与します。 XML 要素の構造の深さ、属性の数とサイズ、属性内のエンティティの数の組み合わせによって、この問題が発生する可能性があります。 ただし、この制限に達するために必要な複雑さのレベルは、数メガバイトの XML ドキュメントに見られます。

## <a name="user-action"></a>ユーザー アクション

この問題を回避するには、XML ドキュメントの複雑さを減らすようにしてください。

> [!NOTE]
> 数多くの XML \ エンティティが含まれる単一の非常に大きな文字列属性に注意してください。
