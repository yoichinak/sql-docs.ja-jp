---
title: VBScript を使用して WMI プロバイダーにアクセスする
description: コンピューター上で実行されている SQL Server のインストール済みインスタンスのバージョンを一覧表示する VBScript プログラムを作成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8b41779568bee4e3d83d8425fc6745d1191c7b58
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89520394"
---
# <a name="access-wmi-provider-for-configuration-management-using-vbscript"></a>VBScript を使用した構成管理用 WMI プロバイダーへのアクセス
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このセクションで [!INCLUDE[msCoName](../../includes/msconame-md.md)] は、コンピューター上で実行されているのインストール済みインスタンスのバージョンを一覧表示する VBScript プログラムを作成する方法について説明し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 コード例では、コンピューター上で実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスおよびそのバージョンをリストします。  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>SQL Server のインストール済みインスタンスの名前およびバージョンのリスト表示  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] のメモ帳など、テキスト エディターで新しいドキュメントを開きます。 この手順の後に示すコードをコピーし、.vbs 拡張子を付けてファイルを保存します。 この例の名前を test.vbs とします。  
  
2.  VBScript の `GetObject` 関数を使用して、コンピューター管理用の WMI プロバイダーのインスタンスに接続します。 この例では、mpc という名前のリモート コンピューターに接続しますが、コンピューター名は省略してローカル コンピューター (winmgmts:root\Microsoft\SqlServer\ComputerManagement) に接続してください。 `GetObject` 関数の詳細については、VBScript リファレンスを参照してください。  
  
3.  `InstancesOf` メソッドを使用して、サービスのリストを列挙します。 サービスは、`ExecQuery` メソッドの代わりに、簡単な WQL クエリと `InstancesOf` メソッドを使用して列挙することもできます。  
  
4.  `ExecQuery` メソッドおよび WQL クエリを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール済みインスタンスの名前およびバージョンを取得します。  
  
5.  ファイルを保存します。  
  
6.  コマンドプロンプトで「 **cscript test.vbs** 」と入力してスクリプトを実行します。  

## <a name="example"></a>例  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
