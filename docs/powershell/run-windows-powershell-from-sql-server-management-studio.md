---
title: SQL Server Management Studio から Windows PowerShell を実行する方法 | Microsoft Docs
description: パスが、選択したオブジェクトの場所にあらかじめ設定されている場合に、SQL Server Management Studio のオブジェクト エクスプローラーから Windows PowerShell セッションを開始する方法について説明します。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 03/14/2017
ms.openlocfilehash: c074b0f0ed5f5b041a8a4c4ed341837fec2b1926
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006164"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio から Windows PowerShell を実行する方法

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Windows PowerShell セッションは、 **の** オブジェクト エクスプローラー [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]から起動できます。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] によって Windows PowerShell が起動され、**SqlServer** モジュールが読み込まれて、パス コンテキストが、**オブジェクト エクスプローラー** ツリー内の関連ノードに設定されます。  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

**オブジェクト エクスプローラー**でオブジェクトに対して PowerShell の実行を指定すると、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] PowerShell スナップインの読み込みと登録が完了した Windows PowerShell セッションが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によって開始されます。 セッションのパスは、オブジェクト エクスプローラーで右クリックしたオブジェクトの場所にあらかじめ設定されています。 たとえば、オブジェクト エクスプローラーで [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベース オブジェクトを右クリックして **[PowerShell の起動]** を選択した場合、Windows PowerShell パスは次のように設定されます。  

```powershell
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```

## <a name="run-powershell"></a>PowerShell の実行

### <a name="to-run-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio から PowerShell を実行するには

1. **オブジェクト エクスプローラー**を開きます。

2. 作業対象オブジェクトのノードに移動します。

3. オブジェクトを右クリックし、 **[PowerShell の起動]** を選択します。

## <a name="permissions"></a>アクセス許可

PowerShell を [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] で開いた場合は管理者特権で実行されないため、WMI の呼び出しなどの一部のアクティビティが実行されない場合があります。  
  
## <a name="see-also"></a>参照

- [SQL Server PowerShell](sql-server-powershell.md)