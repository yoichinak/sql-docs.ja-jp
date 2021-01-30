---
description: DefaultDatabase プロパティ
title: DefaultDatabase プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
author: rothja
ms.author: jroth
ms.openlocfilehash: 8cff37ae3bc0940a62e2acc9af3ac6c25d1379a4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99167589"
---
# <a name="defaultdatabase-property"></a>DefaultDatabase プロパティ
[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの既定のデータベースを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 プロバイダーから使用可能なデータベースの名前に評価される **文字列** 値を設定または返します。  
  
## <a name="remarks"></a>コメント  
 **Defaultdatabase** プロパティを使用して、特定の **接続** オブジェクトの既定のデータベースの名前を設定または取得します。  
  
 既定のデータベースが存在する場合、SQL 文字列では、そのデータベース内のオブジェクトにアクセスするために非修飾構文を使用できます。 **Defaultdatabase** プロパティで指定されていないデータベース内のオブジェクトにアクセスするには、目的のデータベース名を使用してオブジェクト名を修飾する必要があります。 接続時に、プロバイダーは既定のデータベース情報を **defaultdatabase** プロパティに書き込みます。 プロバイダーによっては、接続ごとに1つのデータベースしか使用できない場合があります。この場合、 **Defaultdatabase** プロパティを変更することはできません。  
  
 一部のデータソースおよびプロバイダーでは、この機能がサポートされていない場合があり、エラーまたは空の文字列が返されることがあります。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況** このプロパティは、クライアント側の **接続** オブジェクトでは使用できません。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Provider および DefaultDatabase プロパティの例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider および DefaultDatabase プロパティの例 (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
