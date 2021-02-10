---
description: データ移行レポート (OracleToSQL)
title: データ移行レポート (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d63aa7e2-62c6-4c84-b3da-dcf2d89ee134
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: cee9e42386aa76616e049261a4d1f5b6d965fe26
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100058677"
---
# <a name="data-migration-report--oracletosql"></a>データ移行レポート (OracleToSQL)
[ **データ移行レポート** ] ダイアログボックスは、にデータを移行した後に表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="options"></a>Options  
**状態**  
転送元データベースから転送先データベースへのデータ移行の状態が表示されます。  
  
**From**  
ソーステーブルです。  
  
**To**  
対象のテーブル。  
  
**行の合計数**  
ソーステーブル内のデータ行の数。  
  
**正常に移行された行の数**  
ターゲットテーブルに正常に移行されたデータの行の数。  
  
**比率**  
正常に移行された行の割合。  
  
**詳細**  
データの移行に失敗した場合は、クリックすると、レポート内の選択した行の移行の詳細が表示されます。 SSMA には、エラーの理由が表示されます。  
  
**レポートの保存**  
レポートをに保存します。CSV (コンマ区切り値) ファイル。 Microsoft Excel を使用して調べることができます。  
  
