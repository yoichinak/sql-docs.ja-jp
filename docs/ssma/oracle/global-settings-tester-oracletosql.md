---
description: グローバル設定 (テスター) (OracleToSQL)
title: グローバル設定 (テスター) (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4acc0f2a-85ba-4c99-856a-89030f5c418e
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: f3b8a5871ae12f9408700153afa4f429a4865514
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100067939"
---
# <a name="global-settings-tester-oracletosql"></a>グローバル設定 (テスター) (OracleToSQL)
[ **グローバル設定** ] ダイアログボックスの [テスト担当者] ページを使用して、Ssma tester の設定を指定します。  
  
テスト担当者の設定にアクセスするには、[ **ツール** ] メニューの [ **グローバル設定**] を選択し、左側のウィンドウの下部にある [ **テスト担当** 者] をクリックします。  
  
## <a name="options"></a>オプション  
**テスト可能オブジェクト分析**  
この設定では、テスト可能オブジェクトの分析を実行するかどうかを指定します。 SSMA Tester が依存オブジェクトを分析し、自動的に確認するようにする場合は、[ **はい]** を選択します。 既定のオプションセットは **[はい]** です。  
  
この設定では、次のオプションを使用できます。  
  
1.  はい  
  
2.  いいえ  
  
**補助テーブル保存モード**  
この設定では、テストケースの実行中に作成された内部補助テーブルを保存する方法を指定します。 この特定の設定には、次のオプションを設定できます。  
  
1.  必ず削除するアカウント  
  
2.  常に保存  
  
3.  テーブル比較に失敗した場合に保存する  
  
4.  テーブル比較に失敗した場合にユーザーに確認する  
  
既定のオプションセットは、[ **常に削除**] です。  
  
**データのロールバックを実行する**  
この設定では、各テストケースが実行された後にロールバック操作を実行するかどうかを指定します。 既定のオプションセットは [ **いいえ**] です。  
  
この設定では、次のオプションを使用できます。  
  
1.  はい  
  
2.  いいえ  
  
**最初の失敗後にテストの実行を停止する**  
この設定では、実行中にエラーが発生した場合に、現在実行中のテストケースを停止するかどうかを指定します。 既定のオプションセットは **[はい]** です。  
  
この設定では、次のオプションを使用できます。  
  
1.  はい  
  
2.  いいえ  
  
## <a name="see-also"></a>関連項目  
[テストケースの準備 &#40;OracleToSQL&#41;を終了しています ](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
