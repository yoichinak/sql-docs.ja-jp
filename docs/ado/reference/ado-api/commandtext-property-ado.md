---
description: CommandText プロパティ (ADO)
title: CommandText プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
author: rothja
ms.author: jroth
ms.openlocfilehash: c0e7f2e9e346a5379051b101236df186b815aa85
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975193"
---
# <a name="commandtext-property-ado"></a>CommandText プロパティ (ADO)
プロバイダーに対して発行されるコマンドのテキストを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 SQL ステートメント、テーブル名、相対 URL、またはストアドプロシージャの呼び出しなど、プロバイダーコマンドを含む **文字列** 値を取得します。値の設定もできます。 既定値は空の文字列 ("") です。  
  
## <a name="remarks"></a>解説  
 **CommandText**プロパティを使用して、 [command](./command-object-ado.md)オブジェクトによって表されるコマンドのテキストを設定または取得します。 通常、これは SQL ステートメントですが、ストアドプロシージャの呼び出しなど、プロバイダーによって認識される他の種類のコマンドステートメントにすることもできます。 SQL ステートメントは、プロバイダーのクエリプロセッサでサポートされている特定の言語またはバージョンである必要があります。  
  
 **Command**オブジェクトの[準備](./prepared-property-ado.md)されたプロパティが**True**に設定されていて、 **CommandText**プロパティを設定するときに**command**オブジェクトが開いている接続にバインドされている場合、ADO は[Execute](./execute-method-ado-command.md)メソッドまたは[open](./open-method-ado-connection.md)メソッドを呼び出すと、クエリ (つまり、プロバイダーによって格納されるクエリのコンパイル済みの形式) を準備します。  
  
 [CommandType](./commandtype-property-ado.md)プロパティの設定によっては、ADO によって**CommandText**プロパティが変更される場合があります。 いつでも **CommandText** プロパティを読み取り、ADO が実行時に使用する実際のコマンドテキストを確認できます。  
  
 ファイルやディレクトリなどのリソースを指定する相対 URL を設定または取得するには、 **CommandText** プロパティを使用します。 リソースは、絶対 URL によって明示的に指定された場所、または開いている [接続](./connection-object-ado.md) オブジェクトによって暗黙的に指定された場所を基準としています。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery メソッド](./requery-method.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)