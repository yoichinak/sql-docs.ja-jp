---
description: データベースからの更新 (OracleToSQL)
title: データベースからの更新 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: ecf7edd43af59f2d388f83b118ad8b6a1583b0be
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100067647"
---
# <a name="refresh-from-database-oracletosql"></a>データベースからの更新 (OracleToSQL)
[ **データベースから更新** ] ダイアログボックスでは、Oracle データベースから更新するオブジェクトを選択できます。 ダイアログボックス内の行は、メタデータの状態に基づいて色分けされています。  
  
-   オブジェクトメタデータがローカルと Oracle データベースで変更されている場合、行は青色になります。  
  
-   Oracle データベースではオブジェクトメタデータが変更されたが SSMA では変更されていない場合、行は黄色になります。  
  
-   オブジェクトメタデータが Oracle データベースではなくローカルに変更された場合、その行は緑色になります。  
  
-   オブジェクトが Oracle データベースで新しく追加された場合、行はピンクです。  
  
既定のオブジェクト更新設定は、[ **プロジェクトの設定** ] ダイアログボックスで指定できます。 詳細については、「 [プロジェクトの設定&#40;同期&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)」を参照してください。  
  
[ **データベースから更新** ] ダイアログボックスにアクセスするには、Oracle メタデータエクスプローラーでオブジェクトを右クリックし、[ **データベースからの更新**] をクリックします。  
  
## <a name="options"></a>オプション  
**折りたたみ (-)**  
すべてのオブジェクトグループを折りたたむと、個々のオブジェクトが非表示になります。  
  
**展開 (+)**  
[すべてのオブジェクトグループ] を展開して、個々のオブジェクトを表示します。  
  
**同じオブジェクトの非表示/表示**  
Oracle データベースと SSMA のオブジェクトメタデータが同じである場合、リストのオブジェクトを非表示にします。  
  
**データベースからの更新 (矢印ボタン)**  
矢印ボタンを使用して、SSMA で選択したオブジェクトのメタデータを更新するように指定します。  
  
**データベースから更新しない (X ボタン)**  
[X] ボタンを使用して、選択したオブジェクトのメタデータを SSMA で更新しないように指定します。  
  
**凡例**  
[ **凡例** ] ダイアログボックスを表示します。 凡例には、行の色とメタデータの状態との間のマッピングが含まれます。  
  
[**データベースからの更新**] ダイアログボックスの上部にある [**凡例**] ダイアログボックスを維持するには、[上 **に表示**] チェックボックスをオンにします。  
  
