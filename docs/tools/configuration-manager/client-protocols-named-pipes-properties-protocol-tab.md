---
title: クライアント プロトコル - [名前付きパイプのプロパティ] ダイアログ ボックス ([プロトコル] タブ)
description: SQL Server 構成マネージャーで既定のパイプの説明を表示または変更する方法について説明します。 別のパイプに接続する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 97be95a8db2160bb75a7a4fe4947aa96deca05a7
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88900580"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>クライアント プロトコル - [名前付きパイプのプロパティ] ダイアログ ボックス ([プロトコル] タブ)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーでは、 **[名前付きパイプのプロパティ]** ダイアログ ボックスの **[プロトコル]** タブを使用して、既定のパイプに関する説明の表示や変更を行います。 別のパイプに接続するには、そのパイプを **[既定のパイプ]** ボックスに入力してください。 接続文字列の詳細については、「 [Creating a Valid Connection String Using Named Pipes](/previous-versions/sql/sql-server-2016/ms189307(v=sql.130))」を参照してください。  
  
## <a name="options"></a>Options  
 **[既定のパイプ]**  
 名前付きパイプ Net-Library が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の対象インスタンスに接続するために使用する既定のパイプを指定します。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は `\\.\pipe\sql\query`  
  
 既定のパイプに接続するには、 `sql\query`  
  
 **有効**  
 可能な値は、 **[はい]** と **[いいえ]** です。  
  
## <a name="see-also"></a>参照  
 [ネットワーク プロトコルの選択](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))  
  
