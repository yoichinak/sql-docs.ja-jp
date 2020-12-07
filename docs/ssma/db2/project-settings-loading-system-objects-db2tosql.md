---
description: プロジェクトの設定 (システムオブジェクトの読み込み) (DB2ToSQL)
title: プロジェクトの設定 (システムオブジェクトの読み込み) (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cb0f25ce5063a22fb89d0afa8619b90d34a96f16
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426964"
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>プロジェクトの設定 (システムオブジェクトの読み込み) (DB2ToSQL)
[ **プロジェクトの設定** ] ダイアログボックスの [システムオブジェクトの読み込み] ページでは、ssma によって変換および読み込まれる DB2 システムオブジェクトを指定でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
[システムオブジェクトの読み込み] ウィンドウは、[ **プロジェクトの設定** ] ダイアログボックスと [既定のプロジェクトの **設定** ] ダイアログボックスで使用できます。  
  
-   すべての SSMA プロジェクトの設定を指定するには、[ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックし、[移行の **対象バージョン** から設定を表示または変更する必要がある移行プロジェクトの種類] ドロップダウンから [ **全般** ] をクリックし、[ **システムオブジェクトの読み込み**] をクリックします。  
  
-   現在のプロジェクトの設定を指定するには、[ **ツール** ] メニューの [ **プロジェクトの設定**] をクリックし、左側のウィンドウの下部にある [ **全般** ] をクリックして、[ **システムオブジェクトの読み込み**] をクリックします。  
  
## <a name="default-settings"></a>既定の設定  
システムオブジェクトを変換すると、システムリソースが消費され、時間がかかります。 パフォーマンスを向上させるために、SSMA は、次の一覧に示すように、最もよく使用されるシステムオブジェクトのみを選択します。  
  
-   SYS.DATABASES.DBMS_OUTPUT  
  
-   SYS.DATABASES.DBMS_PIPE  
  
-   SYS.DATABASES.DBMS_UTILITY  
  
-   SYS.DATABASES.規格  
  
-   SYS.DATABASES.UTL_FILE  
  
-   SYS.DATABASES.DBMS_LOB  
  
-   SYS.DATABASES.DBMS_SQL  
  
-   SYS.DATABASES.DBMS_SESSION  
  
DB2 オブジェクトが追加のシステムオブジェクトを参照する場合は、それらのオブジェクトを選択する必要があります。 DB2 データベースオブジェクトによって参照されているシステムオブジェクトを選択しない場合、SSMA は変換エラーを報告します。 システムオブジェクトがないことが原因で変換エラーが発生した場合は、このダイアログボックスで不足しているオブジェクトを選択します。 その後、必要に応じて変換を繰り返すことができます。  
  
