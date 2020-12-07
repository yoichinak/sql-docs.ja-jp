---
description: 変数値ファイルの作成 (「に」)
title: 変数値ファイルの作成 (による) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4b8f84909de05efc5d53b924eb298adcaab93d7f
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985035"
---
# <a name="creating-variable-value-files-accesstosql"></a>変数値ファイルの作成 (「に」)
変数値ファイルは、サーバーの移行間で頻繁に変更されるコマンドのパラメーター値 (転送元または転送先のサーバー名など) を構成する XML ファイルです。 多数のデータベースの移行が行われると、コマンドラインで **-v** スイッチを使用して、各ソースサーバーの値を格納するための複数の変数ファイルが作成され、マスタースクリプトファイルに参照されます。 この動作により、複数の変数ファイルの変数値を使用して、少数のスクリプトファイルで静的な値を保持することができます。  
  
> [!NOTE]  
> -  変数名の先頭には $ (ドル) 記号が付きます。 変数に変数値ファイルの値が割り当てられていない場合は、スクリプトファイルの解析中にエラーが発生し、コンソールの実行プロセスが停止します。  
> -  のエスケープ文字 **$** は **$$** です。 パラメーターの変数または静的な値に (ドル) 記号が含まれている場合は、を変数では **$** **$$** なく文字として扱うように指定する必要があります。  
> -  保守性を確保するために、 `'variable-group'` ユーザー定義変数を論理的に分離するために、要素内で変数を宣言できます。  この要素の使用は必須ではありません。  
  
**例:**  
  
**例 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**例 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>変数値ファイルの検証  
ユーザーは、[スキーマ] フォルダーで使用可能なスキーマ定義ファイル **ConsoleScriptVariablesSchema** に対して、変数の値ファイルを簡単に検証できます。  
  
## <a name="next-step"></a>次の手順  
コンソールを操作する次の手順では、 [サーバー接続ファイル &#40;作成して、sql&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>関連項目  
[サーバー接続ファイルの作成 (アクセス)](./creating-the-server-connection-files-accesstosql.md)  
