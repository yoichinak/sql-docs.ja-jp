---
description: メタデータの保存 (MySQLToSQL)
title: メタデータの保存 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9bc6273f-e8b1-430b-81a5-14330a783562
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b19ba78707fb596fde5ab73f04003a9d2d3feb9b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418458"
---
# <a name="save-metadata--mysqltosql"></a>メタデータの保存 (MySQLToSQL)
[ **メタデータの保存** ] ダイアログボックスでは、メタデータを保存する前に ssma プロジェクトに読み込むように求めるメッセージが表示されます。 これにより、オフラインで使用したり、技術サポート担当者などの他のユーザーに送信したりできる、完全なプロジェクトファイルを作成できます。  
  
[ **メタデータの保存** ] ダイアログボックスにアクセスするには、プロジェクトを保存します。 メタデータが見つからない場合は、SSMA によって [ **メタデータの保存** ] ダイアログボックスが表示されます。  
  
## <a name="options"></a>オプション  
**名前**  
プロジェクト内の各データベースの名前。  
  
**状態**  
メタデータが SSMA プロジェクトに読み込まれるかどうか、またはメタデータが存在しないかどうかを示します。  
  
SSMA は、必要に応じてメタデータをプロジェクトに読み込みます。 メタデータを参照し、スキーマを変換すると、メタデータが自動的に読み込まれます。  
  
**[すべて選択]**  
一覧表示されているすべてのデータベースを選択します。  
  
**Clear**  
メタデータが欠落しているすべてのデータベースのチェックボックスをオフにします。 メタデータが読み込まれている場合は、このチェックボックスをオフにすることはできません。  
  
**および**  
プロジェクトを保存し、メタデータが存在しない選択したデータベースのメタデータを読み込みます。  
  
**キャンセル**  
保存操作をキャンセルします。 見つからないメタデータはプロジェクトに読み込まれません。  
  
