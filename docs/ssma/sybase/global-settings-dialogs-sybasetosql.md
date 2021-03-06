---
description: グローバル設定 (ダイアログ) (SybaseToSQL)
title: グローバル設定 (ダイアログ) (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e11452b7-ba94-4367-a745-5ccf1764acec
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a4d822ff4897cabdf97d674ab1a7ec0db4ef4c6a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100078693"
---
# <a name="global-settings-dialogs--sybasetosql"></a>グローバル設定 (ダイアログ) (SybaseToSQL)
[ **グローバル設定** ] ダイアログボックスの [ダイアログ] ページを使用して、ssma の既定のユーザー操作と警告設定を指定します。  
  
[ **ツール** ] メニューのダイアログ設定にアクセスするには、[ **グローバル設定**] を選択し、左側のウィンドウの下部にある [ **GUI** ] をクリックして、[ **ダイアログ**] を選択します。  
  
## <a name="options"></a>オプション  
**オブジェクトを上書きする前に警告する**  
SSMA がオブジェクトを SQL Server に変換するときに、プロジェクトの SQL Server メタデータに既に存在しているオブジェクトもあります。 これらのオブジェクトは既に変換されている場合もあれば、変換するオブジェクトとしてターゲットスキーマ内でオブジェクトの名前が同じである場合もあります。  
  
このオプションを使用して、重複するオブジェクト定義を上書きするように SSMA が要求するかどうかを指定します。  
  
-   [ **True**] を選択した場合、重複するオブジェクトが見つかったときに ssma によって警告ダイアログボックスが表示されます。 このダイアログボックスでは、個々のオブジェクトまたはすべての重複オブジェクトを上書きするように指定することも、個々のオブジェクトまたはすべての複製オブジェクトをスキップすることもできます。  
  
-   [ **False**] を選択すると、既定のアクションを指定したときに、[ **既定のアクションを上書き** する] オプションが表示されます。  
  
**オブジェクト上書きの既定の操作**  
このオプションは、[**オブジェクトを上書きする前に警告** する] オプションで [ **False** ] を選択した場合に表示されます。  
  
このオプションを使用して、既定のオブジェクトの上書き動作を指定します。  
  
-   [ **True**] を選択すると、ssma は、同じ名前を持ち、変換するオブジェクトと同じターゲットスキーマ内にある、SQL Server プロジェクトメタデータ内のオブジェクトを自動的に上書きします。  
  
-   **False** を選択した場合、ssma は変換中にオブジェクトメタデータを上書きしません。  
  
