---
description: DROP TABLE コマンド
title: DROP TABLE コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1284b2bb446b21986ae2862e9f8138de910b7922
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99198573"
---
# <a name="drop-table-command"></a>DROP TABLE コマンド
データソースで指定されたデータベースからテーブルを削除し、ディスクから削除します。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブな Visual FoxPro 言語構文がサポートされています。 ドライバー固有の情報については、「解説」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>設定  
 *TableName*  
 データソースで指定されたデータベースから削除するテーブルと、ディスクから削除するテーブルを指定します。  
  
 *FileName*  
 ディスクから削除するフリーテーブルを指定します。  
  
 ?  
 [削除] ダイアログを表示します。このダイアログボックスでは、データソースで指定されたデータベースから削除するテーブルを選択したり、ディスクから削除したりできます。  
  
## <a name="remarks"></a>コメント  
 DROP TABLE が発行されると、テーブルに関連付けられているすべてのプライマリインデックス、既定値、および検証ルールも削除されます。 DROP TABLE は、削除するテーブルに関連付けられたルールまたはリレーションがテーブルにある場合に、データソースで指定されたデータベース内の他のテーブルにも影響します。 テーブルがデータベースから削除されても、ルールとリレーションは無効になります。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションが ODBC SQL ステートメントドロップテーブルをデータソースに送信すると、次の表に示す構文を使用して、Visual FoxPro ODBC ドライバーによってコマンドが Visual FoxProDROP TABLE コマンドに変換されます。  
  
|ODBC 構文|データ ソースの|Visual FoxPro の構文|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE *-テーブル名*|データベース (dbc ファイル)|テーブル *TableName* 削除の削除|  
||フリーテーブル (.dbf ファイル) のディレクトリ|削除、 *Dbfname*<br /><br /> *CdxName* の消去<br /><br /> *Fptname* の消去|
