---
title: MySQL と SQL Server 文字セットのマッピング (MySQLToSQL) |Microsoft Docs
description: SSMA for MySQL による文字データ型の変換中に使用する MySQL 文字のデータ型、式、およびリテラルの文字セットを指定する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 13b2accd6b4dc2ba2bbd8c9c1e6db312650d2d62
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100077623"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>MySQL と SQL Server 文字セットのマッピング (MySQLToSQL)
文字セット (Charset) は、MySQL 文字のデータ型、式、およびリテラルに指定できます。  
  
## <a name="charset-mapping"></a>文字セットのマッピング  
文字セットマッピングは、各 MySQL 文字セットに対して定義され、文字データ型の変換中に使用されます。 この例では、特定の文字セットの文字列データ型を変換する方法を指定します。  
  
-   National SQL Server 文字型 (NCHAR/NVARCHAR)、または  
  
-   標準 SQL Server 文字型 (CHAR/VARCHAR)  
  
1.  **national** target データベースの文字データ型は次のとおりです。  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **標準** ターゲットデータベースの文字データ型は次のとおりです。  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  型マッピングでは、 **各国** 語文字のデータ型へのマッピングのみを行うことができます。 MySQL 文字データ型が型マッピングに従って変換された後、文字セットマッピングが適用されます。  
  
> [!NOTE]  
> 文字セットマッピングは、メタデータオブジェクトエクスプローラーの各ノードレベルで定義でき、MySQL から読み取られたすべての文字セットを表します。  
  
## <a name="charset-mapping-on-different-node-levels"></a>異なるノードレベルでの文字セットマッピング  
文字セットマッピングは、次のようにさまざまなノードレベルで異なります。  
  
1.  ルートメタデータノードレベル  
  
2.  データベース、カテゴリ、およびオブジェクトノードレベル  
  
> [!NOTE]  
> 文字セットのマッピングを編集するために選択したタブには、異なるノードレベルでのマッピングに関係なく、3つのボタンが含まれています。  
>   
> これらは次のとおりです。  
>   
> 1.  **適用:** ユーザーによって行われた変更を適用します。これは、文字セットマッピングが編集され、まだ保存されていない場合にのみ有効です。  
> 2.  **取り消し:** ユーザーによって行われた変更を取り消します。 このボタンは、文字セットマッピングが編集されていても保存されていない場合に有効になります。  
> 3.  **既定値にリセット:** すべてのマッピングを既定値にリセットします。  
  
1.  **ルートメタデータノードレベルの場合:**  文字セットマッピンググリッドには、文字セットごとに個別の列を含む charset グリッドが含まれています。 グリッドの列は次のとおりです。  
  
    1.  グリッドの最初の列 ( **Charset 名** ) には、文字セット名が含まれています。  
  
    2.  2つ目の名前付き **文字の説明** には、文字セットの説明が含まれています。  
  
    3.  3番目の列、 **ターゲット文字セットの種類** には、特定の文字セットのマッピング設定が含まれています。 この列の値は次のとおりです。  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > 特定の文字セットの既定値は、CHAR/VARCHAR または NCHAR/NVARCHAR の後に ' (既定値) ' というプレフィックスが付いています。  
  
    MySQL データベースと、ルートメタデータノードレベルでのターゲットデータベースとの文字セットマッピングを以下に示します。  
  
    |文字セット名|文字セットの説明|ターゲット文字セットの種類 (既定値)|  
    |-|-|-|  
    |big5|Big5 繁体字中国語|NCHAR/NVARCHAR (既定値)|  
    |dec8|DEC (西ヨーロッパ)|CHAR/VARCHAR (既定値)|  
    |cp850|DOS 西ヨーロッパ|CHAR/VARCHAR (既定値)|  
    |hp8|HP 西ヨーロッパ|CHAR/VARCHAR (既定値)|  
    |koi8r|KOI8-R Relcom ロシア語|CHAR/VARCHAR (既定値)|  
    |ラテン1|cp1252 西ヨーロッパ|CHAR/VARCHAR (既定値)|  
    |latin2|ISO 8859-2 中央ヨーロッパ|CHAR/VARCHAR (既定値)|  
    |swe7|7bit スウェーデン語|CHAR/VARCHAR (既定値)|  
    |ascii|US ASCII|CHAR/VARCHAR (既定値)|  
    |ujis|EUC-日本日本語|NCHAR/NVARCHAR (既定値)|  
    |sjis|シフト JIS 日本語|NCHAR/NVARCHAR (既定値)|  
    |ヘブライ語|ISO 8859-8 ヘブライ語|CHAR/VARCHAR (既定値)|  
    |tis620|TIS620 タイ語|CHAR/VARCHAR (既定値)|  
    |euckr|EUC-韓国韓国語|NCHAR/NVARCHAR (既定値)|  
    |koi8u|KOI8-U ウクライナ語|CHAR/VARCHAR (既定値)|  
    |gb2312|GB2312 簡体字中国語|NCHAR/NVARCHAR (既定値)|  
    |greek|ISO 8859-7 ギリシャ語|CHAR/VARCHAR (既定値)|  
    |cp 1250|Windows 中央ヨーロッパ|CHAR/VARCHAR (既定値)|  
    |gbk|GBK 簡体字中国語|NCHAR/NVARCHAR (既定値)|  
    |latin5|ISO 8859-3 トルコ語|CHAR/VARCHAR (既定値)|  
    |armscii8|ARMSCII-8 アルメニア語|CHAR/VARCHAR (既定値)|  
    |utf8|UTF-8 Unicode|NCHAR/NVARCHAR (既定値)|  
    |ucs2|UCS-2 Unicode|NCHAR/NVARCHAR (既定値)|  
    |cp866|DOS ロシア語|CHAR/VARCHAR (既定値)|  
    |keybcs2|DOS Kamenicky Czech-Slovak|CHAR/VARCHAR (既定値)|  
    |macce|Mac 中央ヨーロッパ|CHAR/VARCHAR (既定値)|  
    |マクロ man|Mac 西ヨーロッパ|CHAR/VARCHAR (既定値)|  
    |cp852|DOS 中央ヨーロッパ|CHAR/VARCHAR (既定値)|  
    |latin7|ISO 8859-13 バルト語|CHAR/VARCHAR (既定値)|  
    |cp 1251|Windows キリル語|CHAR/VARCHAR (既定値)|  
    |cp 1256|Windows アラビア語|CHAR/VARCHAR (既定値)|  
    |cp 1257|Windows バルト言語|CHAR/VARCHAR (既定値)|  
    |binary|バイナリ擬似文字セット|CHAR/VARCHAR (既定値)|  
    |geostd8|GEOSTD8 グルジア語|CHAR/VARCHAR (既定値)|  
    |cp932|SJIS for Windows 日本語|NCHAR/NVARCHAR (既定値)|  
    |eucjpms|Windows 日本語用 UJIS|NCHAR/NVARCHAR (既定値)|  
  
2.  **データベース、カテゴリ、またはオブジェクトノードのレベル:** データベース、カテゴリ、またはオブジェクトノードレベルでは、[文字セットマッピング] グリッドに、ルートメタデータノードレベル可視化の行と同じ行が含まれます。  
  
    1.  というタイトルのグリッドの最初の列には、 **文字セット名に文字セット** 名が含まれています。  
  
    2.  2番目の列には、 **文字セットの説明** に文字セットの説明が含まれています。  
  
    3.  唯一の違いは、グリッドの3番目の列の値です。 3番目の列、 **ターゲットデータ型** には、特定の文字セットのマッピング設定が含まれています。 列の値は次のとおりです。  
  
        -   継承された (CHAR/VARCHAR または NCHAR/NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   データベース、カテゴリ、およびオブジェクトノードレベルでの MySQL データベースとターゲットデータベース間の文字セットマッピングでは、列 **ターゲットデータ型** のルート以外の各レベルの特定の文字セットの既定値は "継承" にする必要があります。  
> -   グリッドでは、この特定の文字セットによって親から継承された値に応じて、 **継承** された値に ' (CHAR/VARCHAR) ' または ' (NCHAR/NVARCHAR) ' のいずれかのサフィックスが付きます。  
  
