---
description: XML のセキュリティに関する考慮事項
title: XML のセキュリティに関する考慮事項 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: rothja
ms.author: jroth
ms.openlocfilehash: 608ad67d531573d0124ea312252e6d30c289bf15
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978793"
---
# <a name="xml-security-considerations"></a>XML のセキュリティに関する考慮事項
Recordset オブジェクトの ADO Save および Open メソッドは、Internet Explorer で実行するための安全な操作とは見なされません。 このため、これらのメソッドが、ブラウザーでホストされているアプリケーションまたはコントロールで実行されているスクリプトコードで使用されている場合、ブラウザーのセキュリティ構成はその動作に影響します。  
  
 Internet Explorer 5 では、インターネットゾーンの既定では、このような操作に対してセキュリティ上の制限があります。 その構成では、レコードセットによって、クライアント上のローカルファイルシステムへのアクセスを許可したり、ページのダウンロード元のサーバーのドメインの外部にあるデータソースにアクセスしたりすることはできません。 具体的には、ブラウザーホスト内で実行されている場合、レコードセットは、ページのダウンロード元と同じサーバー上にある場合にのみ、ファイルに保存できます。 同様に、ファイルからファイルを読み込んでレコードセットを開くこともできます。その場合は、そのファイルが、ページのダウンロード元と同じサーバー上にある場合に限られます。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](./persisting-records-in-xml-format.md)