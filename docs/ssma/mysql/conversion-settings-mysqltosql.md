---
description: 変換の設定 (MySQLToSQL)
title: 変換の設定 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1652913173dcd7427515db8c74d15afc75077820
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988638"
---
# <a name="conversion-settings-mysqltosql"></a>変換の設定 (MySQLToSQL)
[ **設定** ] タブでは、ユーザーはノードレベルの設定を設定できます。 このタブは、次のメタベースノードで使用できます。  
  
-   データベースノード  
  
-   Functions カテゴリ  
  
-   Function ノード  
  
-   テーブルカテゴリ  
  
-   テーブルノード  
  
## <a name="specifications"></a>仕様  
[ **設定** ] タブには、可視化という2つのユーザー設定があります。  
  
1.  関数の変換  
  
2.  テーブルの変換  
  
これらの設定は、メタベースノードの種類に基づいて使用できます。 たとえば、関数の変換に関連する設定は、テーブルノードでは使用できません。  
  
> [!NOTE]  
> -   ユーザーによって行われた変更は、プロジェクトワークスペースに個別の基本設定ファイルとして保存されます。  
> -   このファイルの拡張子は **ccprefs**使用します。  
  
1.  **関数の変換の設定:**  
  
    1.  このタブには、 **[関数の強制変換** ] オプションが含まれています。 オプションには、次の4つの値のいずれかを指定できます。  
  
        -   プロジェクト設定に従って変換する [継承]  
  
        -   常に関数に変換する  
  
        -   常にプロシージャに変換する  
  
        -   プロジェクト設定に従って変換する  
  
    2.  設定に基づいて、関数は関数またはストアドプロシージャのいずれかに変換されます。  
  
    3.  ユーザーが行った設定は、[ **適用** ] ボタンをクリックしたときにカスケード設定ファイルに保存されます。  
  
2.  **テーブル変換の設定:**  
  
    1.  このタブには、 **[ROWID の補助列の生成を抑制** する] オプションが含まれています。 オプションには、次の4つの値のいずれかを指定できます。  
  
        -   プロジェクト設定に従って変換する [継承]  
  
        -   はい  
  
        -   いいえ  
  
        -   プロジェクト設定に従って変換する  
  
    2.  **' Yes '** の場合、この設定では、対象テーブルで ROWID 補助列作成を作成することが禁止されます。  
  
    3.  ユーザーが行った設定は、[ **適用** ] ボタンをクリックしたときにカスケード設定ファイルに保存されます。  
  
## <a name="see-also"></a>参照  
[プロジェクトの設定 (変換) (MySQL から SQL)](./project-settings-conversion-mysqltosql.md)  
