---
description: Microsoft OLE DB Provider for Microsoft Active Directory サービス
title: Microsoft OLE DB Provider for Microsoft Active Directory Service |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
author: rothja
ms.author: jroth
ms.openlocfilehash: 08d945b101ac91300793920e3e01ea0a9619b372
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991053"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Microsoft OLE DB Provider for Microsoft Active Directory サービス
Active Directory サービスインターフェイス (ADSI) プロバイダーにより、ADO は、ADSI を介して異種のディレクトリサービスに接続できます。 これにより、ADO アプリケーションは、LDAP に準拠しているディレクトリサービスと Novell ディレクトリサービスに加えて、Microsoft Windows NT 4.0 および Microsoft Windows 2000 ディレクトリサービスへの読み取り専用アクセスを提供します。 ADSI 自体はプロバイダーモデルに基づいているため、別のディレクトリへのアクセスを提供する新しいプロバイダーがあると、ADO アプリケーションはシームレスにアクセスできるようになります。 ADSI プロバイダーは、フリースレッドで、Unicode が有効になっています。  
  
## <a name="connection-string-parameters"></a>接続文字列パラメーター  
 このプロバイダーに接続するには、 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)プロパティの**provider**引数を次のように設定します。  
  
```vb
ADSDSOObject  
```  
  
 [プロバイダー](../../reference/ado-api/provider-property-ado.md)プロパティを読み取ると、この文字列も返されます。  
  
## <a name="typical-connection-string"></a>一般的な接続文字列  
 このプロバイダーの一般的な接続文字列は次のとおりです。  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 文字列は、次のキーワードで構成されています。  
  
|キーワード|説明|  
|-------------|-----------------|  
|**プロバイダー**|Active Directory サービスの OLE DB プロバイダーを指定します。|  
|**[ユーザー ID]**|ユーザー名を指定します。 このキーワードを省略した場合は、現在のログオンが使用されます。|  
|**パスワード**|ユーザーのパスワードを指定します。 このキーワードが省略されている場合は。 その後、現在のログオンが使用されます。|  
  
> [!NOTE]
>  Windows 認証をサポートするデータソースプロバイダーに接続する場合は、接続文字列にユーザー ID とパスワードの情報ではなく、 **Trusted_Connection = yes** または **INTEGRATED Security = SSPI** を指定する必要があります。  
  
## <a name="command-text"></a>コマンド テキスト  
 次の構文では、4つの要素から構成されるコマンドテキスト文字列がプロバイダーによって認識されます。  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|[値]|説明|  
|-----------|-----------------|  
|*ルート*|検索を開始する **ADsPath** オブジェクト (つまり、検索のルート) を示します。|  
|*Assert*|RFC 1960 形式の検索フィルターを示します。|  
|*属性*|返される属性のコンマ区切りのリストを示します。|  
|*スコープ*|省略可能。 検索のスコープを指定する **文字列** 。 以下のいずれかを指定できます。<br /><br /> -Base-ベースオブジェクト (検索のルート) のみを検索します。<br />-OneLevel-1 つのレベルのみを検索します。<br />-Subtree-サブツリー全体を検索します。|  
  
 次に例を示します。  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 プロバイダーは、コマンドテキストの SQL SELECT もサポートしています。 次に例を示します。  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>解説  
 プロバイダーは、ストアドプロシージャ呼び出しまたは単純なテーブル名を受け入れません (たとえば、 [CommandType](../../reference/ado-api/commandtype-property-ado.md) プロパティは常に **adcmdtext**になります)。 コマンドテキスト要素の詳細な説明については、Active Directory サービスインターフェイスのドキュメントを参照してください。  
  
## <a name="recordset-behavior"></a>レコードセットの動作  
 次の表は、このプロバイダーを使用して開かれた [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトで使用できる機能を示しています。 静的カーソルの種類 (**Adopenstatic**) のみを使用できます。  
  
 プロバイダー構成の**レコードセット**の動作の詳細については[、サポート](../../reference/ado-api/supports-method.md)メソッドを実行し、**レコードセット**の[properties](../../reference/ado-api/properties-collection-ado.md)コレクションを列挙して、プロバイダー固有の動的プロパティが存在するかどうかを判断します。  
  
 **標準の ADO レコードセットプロパティの可用性:**  
  
|プロパティ|可用性|  
|--------------|------------------|  
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|読み取り/書き込み|  
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|読み取り/書き込み|  
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|読み取り専用|  
|[BOF](../../reference/ado-api/bof-eof-properties-ado.md)|読み取り専用|  
|[ブックマーク](../../reference/ado-api/bookmark-property-ado.md)|読み取り/書き込み|  
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|読み取り/書き込み|  
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|常に **Aduseserver**|  
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|常に **Adopenstatic**|  
|[EditMode](../../reference/ado-api/editmode-property.md)|常に **adEditNone**|  
|[EOF](../../reference/ado-api/bof-eof-properties-ado.md)|読み取り専用|  
|[Assert](../../reference/ado-api/filter-property.md)|読み取り/書き込み|  
|[LockType](../../reference/ado-api/locktype-property-ado.md)|読み取り/書き込み|  
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|利用不可|  
|[数](../../reference/ado-api/maxrecords-property-ado.md)|読み取り/書き込み|  
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|読み取り専用|  
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|読み取り/書き込み|  
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|読み取り専用|  
|[ソース](../../reference/ado-api/source-property-ado-recordset.md)|読み取り/書き込み|  
|[State](../../reference/ado-api/state-property-ado.md)|読み取り専用|  
|[状態](../../reference/ado-api/status-property-ado-recordset.md)|読み取り専用|  
  
 **標準の ADO レコードセットメソッドの可用性:**  
  
|方法|利用可能か|  
|------------|----------------|  
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|いいえ|  
|[キャンセル](../../reference/ado-api/cancel-method-ado.md)|いいえ|  
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|いいえ|  
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|いいえ|  
|[複製](../../reference/ado-api/clone-method-ado.md)|はい|  
|[閉じる](../../reference/ado-api/close-method-ado.md)|はい|  
|[削除](../../reference/ado-api/delete-method-ado-recordset.md)|いいえ|  
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|はい|  
|[移動](../../reference/ado-api/move-method-ado.md)|はい|  
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|  
|[MoveLast](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|  
|[MoveNext](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|  
|[MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|  
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)|はい|  
|[[ファイル]](../../reference/ado-api/open-method-ado-recordset.md)|はい|  
|[Requery](../../reference/ado-api/requery-method.md)|はい|  
|[再同期](../../reference/ado-api/resync-method.md)|はい|  
|[サポート](../../reference/ado-api/supports-method.md)|はい|  
|[アップデート](../../reference/ado-api/update-method.md)|いいえ|  
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|いいえ|  
  
 ADSI とプロバイダーの詳細については、Active Directory サービスインターフェイスに関するドキュメントを参照するか、ADSI の Web ページを参照してください。  
  
## <a name="see-also"></a>参照  
 [CommandType プロパティ (ADO)](../../reference/ado-api/commandtype-property-ado.md)   
 [ConnectionString プロパティ (ADO)](../../reference/ado-api/connectionstring-property-ado.md)   
 [Properties コレクション (ADO)](../../reference/ado-api/properties-collection-ado.md)   
 [Provider プロパティ (ADO)](../../reference/ado-api/provider-property-ado.md)   
 [Recordset オブジェクト (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [Supports メソッド](../../reference/ado-api/supports-method.md)