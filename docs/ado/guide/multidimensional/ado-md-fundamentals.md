---
description: ADO MD の基礎
title: ADO MD の基礎 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
author: rothja
ms.author: jroth
ms.openlocfilehash: 7634d32b35eef7d0289ef778bee9646a050e8755
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100032194"
---
# <a name="ado-md-fundamentals"></a>ADO MD の基礎
Microsoft® ActiveX®データオブジェクト (多次元) (ADO MD) を使用すると、Microsoft Visual Basic®、Microsoft Visual C++®などの言語から多次元データに簡単にアクセスできます。 ADO MD により、Microsoft ActiveX® Data Objects (ADO) が拡張され、 [CubeDef](../../reference/ado-md-api/cubedef-object-ado-md.md) オブジェクトや [Cellset](../../reference/ado-md-api/cellset-object-ado-md.md) オブジェクトなどの多次元データに固有のオブジェクトが含まれるようになります。 ADO MD を使用すると、多次元スキーマの参照、キューブのクエリ、および結果の取得を行うことができます。  
  
 ADO と同様に、ADO MD は、基になる OLE DB プロバイダーを使用してデータにアクセスします。 ADO MD を使用するには、プロバイダーが OLAP 仕様の OLE DB で定義されている多次元データプロバイダー (.MDP) である必要があります。 .MDP は、表形式のビューではなく、多次元ビューにデータを表示します。これは、表形式のデータプロバイダー (TDP) がデータを提示する方法です。 プロバイダーでサポートされている特定の構文と動作の詳細については、OLAP OLE DB プロバイダーのドキュメントを参照してください。  
  
 このドキュメントでは、Visual Basic プログラミング言語に関する実用的な知識と、ADO および OLAP に関する一般的な知識を前提としています。 詳細については、 [ADO プログラマーズガイド](../ado-programmer-s-guide.md) および [オンライン分析処理 (OLAP) の OLE DB](/previous-versions/windows/desktop/ms717005(v=vs.85))を参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [多次元スキーマとデータの概要](./overview-of-multidimensional-schemas-and-data.md)  
  
-   [多次元データの操作](./working-with-multidimensional-data.md)  
  
-   [ADO MD と ADO の併用](./using-ado-with-ado-md.md)  
  
-   [ADO MD を使用したプログラミング](./programming-with-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [ADO MD オブジェクトモデル](../../reference/ado-md-api/ado-md-object-model.md)   
 [ADO プログラマーズガイド](../ado-programmer-s-guide.md)   
 [データ定義言語およびセキュリティ用の ADO 拡張機能 (ADOX)](../extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [多次元スキーマとデータの概要](./overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD を使用したプログラミング](./programming-with-ado-md.md)   
 [ADO MD での ADO の使用](./using-ado-with-ado-md.md)   
 [多次元データの操作](./working-with-multidimensional-data.md)