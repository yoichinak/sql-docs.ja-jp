---
description: 型のマッピングの編集 (SybaseToSQL)
title: 型マッピングの編集 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 513f071a-d5e6-4ed5-acca-269bf76323c5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7fc5d4a2e2e907feb867d5cd9e44d2b7d8e77bd4
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100064227"
---
# <a name="edit-type-mapping-sybasetosql"></a>型のマッピングの編集 (SybaseToSQL)
[ **型マッピングの編集** ] ダイアログボックスでは、転送元データベースオブジェクトと転送先データベースオブジェクトの間で型がどのようにマップされるかを指定できます。  
  
このダイアログボックスには、いくつかの場所でアクセスできます。  
  
-   ソースデータベースまたはデータベースオブジェクトを選択すると、[ **型マッピング** ] タブがメタデータエクスプローラーの右側に表示されます。 [ **追加** ] をクリックして新しい型マッピングを追加するか、[ **編集** ] をクリックして既存の型マッピングを変更します。  
  
-   [ **ツール** ] メニューの [ **プロジェクトの設定** ] または [既定の **プロジェクトの設定**] をクリックします。 表示されるダイアログボックスで、[ **型マッピング**] を選択します。 [ **追加** ] をクリックして新しい型マッピングを追加するか、[ **編集** ] をクリックして既存の型マッピングを変更します。  
  
テーブル固有の型マッピングは、データベースおよびプロジェクトの種類のマッピングをオーバーライドします。 データベース固有のマッピングは、プロジェクトのマッピングをオーバーライドします。  
  
## <a name="options"></a>オプション  
**ソースの種類**  
データ型にマップするソースデータ型を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
データ型が可変長の場合、[ **ソースの種類**] の下に次のフィールドが表示されます。  
  
**From**  
このマッピングの最小の長さを指定します。 たとえば、 **nchar** データ型の場合は、「10」と入力して、このマッピングが **nchar (10)** から始まる範囲になるように指定できます。  
  
**To**  
このマッピングの最大長を指定します。 たとえば、 **nchar** データ型の場合は、「20」と入力すると、このマッピングが **nchar (20)** で終わる範囲に対して指定されます。  
  
**ターゲットの種類**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]変換元のデータ型がマップされるデータ型を選択します。 SSMA によってテーブルまたはストアドプロシージャが作成されると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、変換元のデータ型はこのデータ型に変更されます。  
  
データ型が可変長の場合、[ **対象の型**] の下に次のフィールドが表示されます。  
  
**Replace with**  
このマッピングの対象の長さを指定します。 たとえば、 **nvarchar** データ型の場合、「20」と入力すると、指定した変換元データ型を **nvarchar (20)** にマップするように指定できます。  
  
