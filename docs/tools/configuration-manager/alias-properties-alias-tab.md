---
title: '[別名] プロパティ ([別名] タブ)'
description: '[プロパティ] ダイアログ ボックスの [別名] タブを使用して、SQL Server のインスタンスに接続するときに代替名を使用できるように別名を構成します。'
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 2d1498e2-129c-4ce7-88e5-408e4037243c
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cd2a47f55032cc4b40ad4e0e14e57478ff88570a
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88900901"
---
# <a name="ltaliasgt-properties-alias-tab"></a>&lt;[別名]&gt; プロパティ ([別名] タブ)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

別名は、接続のために使用できる代替名です。 別名は、接続文字列の必須要素をカプセル化したものであり、ユーザーが選択した名前でそれらの要素を公開できます。 **[\<**Alias name**> のプロパティ]** ダイアログ ボックスの **[別名]** ページを使用して、別名の接続文字列の各要素を表示または指定します。

## <a name="options"></a>Options

**[別名]**

この接続を参照するために使用する名前 (別名) です。  

**[パイプ名]**  /  **[ポート番号]**  

接続文字列の追加要素です。 このボックスの名前は、選択したプロトコルによって異なります。 例については、最後に示すトピックを参照してください。  

**プロトコル**

接続に使用するプロトコルです。

**サーバー**

接続先の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前です。  

## <a name="see-also"></a>参照

- [共有メモリ プロトコルを使用した有効な接続文字列の作成](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
- [TCP/IP を使用した有効な接続文字列の作成](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)
- [名前付きパイプを使用した有効な接続文字列の作成](/previous-versions/sql/sql-server-2016/ms189307(v=sql.130))