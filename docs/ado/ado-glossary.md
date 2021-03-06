---
description: ADO 用語集の用語
title: ADO 用語集の用語 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, glossary
ms.assetid: b0478836-4123-4357-969a-c5784fc28be5
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a79a16b0fe5f0514b2d90333fcbe99e8e5b5023
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100031054"
---
# <a name="ado-glossary-terms"></a>ADO 用語集の用語
このトピックでは、ADO に関連する用語を定義します。

## <a name="a"></a>A
 絶対 URL インターネットまたはイントラネット上に存在するリソースの場所を指定する完全修飾 URL です。 「 *Url* と *相対 url*」も参照してください。

 ActiveX コントロールの自己登録、つまり、デザイン時または実行時にビジュアル要素を持つことが多い、インプロセス COM コンポーネント。 ActiveX コントロールには、Microsoft Internet Explorer などのアクティブなドキュメントコンテナーと通信する機能もあります。

 ADISAPI (高度なデータインターネットサーバーアプリケーションプログラミングインターフェイス) 解析、オートメーションコントロール、レコードセットマーシャリング、および MIME パッケージ化を提供する ISAPI DLL。 ADISAPI コンポーネントは、インターネットインフォメーションサービス (IIS) によって提供される API を介して機能します。 「 *ISAPI*」も参照してください。

 クエリ内の集計関数。 COUNT、AVG、STDEV などの関数は、テーブルの列のすべての行を使用して値を計算します。 式の作成とプログラミングでは、SQL 集計関数 (上記の3つを含む) とドメイン集計関数を使用して、さまざまな統計情報を確認できます。

 別名 SQL SELECT ステートメント内の列または式に指定する代替名です。多くの場合、短いまたはより意味があります。 たとえば、BobSales は、次の SELECT ステートメントのエイリアスです。 "Select wr" to BobSales from SalesDB "。 別名を使用すると、DataControl オブジェクトの制御バインドに列を動的に割り当てることができます。

 アパートメントスレッド。オブジェクトへのすべての呼び出しが1つのスレッドで発生する COM スレッドモデル。 アパートメントスレッドでは、COM は呼び出しの同期とマーシャリングを行います。 「 *Commddefcom*」も参照してください。

 非同期操作は、操作の完了を待たずに、呼び出し元のプログラムに制御を返す操作です。 操作が完了する前に、コードの実行が続行されます。 「 *同期操作*」も参照してください。

## <a name="b"></a>B
 バインドエントリテーブル内のフィールドと変数の間のマッピング。 ADO Visual C++ 拡張機能では、 **レコードセット** フィールドは C/c + + 変数にマップされます。

 ビット単位の値を他の数値と比較するための数値です。通常は、パラメーターまたは戻り値のオプションにフラグを設定します。 通常、この比較を行うには、 **and や** **or** などのビットごとの論理演算子と、C++ での&#124;Visual Basic し **&** ます。 

 たとえば、ADO **FieldAttributeEnum** 値をビットマスクとして使用して、フィールドの属性を決定することができます。 たとえば、フィールドが更新可能であるかどうかを判断したいとします。 Visual Basic では、次の式を使用してこれをテストできます。`Field.Attributes AND adFldUpdatable`

 結果が TRUE の場合、フィールドは更新可能です。

 行のセット内の行を一意に識別するマーカーにブックマークを設定し、ユーザーがすぐに移動できるようにします。

 ビジネスオブジェクトデータ検証やビジネスルールロジックなど、定義済みの操作のセットを実行するオブジェクト。 ビジネスオブジェクトは通常、中間層に存在します。

 ビジネスルール検証の編集、ログオンの検証、データベース参照、ポリシー、および企業の業務遂行を構成するアルゴリズム変換を組み合わせたものです。 *ビジネスロジック* とも呼ばれます。

## <a name="c"></a>C
 計算式が定数ではなく、値が他の値に依存する式。 評価するには、計算式で他のソース (通常は他のフィールドまたは行) から値を取得して計算する必要があります。

 章データソースからの範囲の行への参照。 ADO では、通常、チャプターは別の **レコードセット** への参照です。

 チャプター列を使用すると、親と *子* のリレーションシップを定義できます。 *親* は、チャプター列を含む **レコードセット** であり、 *子* はチャプターによって表される **レコードセット** です。

 chapter-エイリアス親に追加された列を参照するエイリアス。

 文字セットを数値にマップする文字セット。 たとえば、Unicode は、すべての既知の文字をエンコードできる16ビット文字セットであり、世界中の文字エンコード標準として使用されます。

 階層リレーションシップの依存側の子。 子は階層構造のノードであり、その上に別のノードがあります (ルートに近い)。 「 *子エイリアス*、 *親子リレーションシップ*、 *親*」も参照してください。

 子エイリアス子を参照する別名。 「 *別名*、 *子*」も参照してください。

 CLSID (クラス識別子) COM コンポーネントを識別する汎用一意識別子 (UUID)。 各 COM コンポーネントは、他のアプリケーションから読み込むことができるように、Windows レジストリに CLSID を持ちます。 「 *ProgID*、 *COM*」も参照してください。

 クライアント層。通常、ユーザーからのデータを提示して処理する分散システムの論理層。 *フロントエンド* と呼ばれることもあります。 通常、クライアント層は、入力に基づいてサーバーからデータを要求し、その結果を書式設定して表示します。 「 *中間層*」、「 *データソース層*」、「 *分散アプリケーション*」も参照してください。

 COM (コンポーネントオブジェクトモデル) は、開発された言語や、それらが存在するコンピューターに関係なく、ネットワーク環境でオブジェクトを相互運用できるようにするバイナリ標準です。 COM ベースのテクノロジには、ActiveX コントロール、オートメーション、およびオブジェクトのリンクと埋め込み (OLE) が含まれます。 COM を使用すると、オブジェクトは、その機能を他のコンポーネントに公開したり、アプリケーションをホストしたりできます。 オブジェクトがそれ自体を公開する方法と、この公開がプロセス間およびネットワーク間でどのように機能するかを定義します。 COM は、オブジェクトのライフサイクルも定義します。

 COM コンポーネントバイナリファイル (.dll、.ocx、一部の .exe ファイルなど)。オブジェクトを提供するための COM 標準をサポートしています。 このようなファイルには、1つまたは複数のクラスファクトリ、COM クラス、レジストリ入力機構、コードの読み込みなどのコードが含まれています。

 比較演算子2つの式を比較し、ブール値を返す演算子です。

 ">" (より大きい)、"=" (以上)、" \<" (less than), "=" (equal), "> <=" (より小さいまたは等しい)、"<>" (等しくない)、"like" (パターンマッチング) として表すことができる条件パラメーター。

 コンポーネント: データとコードの両方をカプセル化し、公開されているサービスの適切なセットを提供します。

 複合ファイルファイルの COM 構造化ストレージの実装。 複合ファイルは、ストレージオブジェクトとストリームオブジェクトという2つの主要要素で構成される単一の構造化ファイルに、個別のオブジェクトを格納します。 これらの関数は、ファイル内のファイルシステムのように機能します。

 1つの物理ファイルに結合された個別のファイルの数。 複合ファイル内の個々のファイルには、1つの物理ファイルであるかのようにアクセスできます。

 定数は、変更されない数値または文字列値です。 名前付き ADO 列挙 (列挙定数) は、実際の値ではなく、コード内で使用できます。たとえば、 **adUseClient** は値が3である定数です。 (Const adUseClient = 3)。 「 *列挙型*」も参照してください。

 cursor レコードナビゲーション、データの更新、および他のユーザーによってデータベースに加えられた変更の表示を制御するデータベース要素。

## <a name="d"></a>D
 データバインディングアプリケーションのオブジェクトまたはコントロールをデータソースに関連付けるプロセスです。 データソースに関連付けられているコントロールは、 *データバインドコントロール* と呼ばれます。

 データバインドコントロールの内容は、データベースの値に関連付けられています。 たとえば、 **レコード** セットオブジェクトにバインドされているグリッドコントロールは、 **レコードセット** 内の行が更新されたときに更新できます。 **レコードセット** によって新しい値が取得されると、新しい値がグリッドに表示されます。

 データプロバイダーソフトウェア。 ADO アプリケーションに直接、またはサービスプロバイダーを介してデータを公開します。 「サービスプロバイダー」も参照してください。

 データだけでなく **、他の** レコードセットオブジェクトやその他の **レコード** セットオブジェクトに基づいて計算値を参照する特殊な **レコード** セットオブジェクト (図形言語と呼ば *れる) を* 定義するために、形式化された構文 (**図形言語**) を使用するデータシェイプ。

 データソース層は、SQL Server データベースなど、DBMS を実行するコンピューターを表す分散システムの論理層です。 「 *クライアント層*、 *中間層*、 *分散アプリケーション*」も参照してください。

 DCOM は、COM コンポーネントがネットワーク経由で相互に直接通信できるようにするワイヤプロトコルです。 「 *COM*、 *コンポーネント*」も参照してください。

 DDL (データ定義言語) データを操作するのではなく、を定義する SQL のステートメント。 データベースのスキーマは、DDL を使用して作成または変更されます。 たとえば、 **CREATE TABLE**、 **CREATE INDEX**、 **GRANT**、および **REVOKE** は SQL DDL ステートメントです。

 既定のストリーム ( **stream** オブジェクトによって表される) テキストまたはバイナリストリームは、Microsoft OLE DB Provider For Internet Publishing などの特定の OLE DB プロバイダーを使用する場合に、 **レコード** または **レコードセット** オブジェクトに関連付けられています。 既定のストリームには、通常、Web サイトのルートの HTML コードなどのファイルの内容が含まれます。

 配布されたアプリケーション。処理をネットワーク経由で複数のコンピューターに分割できるように、プログラムを作成しました。 通常、分散アプリケーションは、プレゼンテーション層、ビジネスロジック層、およびデータストア層 ( *層*) に分割されます。 「クライアント層」、「中間層」、「データソース層」も参照してください。

 切断されたレコードセットは、サーバーへのライブ接続がなくなったクライアントキャッシュ内の **レコードセット** オブジェクトです。 データの更新など、何らかの理由で元のデータソースに再度アクセスする必要がある場合は、接続を再確立する必要があります。 ただし、切断された **レコードセット** のコレクション、プロパティ、およびメソッドには引き続きアクセスできます。

 DML (データ操作言語) データを定義するのではなく、操作する SQL のステートメント。 データベース内の値は、DML を使用して選択および変更されます。 たとえば、 **INSERT**、 **UPDATE**、 **DELETE**、 **SELECT** は SQL DML ステートメントです。

 ドキュメントソースプロバイダーフォルダーとドキュメントを管理するプロバイダーの特殊なクラスです。 ドキュメントが **レコード** オブジェクトによって表される場合、またはドキュメントのフォルダーが **レコードセット** オブジェクトによって表される場合、ドキュメントソースプロバイダーは、実際のドキュメントそのものではなく、ドキュメントの特性を記述するフィールドの一意のセットをそれらのオブジェクトに挿入します。 「リソースレコード」も参照してください。

 DSN (データソース名) アプリケーションを特定の ODBC データベースに接続するために使用する情報のコレクション。 ODBC ドライバーマネージャーは、この情報を使用してデータベースへの接続を作成します。 DSN は、ファイル (ファイル DSN) または Windows レジストリ (コンピューター DSN) に格納できます。

 動的プロパティデータプロバイダーまたはカーソルサービスに固有のプロパティです。 オブジェクトの **Properties** コレクションには、これらの値が自動的に設定されます ("動的")。 オブジェクトは、特定のデータプロバイダーを介してデータソースに接続されるまで、動的プロパティを持ちません。 「データプロバイダー、カーソル」も参照してください。

## <a name="e"></a>E
 列挙名前付き定数の一覧。 列挙値は一意である必要はありません。 ただし、各値の名前は、列挙型が定義されているスコープ内で一意である必要があります。 ADO では、数値パラメーターと戻り値に対して列挙型を使用して、ADO コードに意味を追加し、数値から開発者を保護します (バージョン間で変更される可能性があります)。 たとえば、静的 **レコードセット** を開くには、 **adopenstatic** 列挙値を使用します。 `Recordset.Open ,,adOpenStatic`

 *列挙定数* とも呼ばれます。 「 *定数*」も参照してください。

 イベント応答するコードを記述できるオブジェクトによって認識されるアクション。 イベントは、コマンドの実行、トランザクションの完了、レコードセットのナビゲーション、データの更新などの操作によって生成できます。 「 *イベントハンドラー*」も参照してください。

 イベントハンドラーイベントハンドラーは、イベントが発生したときに実行されるコードです。 「イベント」も参照してください。

## <a name="h"></a>H
 エラー回復やデータ管理など、一般的で比較的単純な条件または操作を管理するルーチンをハンドラします。

 階層レコードセット別の **レコードセット** を含む **レコードセット**。 「データシェイプ、章」も参照してください。

 詳細については、「 [階層レコードセット内の行へのアクセス](./guide/data/accessing-rows-in-a-hierarchical-recordset.md)」を参照してください。

 階層一般に、階層とは、最上位レベルと下位レベルを持つランク付けされた構造のことです。 ADO では、階層レコード **セット** を使用して、レコードとチャプター間の親子リレーションシップを表します。 また、ADO では、 **レコード** および **ストリーム** オブジェクトを使用して、フォルダーやドキュメントなどの階層ツリー構造にアクセスできます。 ADO MD には、OLAP キューブ内のディメンションのレベル間のリレーションシップを表す **階層** オブジェクトも含まれます。 「階層レコードセット」、「親子リレーションシップ」、「章」、「ツリー」も参照してください。

## <a name="i-l"></a>I-L
 ISAPI (インターネットサーバーアプリケーションプログラミングインターフェイス) インターネットサーバー用の一連の関数 &reg; &reg; (Microsoft インターネットインフォメーションサービス (IIS) を実行する windows NT Server/Windows 2000 サーバーなど)。

 行を一意に識別するテーブル内の1つまたは複数の列。多くの場合、テーブルのインデックス作成に使用されます。

## <a name="m"></a>M
 スレッドまたはプロセスの境界を越えて、パッケージ化、送信、および unpackaging の各インターフェイスメソッドパラメーターのプロセスをマーシャリングします。

 ユーザーインターフェイスまたは Web クライアントとデータベースの間の分散システムの論理層。 これは通常、ビジネスオブジェクトがインスタンス化される場所です。 中間層は、受信情報を生成して操作するビジネスルールと関数のコレクションです。 この処理は、頻繁に変更される可能性があり、アプリケーションロジック自体とは物理的に分離されたコンポーネントにカプセル化されるビジネスルールによって実現されます。 *アプリケーションサーバー層* とも呼ばれます。 「分散アプリケーション」、「クライアント層」、「データソース層」も参照してください。

 MIME (多目的インターネットメール拡張): もともと、異種ネットワーク、コンピューター、および電子メール環境で、豊富なコンテンツを含む電子メールメッセージを交換できるようにするために開発されたインターネットプロトコルです。 実際には、MIME はメール以外のアプリケーションによって採用され、拡張されています。

 MIME は、バイナリデータをインターネット上で公開して読み取ることを可能にする標準です。 バイナリデータを含むファイルのヘッダーには、データの MIME の種類が含まれます。これにより、クライアントプログラム (たとえば、Web ブラウザーとメールパッケージ) に対して、テキストを処理する場合とは異なる方法でデータを処理する必要があることが通知されます。 たとえば、JPEG グラフィックを含む Web ドキュメントのヘッダーには、JPEG ファイル形式に固有の MIME の種類が含まれています。 これにより、ブラウザーは JPEG ビューアーを使用してファイルを表示できます (存在する場合)。

## <a name="n-o"></a>N-O
 ノード階層ツリー構造内の要素。 ノードには、ルートまたは別のノードの子を指定できます。 ノードは、複数の子の親にすることもできます。 「階層、ツリー、ルート、子、親」も参照してください。

 オブジェクト変数オブジェクトへの参照を含む変数です。 たとえば、 `objCustomObject` は、CustomObject 型のオブジェクトを指す変数です。`Set objCustomObject = CreateObject(adodb.Recordset)`

 ODBC (Open Database Connectivity) さまざまなデータソースに接続するために使用される標準のプログラミング言語インターフェイス。 これには通常、コントロールパネルを使用してアクセスします。ここでは、データソース名 (Dsn) を割り当てて、特定の ODBC ドライバーを使用することができます。

 COM を使用してさまざまなソースからデータを公開するインターフェイスのセットを OLE DB します。 OLE DB インターフェイスは、さまざまな情報ソースに格納されているデータへの一貫したアクセスをアプリケーションに提供します。 これらのインターフェイスは、データソースに適した DBMS 機能の量をサポートし、データを共有できるようにします。 「COM」も参照してください。

 オプティミスティックロックでは、1つまたは複数のレコードを含むデータページ (編集中のレコードを含む) は、 **update** メソッドによって更新されているが、 **update** の呼び出しの前後で使用可能な場合にのみ、他のユーザーが使用できないロックの種類です。

 オプティミスティックロックは、 **LockType** パラメーターまたはプロパティを **adlockoptimistic** または **adlockbatchオプティミスティック** に設定して **Recordset** オブジェクトを開くときに使用されます。 「ペシミスティックロック」も参照してください。

 序数値。注文内の項目の位置を表す数値です。 ADO コレクションでは、最初の項目の序数値はゼロ (0) です。 次の項目は 1 (1) です。

## <a name="p"></a>P
 パラメーター化されたコマンドコマンドを実行する前にパラメーター値を設定できるクエリまたはコマンド。 たとえば、sql 文字列は、パラメーターマーカーを SQL 文字列 ('? ' 文字で指定) に埋め込むことによってパラメーター化できます。 次に、アプリケーションは各パラメーターの値を指定し、コマンドを実行します。

 階層リレーションシップの制御側の親。 階層構造では、親は階層の直下に1つまたは複数の子ノードを持ちます。 「親-別名、親子関係、子」も参照してください。

 親-エイリアス親を参照する別名。 「エイリアス、親」も参照してください。

 親子リレーションシップ親が1レベル上位で、1つまたは複数の子に直接関連付けられている階層構造のリレーションシップ。 子は1レベル下位で、1つの親を持つ必要があります。 「親子」も参照してください。

 ペシミスティックロックは、編集中のレコードを含む1つ以上のレコードを含むページを他のユーザーが使用できないようにして、更新が確実に行われるようにします。 ペシミスティックロックの動作は、OLE DB プロバイダーによって定義されます。 通常、レコードは編集時にロックされ、 **更新** メソッドが完了するまで使用不可のままになります。

 ペシミスティックロックは、 **レコードセット** オブジェクトを開いたときに、 **LockType** パラメーターまたはプロパティが **adlockpessimistic** に設定されている場合に有効になります。 「オプティミスティックロック」も参照してください。

 オブジェクトやデータベース接続など、事前に割り当てられたリソースのコレクションの使用に基づいて、パフォーマンスの最適化をプールします。 新しいリソースを作成するよりも、プールから既存のリソースを描画する方が効率的です。

 ProgID (プログラム識別子) COM アプリケーションによって Windows レジストリにマップされる一意の名前。 ADO 接続の ProgID は "ADODB" です。接続 "。 「CLSID、COM」も参照してください。

 プロキシ: 別のスレッドや別のプロセスなど、別の実行環境で実行されているアプリケーションオブジェクトをクライアントが呼び出すために必要なパラメーターのマーシャリングと通信を提供するインターフェイス固有のオブジェクト。 プロキシは、クライアントに配置され、呼び出されているアプリケーションオブジェクトに配置されている対応するスタブと通信します。 「スタブ」も参照してください。

## <a name="r"></a>R
 相対 URL は、インターネット上のリソースまたは絶対 URL または同等の ADO 接続オブジェクトによって指定された開始点を基準とするイントラネット上のリソースを指定する、部分的に修飾された url です。 実際には、連結された絶対 Url と相対 Url は完全な URL を consitute します。 「URL と絶対 URL」も参照してください。

 リモートデータソースローカルシステム (クライアントアプリケーションが実行されている場所) ではなく、別のコンピューター上に存在するデータソース。

 リソースレコードドキュメントソースプロバイダーからのレコードを記録します。このレコードには、フォルダーまたはドキュメントの定義と説明のフィールドが含まれています。 ドキュメント自体はリソースレコードに含まれていませんが、通常は既定のストリーム、または URL を含むリソースレコードのフィールドによってアクセスできます。 「ドキュメントソースプロバイダー、既定のストリーム、URL」も参照してください。

 すべて同じフィールドスキーマを持つデータソースから行のセットを行セットします。 行セットは、テーブルのすべてまたは一部のフィールドを表すことができます。 行セットは、クエリまたは複数のテーブルの結合によって作成された仮想テーブルを表すこともできます。 ADO では、行セットは **レコードセット** オブジェクトによって表されます。

## <a name="s"></a>S
 オブジェクトまたは変数の参照範囲、またはビューまたはテーブル内のレコードの範囲のスコープを指定します。 たとえば、ローカル変数は、その変数が定義されているプロシージャ内でのみ参照できます。 パブリック変数は、アプリケーション内のどこからでもアクセスできます。 現在のデータベースなどのオブジェクトは、定義された検索パスに存在する場合、スコープ内にあります。 レコード範囲は、多くのコマンドで Scope 句を使用して指定できます。

 データの生成と使用によってサービスをカプセル化し、ADO アプリケーションの機能を強化するサービスプロバイダーソフトウェア。 データを直接公開しないプロバイダーであり、クエリ処理などのサービスを提供します。 サービスプロバイダーは、データプロバイダーによって提供されるデータを処理できます。 「データプロバイダー」も参照してください。

 レコードセットの整形。データだけでなく、他のレコードセットオブジェクトや他の **レコード** セットオブジェクトに基づいて計算された値 **への参照**(チャプターとも呼ばれる) を持つ列を含む **レコードセット**。

 階層構造内の2つ以上のノードについて、階層内の同じレベルにある兄弟。 階層内のルートノードに兄弟がありません。

 ストアドプロシージャプリコンパイル済みのコードのコレクション。名前の下に格納され、1つの単位として処理される、SQL ステートメントやオプションのフロー制御ステートメントなどです。 ストアドプロシージャはデータベース内に格納されます。アプリケーションからの1回の呼び出しを使用して実行し、ユーザーが宣言した変数、条件付き実行、その他の強力なプログラミング機能を使用できます。

 別のスレッドや別のプロセスなど、別の実行環境で実行されているクライアントからの呼び出しを受信するために、アプリケーションオブジェクトに必要なパラメーターのマーシャリングと通信を提供するインターフェイス固有のオブジェクトをスタブします。 スタブはアプリケーションオブジェクトと共に配置され、それを呼び出すクライアントに配置されている対応するプロキシと通信します。 「プロキシ」も参照してください。

 サブノード「子」を参照してください。

 同期操作は、次の操作が開始される前に完了するコードによって開始される操作です。 「非同期操作」も参照してください。

## <a name="t-z"></a>T-Z
 ツリー要素 (ノード) 間の階層リレーションシップを表す構造体。 ツリーの最上位レベルに1つのノード (ルート) があります。 ルートの下には、複数の子が存在する場合があります。 各子は、他の子の親になることができます。したがって、ツリーのように分岐します。 ドキュメントやその他のフォルダーを含むフォルダーは、一般的なツリー構造の例です。 「階層、ノード、ルート、子、親」も参照してください。

 Web サーバーイントラネットおよびインターネットユーザーに Web サービスおよびページを提供するコンピューター。