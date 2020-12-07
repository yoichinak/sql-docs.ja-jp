---
title: external scripts enabled サーバー構成オプション
description: SQL Server の external scripts enabled オプションについて説明します。 有効にすると、R や Python などのサポートされている言語で外部スクリプトを実行できるようになります。
ms.date: 06/30/2020
ms.prod: sql
ms.technology: machine-learning-services
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ec430a256e07cfee21a14bbe3fe97426b044b4fd
ms.sourcegitcommit: 71d2389cf27156fa0404a6e6f65fb7a61c40789a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2020
ms.locfileid: "91636132"
---
# <a name="external-scripts-enabled-server-configuration-option"></a>external scripts enabled サーバー構成オプション
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

**external scripts enabled** オプションを使用して、特定のリモート言語拡張機能を使用したスクリプトの実行を有効します。 このプロパティは既定で無効になっています。 **Machine Learning Services** をインストールするとき、必要に応じてセットアップでこのプロパティを true に設定できます。

## <a name="remarks"></a>解説

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) プロシージャを使用して外部スクリプトを実行する前に、external script enabled オプションを有効にする必要があります。 R や Python などのサポートされている言語で書かれたスクリプトを実行するには、**sp_execute_external_script** を使います。 

+ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] の場合

    [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] には、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] での R 言語のサポートと、一連の R ワークステーション ツールおよび接続性ライブラリが含まれます。

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップの間に **R Services** をインストールして、R スクリプトの実行を有効にします。

+ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] 以降の場合

    [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] では、R と Python の両方の言語がサポートされています。

    外部スクリプトの実行を有効にするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップの間に、**Machine Learning Services** 機能をインストールします。 初期セットアップのときに、必ず少なくとも 1 つの言語を選んでください (R と Python のどちらか一方または両方)。
    
+ [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)] 以降の [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] によって、R、Python、Java のすべてとその他のサード パーティ言語がサポートされています。

任意のサポート言語で外部スクリプトの実行を有効にするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時に、Machine Learning Services と言語拡張機能をインストールします。

## <a name="additional-requirements"></a>その他の要件

セットアップの後、外部スクリプトを有効にするには、次のスクリプトを実行します。

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

詳細については、「[Windows に SQL Server Machine Learning Services (Python と R) をインストールする](../../machine-learning/install/sql-machine-learning-services-windows-install.md)」または [Linux に関するページ](../../linux/sql-server-linux-setup-machine-learning-docker.md?toc=/sql/machine-learning/toc.json)を参照してください。

## <a name="see-also"></a>関連項目

+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
+ [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
+ [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [SQL の機械学習のドキュメント](../../machine-learning/index.yml)
