---
title: '[TCP/IP のプロパティ] ダイアログ ボックス ([プロトコル] タブ)'
description: '[TCP/IP のプロパティ] ダイアログ ボックスの [プロトコル] タブにあるオプションを使用して、Keep Alive 間隔、有効なフラグ、およびその他のプロパティを構成します。'
ms.custom: seo-lt-2019
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1b53ae759c4a8875d329f9ac7b443f4168042c96
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88900926"
---
# <a name="tcpip-properties-protocols-tab"></a>[TCP/IP のプロパティ] ダイアログ ボックス ([プロトコル] タブ)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  **[TCP/IP のプロパティ]** ダイアログ ボックスは、TCP/IP プロトコルのオプションを構成するために使用します。 左ペインで **[TCP/IP]** をクリックすると、詳細ペインに個々の IP アドレス構成が表示されます。  
  
 変更を有効にするには、Microsoft SQL Server を再起動する必要があります。  
  
## <a name="options"></a>Options  
 **有効**  
 可能な値は、 **[はい]** と **[いいえ]** です。  
  
 **[Keep Alive]**  
 接続のリモート側のコンピューターが使用可能かどうかを確認するために、Keep Alive パケットを送信する間隔 (ミリ秒) を指定します。  
  
 **[すべて受信待ち]**  
 コンピューター上のネットワーク カードに割り当てられているすべての IP アドレスで SQL Server がリッスンするかどうかを指定します。 **[いいえ]** に設定した場合は、各 IP アドレスのプロパティ ダイアログ ボックスを使用して、IP アドレスごとに個別の構成を行ってください。 **[はい]** に設定した場合は、 **[IPAll]** プロパティ ボックスの設定がすべての IP アドレスに適用されます。 既定値は **[はい]** です。  
  
 **[遅延なし]**  
 SQL Server では、このプロパティに対する変更は実装されません。  
  
## <a name="see-also"></a>参照  
 [ネットワーク プロトコルの選択](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))   
 [TCP/IP を使用した有効な接続文字列の作成](creating-a-valid-connection-string-using-tcp-ip.md)  
  
