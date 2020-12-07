---
description: 変数値ファイルの作成 (SybaseToSQL)
title: 変数値ファイルの作成 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Creating Variable Value Files
- Sybase Console,Variable Value File Validation
ms.assetid: 395be464-4b19-44f7-91e5-b8876d6743dc
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2f2d3a53cb12a0d7762137a44cc12ec6f06a5d81
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036701"
---
# <a name="creating-variable-value-files-sybasetosql"></a>変数値ファイルの作成 (SybaseToSQL)
変数値ファイルは、などのコマンドのパラメーター値を構成する XML ファイルです。サーバーの移行から別のサーバーへの移行に頻繁に変更される転送元または転送先のサーバー名を指定します。 多数のデータベースの移行が行われると、各ソースサーバーの値を格納するための複数の変数ファイルが作成され、コマンドラインで **-v** スイッチを使用してマスタースクリプトファイルに参照されます。 これにより、複数の変数ファイルの変数値を使用して、いくつかのスクリプトファイルで静的な値を保持することができます。  
  
> [!NOTE]  
> 1.  変数名の先頭には $ (ドル) 記号が付きます。 変数に変数値ファイルの値が割り当てられていない場合、スクリプトファイルの解析中にエラーが発生し、コンソールの実行プロセスが停止します。  
> 2.  のエスケープ文字 **$** は **$$** です。 パラメーターの変数または静的な値に (ドル) 記号が含まれている場合は、を変数では **$** **$$** なく文字として扱うように指定する必要があります。  
> 3.  保守性を確保するために、 `'variable-group'` ユーザー定義変数を論理的に分離するために、要素内で変数を宣言できます。  この要素の使用は必須ではありません。  
  
**例:**  
  
**例 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**例 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>変数値ファイルの検証  
ユーザーは、[スキーマ] フォルダーで使用可能なスキーマ定義ファイル **ConsoleScriptVariablesSchema** に対して、変数の値ファイルを簡単に検証できます。  
  
## <a name="next-step"></a>次の手順  
コンソールを操作する次の手順では、[サーバー接続ファイル &#40;SybaseToSQL&#41;を作成し](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)ます。  
  
## <a name="see-also"></a>参照  
[サーバーファイルを作成する (Sybase)](./creating-the-server-connection-files-sybasetosql.md)  
