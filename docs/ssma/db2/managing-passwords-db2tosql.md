---
description: パスワードの管理 (DB2ToSQL)
title: パスワードの管理 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/05/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 56d546e3-8747-4169-aace-693302667e94
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f68af2ae2176ed4860f92a829544c7ff463254e9
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987418"
---
# <a name="managing-passwords-db2tosql"></a>パスワードの管理 (DB2ToSQL)
このセクションでは、データベースのパスワードをセキュリティで保護する方法と、サーバー間でインポートまたはエクスポートする手順について説明します。  
  
1.  パスワードのセキュリティ保護  
  
2.  暗号化されたパスワードのエクスポートまたはインポート  
  
## <a name="securing-password"></a>パスワードのセキュリティ保護  
SSMA を使用すると、データベースのパスワードをセキュリティで保護することができます。  
  
セキュリティで保護された接続を実装するには、次の手順に従います。  
  
次の3つの方法のいずれかを使用して、有効なパスワードを指定します。  
  
1.  **クリアテキスト:** [パスワード] ノードの値属性にデータベースパスワードを入力します。 これは、スクリプトファイルまたはサーバー接続ファイルのサーバーセクションの [サーバー定義] ノードの下にあります。  
  
    クリアテキストのパスワードはセキュリティで保護されていません。 このため、コンソールの出力には、 *"サーバー &lt; サーバー-id パスワードはセキュリティで保護されてい &gt; ないクリアテキスト形式で提供されます。 ssma コンソールアプリケーションは、暗号化によってパスワードを保護するオプションを提供します。詳細については、ssma ヘルプファイルの-securepassword オプションを参照してください。"*  
  
    **暗号化されたパスワード:** この場合、指定されたパスワードは、ProtectedStorage のローカルコンピューター上の暗号化された形式で格納されます。  
  
    -   **パスワードのセキュリティ保護**  
  
        -   を使用してを実行し、 `SSMAforDB2Console.exe` `-securepassword` コマンドラインで [サーバーの定義] セクションの [パスワード] ノードを含むサーバー接続またはスクリプトファイルを渡します。  
  
        -   プロンプトが表示されたら、データベースのパスワードを入力して確認します。  
  
            サーバー定義 id とそれに対応する暗号化されたパスワードは、ローカルコンピューター上のファイルに格納されます。  
            
            例 1:
            
            ```console
            Specify password
            C:\SSMA\SSMAforDB2Console.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\ VariableValueFileSample.xml"
            
            Enter password for server_id 'XXX_1': xxxxxxx
            
            Re-enter password for server_id 'XXX_1': xxxxxxx
            ```
            
            例 2:
            
            ```console
            C:\SSMA\SSMAforDB2Console.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\ VariableValueFileSample.xml" -o
            
            Enter password for server_id 'source_1': xxxxxxx
            
            Re-enter password for server_id 'source_1': xxxxxxx
            
            Enter password for server_id 'target_1': xxxxxxx
            
            Re-enter password for server_id 'target _1': xxxxxxx  
            ```
    
    -   **暗号化されたパスワードの削除**  
  
        とを使用してを実行し、 `SSMAforDB2Console.exe` `-securepassword` サーバー id を渡してコマンドラインでを実行して、 `-remove` 暗号化されたパスワードをローカルコンピューターに存在する保護されたストレージファイルから削除します。  
  
        例:  

        ```console
        C:\SSMA\SSMAforDB2Console.EXE -securepassword -remove all
        C:\SSMA\SSMAforDB2Console.EXE -securepassword -remove "source_1,target_1"
        ```

    -   **パスワードが暗号化されているサーバー Id を一覧表示する**  
  
        を実行し、 `SSMAforDB2Console.exe` `-securepassword` コマンドラインでを実行して、 `-list` パスワードが暗号化されているすべてのサーバー id を一覧表示します。  
  
        例:  

        ```console
        C:\SSMA\SSMAforDB2Console.EXE -securepassword -list
        ```

    > [!NOTE]  
    > 1.  スクリプトまたはサーバー接続ファイルで説明されているクリアテキストのパスワードは、セキュリティで保護されたファイルの暗号化されたパスワードよりも優先されます。  
    > 2.  サーバー接続ファイルまたはスクリプトファイルの server セクションにパスワードが存在しない場合、またはローカルコンピューター上でセキュリティ保護されていない場合は、コンソールにパスワードの入力を求めるメッセージが表示されます。  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>暗号化されたパスワードのエクスポートまたはインポート  
SSMA コンソールアプリケーションを使用すると、ローカルコンピューター上のファイルに存在する暗号化されたデータベースパスワードを、セキュリティで保護されたファイルにエクスポートできます。また、その逆も可能です。 暗号化されたパスワードをコンピューターに依存させるのに役立ちます。

_エクスポート機能_ は、ローカルで保護されているストレージからサーバー id とパスワードを読み取ります。 次に、暗号化されたファイルに id とパスワードを保存します。 ユーザーは、セキュリティで保護されたファイルのパスワードを入力するように求められます。 入力したパスワードが8文字以上の長さであることを確認してください。 このセキュリティで保護されたファイルは、異なるコンピューター間で移植できます。

_インポート機能_ は、サーバー id とパスワードの情報をセキュリティで保護されたファイルから読み取ります。 ユーザーは、セキュリティで保護されたファイルのパスワードを入力するように求められ、ローカルで保護されているストレージに情報が追加されます。  

### <a name="export-example"></a>エクスポートの例

1. パスワードをエクスポートします。

2. エクスポートされたファイルを保護するためのパスワードを入力します。

3. &nbsp; `C:\SSMA\SSMAforDB2Console.EXE -securepassword -export all "machine1passwords.file"` を実行します。

4. エクスポートされたファイルを保護するためのパスワードを入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

5. パスワードの確認入力: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

6. &nbsp; `C:\SSMA\SSMAforDB2Console.EXE -p -e "DB2DB_1_1,Sql_1" "machine2passwords.file"` を実行します。

7. エクスポートされたファイルを保護するためのパスワードを入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

8. パスワードの確認入力: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  

### <a name="import-example"></a>インポートの例

1. 暗号化されたパスワードをインポートします。

2. インポートされたファイルを保護するためのパスワードを入力します。

3. &nbsp; `C:\SSMA\SSMAforDB2Console.EXE -securepassword -import all "machine1passwords.file"` を実行します。

4. 暗号化されたファイルからサーバーをインポートするためのパスワードを入力します: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

5. パスワードの確認入力: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

6. &nbsp; `C:\SSMA\SSMAforDB2Console.EXE -p -i "DB2DB_1,Sql_1" "machine2passwords.file"` を実行します。

7. 暗号化されたファイルからサーバーをインポートするためのパスワードを入力します: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

8. パスワードの確認入力: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="see-also"></a>参照  
[SSMA コンソールの実行](./executing-the-ssma-console-db2tosql.md)  
