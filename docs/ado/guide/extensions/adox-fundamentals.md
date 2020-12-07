---
description: ADOX の基礎
title: ADOX の基礎 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX, fundamentals
ms.assetid: 954476fc-5f72-4ada-ace5-d9acb27d18f8
author: rothja
ms.author: jroth
ms.openlocfilehash: 6bb64cb60584444ba845ef1464fb07886c5db782
ms.sourcegitcommit: 9774e2cb8c07d4f6027fa3a5bb2852e4396b3f68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92098631"
---
# <a name="adox-fundamentals"></a>ADOX の基礎
Microsoft® ActiveX® Data Objects Extensions for Data Definition Language and Security (ADOX) は、ADO オブジェクトとプログラミングモデルの拡張機能です。 ADOX には、スキーマの作成と変更、およびセキュリティのためのオブジェクトが含まれています。 スキーマ操作に対するオブジェクトベースのアプローチであるため、ネイティブ構文の違いに関係なく、さまざまなデータソースに対して機能するコードを記述できます。  
  
 ADOX は、中核となる ADO オブジェクトに関連するライブラリです。 テーブルやプロシージャなどのスキーマオブジェクトを作成、変更、および削除するための追加のオブジェクトを公開します。 また、ユーザーとグループを管理したり、オブジェクトに対する権限を許可および取り消すためのセキュリティオブジェクトも含まれます。  
  
 開発ツールで ADOX を使用するには、ADOX タイプライブラリへの参照を設定する必要があります。 ADOX ライブラリの説明は、"Microsoft ADO Ext for DDL and Security" です。 ADOX ライブラリファイル名は Msadox.dll、プログラム ID (ProgID) は "ADOX" です。 ライブラリへの参照を確立する方法の詳細については、開発ツールのドキュメントを参照してください。  
  
 Microsoft Jet 用の Microsoft OLE DB プロバイダーデータベースエンジンは、ADOX を完全にサポートしています。 データプロバイダーによっては、ADOX の特定の機能がサポートされない場合があります。  
  
 このドキュメントでは、Microsoft® Visual Basic®プログラミング言語と ADO に関する一般的な知識に関する実用的な知識があることを前提としています。 ADO の詳細については、「 [Ado プログラマーズガイド](../ado-programmer-s-guide.md)」を参照してください。 ADOX の概要については、次のトピックを参照してください。  
  
-   [ADOX オブジェクト モデル](../../reference/adox-api/adox-object-model.md)  
  
-   [ADOX オブジェクト](../../reference/adox-api/adox-objects.md)  
  
-   [ADOX のコレクション](../../reference/adox-api/adox-collections.md)  
  
-   [ADOX のプロパティ](../../reference/adox-api/adox-properties.md)  
  
-   [ADOX のメソッド](../../reference/adox-api/adox-methods.md)  
  
-   [ADOX の例](../../reference/adox-api/adox-code-examples.md)  
  
## <a name="see-also"></a>参照  
 [ADOX API リファレンス](../../reference/adox-api/adox-object-model.md?view=sql-server-ver15)   
 [ADOX のコード例](../../reference/adox-api/adox-code-examples.md)   
 [ADOX コレクション](../../reference/adox-api/adox-collections.md)   
 [ADOX 列挙型定数](../../reference/adox-api/adox-enumerated-constants.md)   
 [ADOX のメソッド](../../reference/adox-api/adox-methods.md)   
 [ADOX オブジェクトモデル](../../reference/adox-api/adox-object-model.md)   
 [ADOX オブジェクト](../../reference/adox-api/adox-objects.md)   
 [ADOX のプロパティ](../../reference/adox-api/adox-properties.md)   
 [ADO (多次元) (ADO MD)](../multidimensional/ado-multidimensional-ado-md.md)   
 [ADO プログラマー ガイド](../ado-programmer-s-guide.md)
