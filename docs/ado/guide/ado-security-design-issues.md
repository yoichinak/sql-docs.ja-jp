---
description: ADO のセキュリティデザイン機能
title: ADO セキュリティ設計の問題 |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
author: rothja
ms.author: jroth
ms.openlocfilehash: 1d485dbb17075033add5e3ee93dbcf9b6bf44e65
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991223"
---
# <a name="ado-security-design-features"></a>ADO のセキュリティデザイン機能
以下のセクションでは、ActiveX データオブジェクト (ADO) 2.8 以降のセキュリティ設計機能について説明します。 これらの変更は、セキュリティを強化するために ADO 2.8 で行われました。 Windows Vista の Windows DAC 6.0 に含まれる ADO 6.0 は、windows XP および Windows Server 2003 の MDAC 2.8 に含まれていた ADO 2.8 と機能的には同等です。 このトピックでは、ADO 2.8 以降でアプリケーションを最適に保護する方法について説明します。

> [!IMPORTANT]
>  以前のバージョンの ADO からアプリケーションを更新する場合は、運用環境以外のコンピューターで更新されたアプリケーションをテストしてから、顧客にデプロイすることをお勧めします。 これにより、更新されたアプリケーションを展開する前に、互換性の問題を認識していることを確認できます。

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer のファイルアクセスのシナリオ
 次の機能は、Internet Explorer のスクリプト化された Web ページで ADO 2.8 以降が使用される場合の動作に影響します。

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>ユーザーにアラートを通知するために使用される、変更および強化されたセキュリティ警告メッセージボックス
 ADO 2.7 以前のバージョンでは、スクリプト化された Web ページが信頼されていないプロバイダーから ADO コードを実行しようとすると、次の警告メッセージが表示されます。

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 ADO 2.8 以降では、上記のメッセージは表示されなくなりました。 代わりに、次のメッセージがこのコンテキストに表示されます。

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 上記のメッセージを使用すると、ユーザーは情報に基づいた決定を行うことができますが、どちらの方法でも結果を把握できます。

-   ユーザーがサイトを信頼している場合は、[OK] をクリックすると、すべてのディスクセーフコード (このトピックで後述するディスクアクセス可能な Api の例外を含むすべての ADO メソッドとプロパティ) が実行され、ブラウザーウィンドウで実行できるようになります。

-   ユーザーがサイトを信頼していない場合、[キャンセル] をクリックすると、データアクセスの ADO コードが実行され、その全体が実行されます。

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>ディスクからアクセス可能なコードが、信頼済みサイトに限定されるようになりました
 ADO 2.8 では、ローカルコンピューター上のファイルの読み取りまたは書き込みの可能性を公開する可能性がある制限付きの Api セットの機能を制限する追加のデザイン変更が行われました。 Internet Explorer の実行時に安全性に関してさらに制限されている API メソッドを次に示します。

-   ADO **ストリーム** オブジェクトの場合は、 [LoadFromFile](../reference/ado-api/loadfromfile-method-ado.md) または [SaveToFile](../reference/ado-api/savetofile-method.md) メソッドが使用されている場合はです。

-   ADO **レコードセット** オブジェクトの場合、 [Save](../reference/ado-api/save-method.md) メソッドまたは [Open](../reference/ado-api/open-method-ado-recordset.md) メソッドがある場合 ( **adcmdfile** オプションが設定されている場合や、 [Microsoft OLE DB 永続化プロバイダー (mspersist)](./appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) が使用されている場合など)。

 これらの制限されたディスクアクセス関数のセットについては、これらのメソッドを使用するコードが Internet Explorer で実行されている場合に、ADO 2.8 以降で次の動作が発生します。

-   コードを提供したサイトが以前に信頼済みサイトゾーンの一覧に追加されている場合は、コードがブラウザーで実行され、ローカルファイルへのアクセスが許可されます。

-   サイトが信頼済みサイトゾーンの一覧に表示されない場合、コードはブロックされ、ローカルファイルへのアクセスは拒否されます。

    > [!NOTE]
    >  ADO 2.8 以降では、信頼済みサイトゾーンの一覧にサイトを追加することは、ユーザーには通知されず、推奨されません。 したがって、信頼済みサイトの一覧の管理は、ローカルファイルシステムへのアクセスを必要とする Web サイトベースのアプリケーションを展開またはサポートしているユーザーの責任です。

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>レコードセットオブジェクトの ActiveCommand プロパティへのアクセスがブロックされました
 Internet Explorer で実行されている場合、ADO 2.8 では、アクティブな**レコードセット**オブジェクトの[activecommand](../reference/ado-api/activecommand-property-ado.md)プロパティへのアクセスがブロックされるようになり、エラーが返されるようになりました。 このエラーは、ページが信頼済みサイトの一覧に登録されている Web サイトからのものであるかどうかに関係なく発生します。

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>OLE DB プロバイダーと統合セキュリティの処理の変更
 ADO 2.7 およびそれ以前のバージョンを確認しながら、潜在的なセキュリティの問題と懸念が発生した場合は、次のシナリオが検出されました。

 場合によっては、統合セキュリティ [DBPROP_AUTH_INTEGRATED](/previous-versions/windows/desktop/ms712973(v=vs.85)) プロパティをサポートする OLE DB プロバイダーは、スクリプト化された Web ページが ADO Connection オブジェクトを再利用して、ユーザーの現在のログイン資格情報を使用して、他のサーバーに誤って接続することを許可する可能性があります。 これを回避するために、ADO 2.8 以降では、統合セキュリティを提供するかどうかを選択した方法に応じて OLE DB プロバイダーが処理されます。

 信頼済みサイトゾーンの一覧に表示されているサイトから読み込まれた Web ページの場合、次の表に、各ケースで ADO 2.8 以降で ADO 接続をどのように管理するかを示します。

|ユーザー認証のための IE 設定、ログオン|プロバイダーが "統合セキュリティ" をサポートし、UID と PWD が指定されている (SQLOLEDB)|プロバイダーは "統合セキュリティ" (JOLT、MSDASQL、MSPersist) をサポートしていません|プロバイダーは "統合セキュリティ" をサポートしていて、SSPI に設定されています (UID/PWD が指定されていません)|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|現在のユーザー名とパスワードで自動的にログオンする|接続の許可|接続の許可|接続の許可|
|ユーザー名とパスワードを入力してログオンする|接続の許可|接続の失敗|接続の失敗|
|イントラネット ゾーンでのみ自動的にログオンする|接続の許可|ユーザーにセキュリティ警告を表示する|ユーザーにセキュリティ警告を表示する|
|匿名でログオンする|接続の許可|接続の失敗|接続の失敗|

 セキュリティの警告が表示された場合は、メッセージボックスにユーザーに通知します。

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 上記のメッセージを使用すると、ユーザーはより詳細な情報を確認し、それに従って処理を進めることができます。

> [!NOTE]
>  信頼されていないサイト (つまり、[信頼済みサイト] ゾーンリストに一覧表示されていないサイト) の場合、プロバイダーが信頼できない場合 (このセクションで既に説明したように)、ユーザーには、1行に2つのセキュリティ警告が表示され、unsafe プロバイダーに関する警告が表示されます。 ユーザーが最初の警告に対して [OK] をクリックすると、前の表で説明されている Internet Explorer の設定と応答動作のコードが実行されます。

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>ADO 接続文字列でパスワードテキストを返すかどうかを制御する
 ADO **Connection**オブジェクトの[ConnectionString](../reference/ado-api/connectionstring-property-ado.md)プロパティの値を取得しようとすると、次のイベントが発生します。

1.  接続が開いている場合は、基になる OLE DB プロバイダーに初期化呼び出しが行われ、接続文字列が取得されます。

2.  [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](/previous-versions/windows/desktop/ms714905(v=vs.85))プロパティの OLE DB プロバイダーの設定によっては、パスワードが返されるその他の接続文字列情報と共に使用されます。

 たとえば、ADO Connection の動的プロパティ永続化 **セキュリティ情報** が **True**に設定されている場合、パスワード情報は返された接続文字列に含まれます。 それ以外の場合、基になるプロバイダーがプロパティを **False** に設定している場合 (たとえば、SQLOLEDB プロバイダーを使用した場合)、返された接続文字列ではパスワード情報が省略されます。

 ADO アプリケーションコードを使用してサードパーティ (Microsoft 以外の) OLE DB プロバイダーを使用している場合は、 **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** プロパティがどのように実装されているかを確認し、ado 接続文字列でパスワード情報を含めることが許可されているかどうかを確認できます。

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>レコードセットまたはストリームの読み込み時または保存時にファイル以外のデバイスを確認する
 ADO 2.7 以前では、ファイルベースのデータの読み取りと書き込みに使用された、 [Open](../reference/ado-api/open-method-ado-recordset.md) や [Save](../reference/ado-api/save-method.md) などのファイル入出力操作により、ディスクベースでないファイルの種類を指定した URL またはファイル名を使用できる場合がありました。 たとえば、LPT1、COM2、PRN.TXT、AUX は、特定のを使用して、システム上のプリンターと補助デバイス間の入出力のエイリアスとして使用できます。

 ADO 2.8 以降では、この機能は更新されています。 **レコードセット**と**ストリーム**オブジェクトを開いたり保存したりするために、ADO では、URL またはファイル名に指定されている入力デバイスまたは出力デバイスが実際のファイルであることを確認するために、ファイルの種類のチェックを実行するようになりました。

> [!NOTE]
>  このセクションで説明するファイルの種類のチェックは、Windows 2000 以降にのみ適用されます。 Windows 98 など、以前の Windows リリースで ADO 2.8 以降が実行されている場合には適用されません。