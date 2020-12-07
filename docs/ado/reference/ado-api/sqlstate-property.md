---
description: SQLState プロパティ
title: SQLState プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
author: rothja
ms.author: jroth
ms.openlocfilehash: bbc849f19c91f7b2387df5e0e71b3455efa0db09
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988863"
---
# <a name="sqlstate-property"></a>SQLState プロパティ
指定された [エラー](./error-object.md) オブジェクトの SQL 状態を示します。  
  
## <a name="return-value"></a>戻り値  
 は、ANSI SQL 標準に従った5文字の **文字列** 値を返し、エラーコードを示します。  
  
## <a name="remarks"></a>解説  
 SQL ステートメントの処理中にエラーが発生した場合にプロバイダーが返す5文字のエラーコードを読み取るには、 **SQLState** プロパティを使用します。 たとえば、Microsoft SQL Server データベースを使用して Microsoft OLE DB Provider for ODBC を使用すると、odbc からの SQL 状態エラーコードが生成されます。これは、ODBC に固有のエラーや、Microsoft SQL Server から発生したエラーに基づいて行われ、ODBC エラーにマップされます。 これらのエラーコードは ANSI SQL 標準に記載されていますが、データソースによって実装方法が異なる場合があります。  
  
## <a name="applies-to"></a>適用対象  
 [Error オブジェクト](./error-object.md)  
  
## <a name="see-also"></a>参照  
 [Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)