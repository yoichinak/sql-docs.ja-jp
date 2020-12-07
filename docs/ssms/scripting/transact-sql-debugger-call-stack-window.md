---
title: '[呼び出し履歴] ウィンドウ'
description: Transact-SQL デバッガーの [呼び出し履歴] ウィンドウを使用して、パラメーターのデータ型、およびストアドプロシージャ、関数、トリガーの値も確認する方法について説明します。
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Call Stack Window [Transact-SQL]
ms.assetid: ddb0b19c-87cd-4883-bcb8-ec09ffb30369
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3df3d33392751bcdc98b2c9efd2ea7b6b24ed5ab
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036185"
---
# <a name="transact-sql-debugger---call-stack-window"></a>Transact-SQL デバッガー - [呼び出し履歴] ウィンドウ

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**[呼び出し履歴]** ウィンドウには、呼び出し履歴上のモジュール、およびモジュールに渡されるパラメーターのデータ型と値が表示されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュール (ストアド プロシージャ、関数、およびトリガーを含む) 呼び出し履歴を表示するには、デバッグ モードである必要があります。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>タスク一覧

**[呼び出し履歴] ウィンドウにアクセスするには**

- **[デバッグ]** メニューの **[ウィンドウ]** をポイントし、 **[呼び出し履歴]** をクリックします。

**現在の呼び出し履歴フレームを変更するには**

次の手順のどちらかを使用して、スタック フレームを現在のフレームにすることができます。

- スタック フレームを右クリックし、 **[フレームに切り替え]** をクリックします。

- スタック フレームをダブルクリックします。  

**現在のフレーム以外のフレームのソースを表示するには**

- スタック フレームを右クリックし、 **[ソース コードへ移動]** をクリックします。

## <a name="stack-frames"></a>スタック フレーム

**[呼び出し履歴]** ウィンドウの各行はスタック フレームと呼ばれ、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイルからモジュールへの呼び出し、またはあるモジュールから別のモジュールへの呼び出しを表します。 表示上、一番下のスタック フレームは、スタックへの最初の呼び出しを行った [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディター ウィンドウの行を表します。 一番上の行は、デバッガーが実行を一時停止した行を表し、ウィンドウの左余白の黄色の矢印で示されます。 その間の各行は、モジュールと、1 つ上のスタック フレームを呼び出したソース コードの行番号を表します。  

**[ローカル]** 、 **[ウォッチ]** 、および **[クイック ウォッチ]** の各ウィンドウ内のすべての式は、現在のスタック フレームに基づいて評価されます。 クエリ エディター ウィンドウには、現在のフレームのコードが表示されます。 既定では、現在のスタック フレームは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーが実行を一時停止したフレームです。 現在のスタック フレームを別のフレームに変更すると、 **[ローカル]**、 **[ウォッチ]**、および **[クイック ウォッチ]** の各ウィンドウ内の式が新しいフレームのコンテキストで再評価され、新しいフレームのソース コードがクエリ エディター ウィンドウに表示されます。  
  
## <a name="columns"></a>[列]

 **名前**  
 呼び出し履歴上のモジュールに関する情報を表示します。  
  
 呼び出し履歴の一番下の行の場合、 **[名前]** には、クエリ エディターのソース ウィンドウとスタックへの最初の呼び出しの行番号が表示されます。 その他の行の場合、 **[名前]** は、 **[Module(Instance.Database)(ParmList) LineNumber]** の形式になります。  
  
 **[Module]**  
 ストアド プロシージャ、関数、または次のフレームを呼び出したストアド プロシージャの名前です。  
  
 **[Instance.Database]**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスと、モジュールを保持しているデータベースです。  
  
 **[ParmList]**  
 モジュールの呼び出し時に渡される各パラメーターのデータ型、名前、および値を示します。  
  
 **LineNumber**  
 一番上の行を除くすべての行では、 **[LineNumber]** は、モジュール内のどの行でフレームを呼び出したかを示します。 一番上の行では、 **[LineNumber]** は、デバッガーのフォーカスが現在置かれている行を示します。  
  
 **Language**  
 **を表す** [Transact-SQL] [!INCLUDE[tsql](../../includes/tsql-md.md)]が表示されます。  
  
## <a name="see-also"></a>参照

- [Transact-SQL デバッガー](./transact-sql-debugger.md)
- [Transact-SQL デバッガー情報](./transact-sql-debugger-information.md)
- [Transact-SQL コードのステップ実行](./step-through-transact-sql-code.md)