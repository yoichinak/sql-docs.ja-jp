---
title: Oracle Database に接続しています (OracleToSQL) |Microsoft Docs
description: Oracle データベースに接続して Oracle データベースを SQL Server に移行する方法について説明します。 SSMA は、すべての Oracle スキーマに関するメタデータを取得して表示します。
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 06/04/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
ms.author: alexiva
ms.openlocfilehash: 4354a4e2726151177c48c27ce37a74e5b4ac335e
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100058799"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>Oracle データベースへの接続 (OracleToSQL)

Oracle データベースをに移行するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、移行する oracle データベースに接続する必要があります。 接続すると、SSMA はすべての Oracle スキーマに関するメタデータを取得し、[Oracle メタデータエクスプローラー] ペインに表示します。 SSMA は、データベースサーバーに関する情報を格納しますが、パスワードは保存しません。

データベースへの接続は、プロジェクトを閉じるまでアクティブなままになります。 プロジェクトを再度開いたときに、データベースへのアクティブな接続が必要な場合は、再接続する必要があります。

Oracle データベースに関するメタデータは自動的に更新されません。 代わりに、Oracle メタデータエクスプローラーでメタデータを更新する場合は、手動で更新する必要があります。 詳細については、このトピックで後述する「Oracle メタデータの更新」セクションを参照してください。

## <a name="required-oracle-permissions"></a>必要な Oracle 権限

Oracle データベースへの接続に使用するアカウントには、少なくとも次の権限が必要です。

- `CONNECT`  
  データベースへの接続 (セッションの作成) に必要です。

- `SELECT ANY DICTIONARY`  
  `SYS.MLOG$`すべてのオブジェクトを検出するためにシステムディクショナリテーブル (たとえば、) のクエリを実行するために必要です。

これにより、SSMA は、接続しているユーザーが所有するスキーマ内のすべてのオブジェクトを読み込むことができます。 ほとんどの実際のシナリオでは、ストアドプロシージャ間にスキーマ間の参照があり、SSMA が正常に変換されるためには、すべての参照先オブジェクトを検出できる必要があります。 他のスキーマで定義されているオブジェクトのメタデータを取得するには、アカウントに次の追加のアクセス許可が必要です。

- `SELECT ANY TABLE`  
  他のスキーマのテーブル、ビュー、具体化されたビュー、およびシノニムを検出するために必要です。

- `SELECT ANY SEQUENCE`  
  他のスキーマ内のシーケンスを検出するために必要です。

- `CREATE ANY PROCEDURE`  
  他のスキーマのプロシージャ、関数、およびパッケージの PL/SQL を検出するために必要です。

- `CREATE ANY TRIGGER`  
  他のスキーマのトリガー定義を検出するために必要です。

- `CREATE ANY TYPE`  
  他のスキーマで定義されている型を検出するために必要です。

SSMA の機能の中には、追加のアクセス許可が必要なものもあります。 たとえば、 [テスト担当](testing-migrated-database-objects-oracletosql.md) 者と [バックアップ管理](managing-backups-oracletosql.md) 機能を使用する場合は、接続するユーザーに次の権限を付与する必要があります。

- `EXECUTE ANY PROCEDURE`  
  すべてのスキーマでテストするプロシージャと関数を実行するために必要です。

- `CREATE ANY TABLE` および `ALTER ANY TABLE`  
  変更の追跡とバックアップの一時テーブルを作成および変更するために必要です。

- `INSERT ANY TABLE` および `UPDATE ANY TABLE`  
  変更の追跡とバックアップデータを一時テーブルに挿入するために必要です。

- `DROP ANY TABLE`  
  変更の追跡とバックアップに使用される一時テーブルを削除する場合に必要です。

- `CREATE ANY INDEX` および `ALTER ANY INDEX`  
  変更の追跡とバックアップに使用される一時テーブルのインデックスを作成および変更するために必要です。

- `DROP ANY INDEX`  
  変更の追跡とバックアップに使用される一時テーブルのインデックスを削除するために必要です。

- `CREATE ANY TRIGGER` および `ALTER ANY TRIGGER`  
  変更の追跡に使用される一時トリガーを作成および変更するために必要です。

- `DROP ANY TRIGGER`  
  変更の追跡に使用される一時トリガーを削除する場合に必要です。

> [!NOTE]
> これは、SSMA を正常に動作させるために必要な一連のアクセス許可です。 移行の範囲をスキーマのサブセットに絞り込むには、ではなく、限られたオブジェクトのセットに対して上記のアクセス許可を付与し `ALL` ます。 可能な限り、すべての依存関係を正確に識別することが非常に困難であるため、SSMA が正常に機能しなくなる可能性があります。 移行プロセス中に発生する可能性のあるアクセス許可の問題を排除するために、前述のように汎用セットに従うことを強くお勧めします。

## <a name="establishing-a-connection-to-oracle"></a>Oracle への接続の確立

データベースに接続すると、SSMA によってデータベースのメタデータが読み取られ、このメタデータがプロジェクトファイルに追加されます。 このメタデータは、SSMA がオブジェクトを構文に変換するとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] およびにデータを移行するときに使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このメタデータは、[Oracle メタデータエクスプローラー] ペインで参照して、個々のデータベースオブジェクトのプロパティを確認できます。

> [!IMPORTANT]
> 接続を試行する前に、データベースサーバーが実行されていて、接続を受け入れることができることを確認してください。

**Oracle に接続するには**

1. [ **ファイル** ] メニューの [ **Oracle への接続**] をクリックします。  
   以前に Oracle に接続していた場合は、コマンド名が **oracle に再接続** されます。
  
2. [ **プロバイダー** ] ボックスで、インストールされているプロバイダーに応じて [ **Oracle クライアントプロバイダー** ] または [ **OLE DB プロバイダー**] を選択します。 既定値は [Oracle client (Oracle クライアント) です。

3. [ **モード** ] ボックスで、[ **標準モード**]、[ **tnsname モード**]、または [ **接続文字列モード**] を選択します。  
   サーバー名とポートを指定するには、標準モードを使用します。 サービス名モードを使用して、Oracle サービス名を手動で指定します。 接続文字列モードを使用して、完全な接続文字列を指定します。

4. [標準] **モード** を選択した場合は、次の値を指定します。
   1. [ **サーバー名** ] ボックスで、データベースサーバーの名前または IP アドレスを入力または選択します。
   2. データベースサーバーが既定のポート (1521) で接続を受け入れるように構成されていない場合は、[ **サーバーポート** ] ボックスに、Oracle 接続に使用するポート番号を入力します。
   3. [ **ORACLE SID** ] ボックスに、システム識別子を入力します。
   4. [ **ユーザー名** ] ボックスに、必要なアクセス許可を持つ Oracle アカウントを入力します。
   5. [ **パスワード** ] ボックスに、指定したユーザー名のパスワードを入力します。

5. **Tnsname モード** を選択した場合は、次の値を指定します。
   1. [ **接続識別子** ] ボックスに、データベースの接続識別子 (TNS alias) を入力します。
   2. [ **ユーザー名** ] ボックスに、必要なアクセス許可を持つ Oracle アカウントを入力します。
   3. [ **パスワード** ] ボックスに、指定したユーザー名のパスワードを入力します。
  
6. **接続文字列モード** を選択した場合は、[**接続文字列**] ボックスに接続文字列を指定します。  
   次の例は、OLE DB 接続文字列を示しています。

   `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`

   次の例は、統合セキュリティを使用する Oracle クライアント接続文字列を示しています。

   `Data Source=MyOracleDB;Integrated Security=yes;`

   詳細については、「 [Connect To Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)」を参照してください。

## <a name="reconnecting-to-oracle"></a>Oracle への再接続

データベースサーバーへの接続は、プロジェクトを閉じるまでアクティブなままになります。 プロジェクトを再度開いたときに、データベースへのアクティブな接続が必要な場合は、再接続する必要があります。 メタデータを更新したり、データベースオブジェクトをに読み込んだり、データを移行したりするまで、オフラインで作業することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

## <a name="refreshing-oracle-metadata"></a>Oracle メタデータの更新

Oracle データベースに関するメタデータは自動的には更新されません。 Oracle メタデータエクスプローラーのメタデータは、最初に接続したとき、またはメタデータを手動で更新したときにメタデータのスナップショットになります。 すべてのスキーマ、単一のスキーマ、または個々のデータベースオブジェクトのメタデータを手動で更新できます。

**メタデータを更新するには**

1. データベースに接続していることを確認します。

2. Oracle メタデータエクスプローラーで、更新する各スキーマまたはデータベースオブジェクトの横にあるチェックボックスをオンにします。

3. [ **スキーマ**]、または個々のスキーマまたはデータベースオブジェクトを右クリックし、[ **データベースから更新**] を選択します。  
   アクティブな接続がない場合は、SSMA によって [ **Oracle への接続** ] ダイアログボックスが表示され、接続できるようになります。

4. [データベースから更新] ダイアログボックスで、更新するオブジェクトを指定します。

   - オブジェクトを更新するには、オブジェクトの横にある **アクティブ** フィールドをクリックして、矢印が表示されるようにします。
   - オブジェクトが更新されないようにするには、 **X** が表示されるまで、オブジェクトの横にある **アクティブな** フィールドをクリックします。
   - オブジェクトのカテゴリを更新または拒否するには、category フォルダーの横にある **アクティブな** フィールドをクリックします。

   色分けの定義を表示するには、[ **凡例** ] ボタンをクリックします。

5. [!INCLUDE[clickOK](../../includes/clickok-md.md)]

## <a name="next-steps"></a>次のステップ

移行プロセスの次の手順では、 [SQL Server のインスタンスに接続](connecting-to-sql-server-oracletosql.md)します。

## <a name="see-also"></a>関連項目

[Oracle データベースの SQL Server &#40;OracleToSQL&#41;への移行 ](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
