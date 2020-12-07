---
title: タブ補完の管理 (SQL Server PowerShell)
description: SQL Server PowerShell モジュールで 3 つの変数を適切に使用することで、Windows PowerShell のタブ補完を制御する方法について学習します。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: d15d859239aa9ea36f0885218d3469489f28a9b2
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006083"
---
# <a name="manage-tab-completion-with-sql-server-powershell"></a>SQL Server PowerShell を使用したタブ補完の管理

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell スナップインには、Windows PowerShell のタブ補完を制御するための 3 つの変数 (**$SqlServerMaximumTabCompletion**、 **$SqlServerMaximumChildItems**、 **$SqlServerIncludeSystemObjects**) が追加されました。 入力された文字列で名前が始まるアイテムの一覧を返すタブ補完によって、入力の手間を削減することができます。  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

Windows PowerShell のタブ補完機能では、パスやコマンドレット名の一部を入力して Tab キーを押すと、既に入力した部分に一致する名前のアイテムの一覧を取得できます。 名前の残りの部分を入力しなくても、その一覧からアイテムを選択できます。  

多数のオブジェクトを含むデータベースで作業する場合、タブ補完の一覧が大きくなることがあります。 また、ビューなどの一部の種類の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オブジェクトには、多数のシステム オブジェクトが含まれます。  

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] スナップインでは、タブ補完および **Get-ChildItem**で表示される情報の量を制御するために使用できる 3 つのシステム変数が導入されています。

## <a name="sqlservermaximumtabcompletion--n"></a>$SqlServerMaximumTabCompletion =** *n*

タブ補完の一覧に含めるオブジェクトの最大数を指定します。 *n* を超える数のオブジェクトが含まれるパス ノードで Tab キーを押した場合、タブ補完の一覧が *n*件までで切り捨てられます。 *n* は整数です。 既定の設定は 0 で、これは一覧表示されるオブジェクトの数に制限がないことを示します。  

## <a name="sqlservermaximumchilditems--n"></a>$SqlServerMaximumChildItems =** *n*

**Get-ChildItem**で表示されるオブジェクトの最大数を指定します。 **n** を超える数のオブジェクトが含まれるパス ノードで *Get-ChildItem* を実行した場合、一覧が *n*件までで切り捨てられます。 *n* は整数です。 既定の設定は 0 で、これは一覧表示されるオブジェクトの数に制限がないことを示します。  

## <a name="sqlserverincludesystemobjects---true--false-"></a>$SqlServerIncludeSystemObjects =** { **$True** | **$False** }

**$True**の場合、タブ補完と **Get-ChildItem**でシステム オブジェクトが表示されます。 **$False**の場合、システム オブジェクトは表示されません。 既定の設定は **$False**です。  

## <a name="set-the-sql-server-tab-completion-variables"></a>SQL Server のタブ補完変数の設定

既定値から変更する場合は、その対象となるすべての変数について、新しい値を設定する必要があります。  

### <a name="example-powershell"></a>例 (PowerShell)

次の例では、3 つすべての変数を設定し、設定を一覧表示します。  

```powershell
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```

## <a name="see-also"></a>参照

- [SQL Server PowerShell のインストール](download-sql-server-ps-module.md)
- [SQL Server PowerShell](sql-server-powershell.md)