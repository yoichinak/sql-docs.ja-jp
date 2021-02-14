---
description: テスト ケースのレポートの表示 (SybaseToSQL)
title: テストケースレポートの表示 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 833b1e862aa5629a9a6cbea5854e3a8db5a5cab2
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100080713"
---
# <a name="viewing-test-case-reports-sybasetosql"></a>テスト ケースのレポートの表示 (SybaseToSQL)
テストケースレポートには、テスト検証の結果と一般的なテスト情報が表示されます。 テストエラーが発生した場合、検証されたオブジェクト内の一致しないデータに関する情報も表示されます。  
  
## <a name="report-structure"></a>レポート構造  
レポートの上部には、次の統計情報が表示されます。  
  
-   テストされたオブジェクトの合計数と、テストが成功したオブジェクトの数。  
  
-   検証されたテーブルと外部キーの合計数と、正常に一致したテーブルと外部キーの数。  
  
-   テストケースの開始時刻、終了時刻、および実行にかかった合計時間。  
  
レポートの残りの部分では、次の4つのカテゴリに情報が表示されます。  
  
**前提条件のエラー**  
**前提条件** の手順で発生したすべてのエラーを表示します。 通常はスキップされます。  
  
**初期化**  
実行の状態を **成功** または **失敗** として表示します。  
  
**テストオブジェクトの結果**  
結果 (成功または失敗) と SSMA Tester が障害発生時に検出した不一致の比較。  
  
**最終**  
実行の状態を **成功** または **失敗** として表示します。  
  
## <a name="see-also"></a>参照  
[実行、テストケース &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[&#40;SybaseToSQL&#41;の移行されたデータベースオブジェクトのテスト ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
