---
description: アドレス帳のコマンド ボタン
title: アドレス帳のコマンドボタン |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
author: rothja
ms.author: jroth
ms.openlocfilehash: d234732b90fdd89b6f0e41efe1762bb3a99ddde2
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724853"
---
# <a name="address-book-command-buttons"></a>アドレス帳のコマンド ボタン
アドレス帳アプリケーションには、次のコマンドボタンが含まれています。  
  
-   クエリをデータベースに送信するための [ **検索** ] ボタン。  
  
-   新しい検索を開始する前にテキストボックスをクリアする **クリア** ボタン。  
  
-   従業員レコードの変更を保存するための [ **更新プロファイル** ] ボタン。  
  
-   変更を破棄するための **[変更のキャンセル** ] ボタン。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="find-button"></a>[検索] ボタン  
 [ **検索** ] ボタンをクリックすると、VBScript の Find_OnClick サブプロシージャがアクティブ化され、SQL クエリが作成されて送信されます。 このボタンをクリックすると、データグリッドが設定されます。  
  
## <a name="building-the-sql-query"></a>SQL クエリの作成  
 Find_OnClick Sub プロシージャの最初の部分では、グローバル SQL SELECT ステートメントにテキスト文字列を追加することによって、1つの句で SQL クエリを作成します。 まず、変数に、 `myQuery` データソーステーブルのすべてのデータ行を要求する SQL SELECT ステートメントを設定します。 次に、サブプロシージャは、ページ上の4つの入力ボックスのそれぞれをスキャンします。  
  
 このプログラムでは、SQL ステートメントの作成に使用されている単語が使用されるため、 `like` クエリは完全一致ではなく、部分文字列検索になります。  
  
 たとえば、[ **姓** ] ボックスにエントリ "" "が含まれていて、[ **タイトル** ] ボックスに" プログラムマネージャー "というエントリが含まれている場合、SQL ステートメント (の値) は次の `myQuery` ようになります。  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 クエリが成功した場合、"Berger" などのテキストを含む姓を持つすべての人と、"プログラムマネージャー" (プログラムマネージャー、高度なテクノロジなど) という語を含むタイトルが HTML データグリッドに表示されます。  
  
## <a name="preparing-and-sending-the-query"></a>クエリの準備と送信  
 Find_OnClick サブプロシージャの最後の部分は、2つのステートメントで構成されます。 最初のステートメントは、RDS の [SQL](../../reference/rds-api/sql-property.md) プロパティを割り当て [ます。DataControl](../../reference/rds-api/datacontrol-object-rds.md) オブジェクトは、動的に構築された SQL クエリと同じです。 2番目のステートメントは、RDS を発生させ **ます。DataControl** object ( `DC1` ) を実行してデータベースを照会し、グリッドにクエリの新しい結果を表示します。  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>[プロファイルの更新] ボタン  
 [ **プロファイルの更新** ] ボタンをクリックすると、VBScript Update_OnClick サブプロシージャがアクティブ化され、RDS が実行さ [れます。DataControl](../../reference/rds-api/datacontrol-object-rds.md) オブジェクトの ( `DC1` ) [SubmitChanges](../../reference/rds-api/submitchanges-method-rds.md) メソッドと [Refresh](../../reference/rds-api/refresh-method-rds.md) メソッド。  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 が実行されると、 `DC1.SubmitChanges` リモートデータサービスはすべての更新情報をパッケージ化し、HTTP 経由でサーバーに送信します。 更新プログラムがすべて-または何もありません。更新プログラムの一部が正常に実行されなかった場合、変更は一切行われず、ステータスメッセージが返されます。 `DC1.Refresh` リモートデータサービスと **SubmitChanges** した後には必要ありませんが、最新のデータが確保されます。  
  
## <a name="cancel-changes-button"></a>[変更の取り消し] ボタン  
 **[変更のキャンセル]** をクリックすると、RDS を実行する VBScript Cancel_OnClick サブプロシージャがアクティブ化され[ます。DataControl](../../reference/rds-api/datacontrol-object-rds.md)オブジェクトの ( `DC1)` [CancelUpdate](../../reference/rds-api/cancelupdate-method-rds.md)メソッド)。  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 `DC1.CancelUpdate`を実行すると、前回のクエリまたは更新以降にユーザーがデータグリッドの employee レコードに対して行ったすべての編集が破棄されます。 元の値を復元します。  
  
## <a name="see-also"></a>参照  
 [アドレス帳のナビゲーションボタン](./address-book-navigation-buttons.md)   
 [DataControl オブジェクト (RDS)](../../reference/rds-api/datacontrol-object-rds.md)