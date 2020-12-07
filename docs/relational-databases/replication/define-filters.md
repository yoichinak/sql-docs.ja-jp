---
description: '[フィルターの定義]'
title: '[フィルターの定義] | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e4834e78ec82a681faba9f6c0fa780d78f890def
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96121324"
---
# <a name="define-filters"></a>[フィルターの定義]
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **[フィルターの定義]** ダイアログ ボックスを使用すると、グリッド内で競合するサブセットを確認するために、データ競合に適用するフィルターを定義できます。 フィルターを定義するには、 **[演算子]** ボックスで演算子を選択し、値を入力します。 たとえば、競合で負けたサーバーが **ReplTest1** の競合だけを表示するには、 **[演算子]** ボックスで **[等しい]** を選択し、1 番目の **[値]** 列に「 **ReplTest1** 」と入力します。  
  
## <a name="options"></a>オプション  
 **[オペレーター]**  
 フィルターで使用する演算子 (たとえば、 **[次の値以下]**) を選択します。
  
 **Value**  
 フィルターの値を入力します。 ほとんどの演算子は 1 番目の **[値]** 列に値を入力するだけで済みますが、 **[次の値の間]** と **[次の値の範囲外]** の操作は、2 つの **[値]** 列に値を入力する必要があります。  
  
 **Clear**  
 このボタンをクリックすると、既に定義されているすべてのフィルターがクリアされます。  
  
## <a name="see-also"></a>参照  
 [[Microsoft レプリケーション競合表示モジュール] (マージ レプリケーション)](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Microsoft レプリケーション競合表示モジュール (トランザクション レプリケーション)](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
