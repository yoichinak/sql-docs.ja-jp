---
description: CacheSize を使用する
title: CacheSize | を使用するMicrosoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: rothja
ms.author: jroth
ms.openlocfilehash: 31c9b1dd1ccc3ef61b120bf3d075b81fc34c0eb6
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100032284"
---
# <a name="using-cachesize"></a>CacheSize を使用する
プロバイダーからローカルメモリに一度に取得するレコードの数を制御するには、 **CacheSize** プロパティを使用します。 たとえば、 **CacheSize** が10の場合、最初に **レコードセット** オブジェクトを開いた後、プロバイダーは最初の10個のレコードをローカルメモリに取得します。 **レコードセット** オブジェクト内を移動すると、プロバイダーはローカルメモリバッファーからデータを返します。 キャッシュ内の最後のレコードを越えて移動すると、プロバイダーは、次の10個のレコードをデータソースからキャッシュに取得します。  
  
> [!NOTE]
>  **CacheSize** は、**最大 Open Rows** プロバイダー固有のプロパティ ( **Recordset** オブジェクトの **Properties** コレクション内) に基づいています。 **CacheSize** は、**最大開い** ている行よりも大きい値に設定することはできません。 プロバイダーによって開くことができる行の数を変更するには、 **[最大開い** ている行数] を設定します。  
  
 **CacheSize** の値は、**レコードセット** オブジェクトの有効期間中に調整できますが、この値を変更しても、後でデータソースからデータを取得した後のキャッシュ内のレコードの数に影響します。 プロパティ値だけを変更しても、キャッシュの現在の内容は変更されません。  
  
 取得するレコードの数が **CacheSize** よりも小さい場合、プロバイダーは残りのレコードを返し、エラーは発生しません。  
  
 **CacheSize** 設定0は許可されていないため、エラーが返されます。  
  
 キャッシュから取得したレコードには、他のユーザーがソースデータに対して行った同時変更は反映されません。 キャッシュされたすべてのデータを強制的に更新するには、 [Resync](../../../ado/reference/ado-api/resync-method.md) メソッドを使用します。  
  
 **CacheSize** が1より大きい値に設定されている場合、ナビゲーションメソッド ([Move](../../../ado/reference/ado-api/move-method-ado.md)、 [MoveFirst、MoveLast、MoveNext、および MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) は、レコードの取得後に削除が発生すると、削除されたレコードに移動する可能性があります。 最初のフェッチの後、削除された行からデータ値にアクセスしようとするまで、その後の削除はデータキャッシュに反映されません。 ただし、 **CacheSize** を1に設定すると、削除された行をフェッチできないため、この問題は解消されます。
