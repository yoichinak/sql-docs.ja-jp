---
description: 各リリースの ADO 機能
title: ADO 履歴 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: rothja
ms.author: jroth
ms.openlocfilehash: 238fe03736fbc295622fa42924f3249f28b9a527
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980813"
---
# <a name="ado-features-for-each-release"></a>各リリースの ADO 機能

このトピックでは、ADO、ADO MD、および ADOX の各リリースで導入された新機能について説明します。

## <a name="ado-60"></a>ADO 6.0

ADO 6.0 は、windows Data Access Components (Windows DAC) 6.0 の一部として、Windows Vista に含まれています。 Ado 6.0 は、機能的には ADO 2.8 と同等です。

## <a name="ado-28"></a>ADO 2.8

ADO 2.8 は、Microsoft Data Access Components (MDAC) 2.8 の一部として、Windows XP および Windows Server 2003 に含まれていました。 また、MDAC 2.8 の再頒布可能バージョンも利用できます。この再頒布可能バージョンは、Windows 2000 にのみインストールする必要があることに注意してください。 ADO 2.8 では、いくつかのセキュリティ関連の問題に対処しています。

*ハードドライブへのアクセスは、信頼済みゾーンの外部では許可されていません。*
信頼できないサイトを含むクロスドメインスクリプトでは、次の操作が無効になっています: **Recordset.Save** **LoadFromFile** **、Stream、** および**recordset. Open**。 **Adcmdfile**フラグまたは Microsoft OLE DB 永続化プロバイダー (mspersist) と組み合わせて使用します。

**Recordset. Open** _、_**recordset. Save** _、LoadFromFile_**、** _および_**stream**は、_物理ファイルに対してのみ動作_します。        
これらのメソッドは、ファイルハンドルが物理ファイルのみを指していることを確認するようになりました。

**Recordset. ActiveCommand**_は、HTML/ASP ページから呼び出されたときにエラーを返し_ます。  
これにより、 **コマンド** オブジェクトが誤用されるのを防ぐことができます。

入れ子になった**Shape**コマンド_によって返される_**レコードセット**_の数__には上限があります。_        
入れ子になった shape コマンドで、最大で512の **レコードセット**が返されるようになりました。 これは、 **Shape** コマンドをどの深さでも入れ子にできなくなることを意味します。 代わりに、各コマンドの結果が単一の (子) **レコードセット**になる場合、最大レベルの深さは512です。 任意のレベルで、 **Shape** コマンドが複数の **レコードセット**を返す場合、深さの最大レベルは512未満になります。

## <a name="ado-27"></a>ADO 2.7

*64 ビットプラットフォームのサポート* ADO 2.7 では、64ビットプロセッサのサポートが導入されています。

## <a name="ado-26"></a>ADO 2.6

**CUBDEF**ADO_2.6 以降で_は、 [UniqueName プロパティ (ADO MD)](../reference/ado-md-api/uniquename-property-ado-md.md)で指定されている一意の名前を使用して ADO MD オブジェクトを取得できます。   親オブジェクトの名前を把握しておく必要はありません。また、スキーマオブジェクトを取得するために親コレクションを設定する必要もありません。 「 [Getschemaobject メソッド (ADO MD)](../reference/ado-md-api/getschemaobject-method-ado-md.md)」を参照してください。

*コマンドストリーム***Command**オブジェクトは、 **CommandText**プロパティを使用する代わりに、ストリーム形式のコマンドをサポートしています。 [Commandstream プロパティ (ADO)](../reference/ado-api/commandstream-property-ado.md)を使用して、XML テンプレートまたはアップデートグラムを、Microsoft OLE DB Provider for SQL Server と共に**コマンド**入力として指定できます。

**言語**_プロパティ_の 
 [言語](../reference/ado-api/dialect-property.md)は、文字列またはストリームを解析するためにプロバイダーが使用する構文と一般規則を定義する新しいプロパティです。  

**Command.Exeかわいらしい**_メソッド_ADO**コマンド**オブジェクトの[Execute メソッド](../reference/ado-api/execute-method-ado-command.md)が拡張され、入力と出力にストリームを使用できるようになりました。  

*フィールドの statusvalues***レコードセット**の**フィールド**を変更するときに DB_E_ERRORSOCCURRED エラーが発生した場合は、ADO によって **"status** " プロパティに適切な状態情報が入力され、問題が発生した原因に関する詳細情報がユーザーに表示されるようになります。 「 [Status プロパティ (ADO Field)](../reference/ado-api/status-property-ado-field.md)」を参照してください。

**Namedparameters**_プロパティ_ 
 [namedparameters](../reference/ado-api/namedparameters-property-ado.md)は、プロバイダーが名前付きパラメーターを使用する必要があることを示す**Command**オブジェクトの新しいプロパティです。  

*ストリーム内の結果セット*ADO では、**レコードセット**オブジェクトではなく、**ストリーム**内のデータソースから結果セットを返すことができます。 最新バージョンの Microsoft OLE DB Provider for SQL Server を使用すると、"For XML" クエリを実行することで、プロバイダーから XML の結果を取得できます。 結果セットを受け取る **ストリーム** は、ソースとして "For XML" コマンドを使用して開くことができます。 「 [ストリームへの結果セットの取得」を](./data/retrieving-resultsets-into-streams.md)参照してください。

*単一行の結果セット* ADO **Record** オブジェクトを、プロバイダーから1行のデータを返すコマンド文字列または **コマンド** オブジェクトで開くことができるようになりました。 その結果、MDAC 2.6 プロバイダーのパフォーマンスが向上します。 「 [Open メソッド (ADO Record)](../reference/ado-api/open-method-ado-record.md)」を参照してください。

## <a name="ado-25"></a>ADO 2.5

**レコード**_オブジェクト_ADO 2.5 では、レコード**セット**またはデータプロバイダーの行を表す**レコード**オブジェクト、またはファイルやディレクトリなどの半構造化データをカプセル化するオブジェクトが導入されています。

**Stream** _オブジェクト_ ADO 2.5 では、バイナリデータまたはテキストデータのストリームを表す *および*ストリーム * * オブジェクトも導入されています。

*URL バインド* ADO 2.5 では、接続文字列とコマンドテキストの代わりに URL を使用して、データストアオブジェクトに名前を付けます。 URL は、既存の **接続** および **レコードセット** オブジェクト、および新しい **レコード** および **ストリーム** オブジェクトと共に使用できます。

*URL バインドをサポートするデータプロバイダー* ADO 2.5 では、URL スキームを認識する OLE DB プロバイダーがサポートされています。 これには、Windows 2000 ファイルシステムにアクセスして既存の HTTP スキームを認識する、インターネット公開の OLE DB プロバイダーが含まれます。
