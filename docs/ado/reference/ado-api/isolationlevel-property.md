---
description: IsolationLevel プロパティ
title: IsolationLevel Property |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
author: rothja
ms.author: jroth
ms.openlocfilehash: 91945d36801005fb7f7c4dbcc9df5a464c6e4fa4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990773"
---
# <a name="isolationlevel-property"></a>IsolationLevel プロパティ
[接続](./connection-object-ado.md)オブジェクトの分離レベルを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 [IsolationLevelEnum](./isolationlevelenum.md)値を設定または返します。 既定値は **adXactReadCommitted**です。  
  
## <a name="remarks"></a>解説  
 **接続**オブジェクトの分離レベルを設定するには、 **IsolationLevel**プロパティを使用します。 この設定は、次に [BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) メソッドを呼び出したときまで有効になりません。 要求した分離レベルが使用できない場合、プロバイダーは、 **IsolationLevel** プロパティを更新せずに、次に高い分離レベルを返すことができます。  
  
 **IsolationLevel**プロパティは読み取り/書き込み可能です。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況** クライアント側の **接続** オブジェクトで使用する場合、 **IsolationLevel** プロパティは **adXactUnspecified**にのみ設定できます。 ユーザーはクライアント側キャッシュで切断された **レコードセット** オブジェクトを操作しているため、マルチユーザーの問題が発生する可能性があります。 たとえば、2人のユーザーが同じレコードを更新しようとした場合、リモートデータサービスは、最初にレコードを更新するユーザーに "win" を許可します。 2番目のユーザーの更新要求は、エラーで失敗します。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [IsolationLevel と Mode プロパティの例 (VB)](./isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel と Mode プロパティの例 (VC + +)](./isolationlevel-and-mode-properties-example-vc.md)