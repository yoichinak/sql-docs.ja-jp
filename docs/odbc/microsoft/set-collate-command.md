---
description: SET COLLATE コマンド
title: COLLATE コマンドの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ca796da60adf0c432b5bbd80065e58563664bc5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466384"
---
# <a name="set-collate-command"></a>SET COLLATE コマンド
後続のインデックス作成および並べ替え操作での文字フィールドの照合順序を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>引数  
 *cSequenceName*  
 照合順序を指定します。 次の表では、使用可能な照合順序のオプションについて説明します。  
  
|オプション|Language|  
|-------------|--------------|  
|オランダ語|オランダ語|  
|GENERAL|英語、フランス語、ドイツ語、スペイン語、ポルトガル語、およびその他の西ヨーロッパ言語|  
|ドイツ語|ドイツ語の電話帳の注文 (DIN)|  
|アイスランド|アイスランド語|  
|装置|コンピューター (以前のバージョンの FoxPro の既定の照合順序)|  
|NORDAN|ノルウェー語、デンマーク語|  
|スペイン語|従来のスペイン語|  
|SWEFIN|スウェーデン語、フィンランド語|  
|UNIQWT|一意の重み|  
  
> [!NOTE]  
>  スペイン語のオプションを指定すると、 *ch*は*c*と*d*の間を並べ替える1文字で、 *l*と*m*の間*で並べ替えら*れます。  
  
 照合順序のオプションをリテラル文字列として指定する場合は、必ずオプションを引用符で囲みます。  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 コンピューターは、既定の照合順序のオプションであり、ユーザーが慣れているシーケンス Xbase です。 文字は、現在のコードページに表示される順序で並べ替えられます。  
  
 米国および西ヨーロッパのユーザーには、[全般] を使用することをお勧めします。 文字は、現在のコードページに表示される順序で並べ替えられます。 2.5 より前のバージョンの FoxPro では、文字フィールドを一貫したケースに変換するために **UPPER**() 関数または **LOWER**() 関数を使用してインデックスが作成されている可能性があります。 2.5 より後のバージョンの FoxPro では、代わりに一般照合順序のシーケンスオプションを指定し、 **UPPER**() 変換を省略できます。  
  
 [コンピューター] 以外の照合順序のオプションを指定した場合に、idx ファイルを作成すると、常に compact. idx が作成されます。  
  
 現在の照合順序を返すには、SET ("COLLATE") を使用します。  
  
 [ODBC Visual FoxPro の [設定] ダイアログボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)を使用するか、 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)で接続文字列内の Collate キーワードを使用して、データソースの照合順序を指定できます。 これは、次のコマンドを発行することと同じです。  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>解説  
 COLLATE を設定すると、サポートされている言語のいずれかで、アクセントが付いた文字を含むテーブルを並べ替えることができます。 [部単位で印刷] の設定を変更しても、以前に開いたインデックスの照合順序には影響しません。 Visual FoxPro では、既存のインデックスが自動的に保持されるため、同じフィールドであっても、さまざまな種類のインデックスを柔軟に作成できます。  
  
 たとえば、[COLLATE] を [全般] に設定してインデックスを作成し、[COLLATE の設定] 設定を後でスペイン語に変更した場合、インデックスには一般的な照合順序が保持されます。  
  
## <a name="see-also"></a>関連項目  
 [ODBC Visual FoxPro セットアップ ダイアログ ボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
