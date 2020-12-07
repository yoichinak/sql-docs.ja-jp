---
description: パスワードの管理 (SybaseToSQL)
title: パスワードの管理 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/07/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Exporting or Importing Encrypted Passwords
- Sybase Console,Managing Passwords
- Sybase Console,Securing Password
ms.assetid: 9b6a70f9-6840-4140-a059-bb7bd7ccc67c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5a43526e9dd4b0d1e5057c9854a827b084a7e17b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036502"
---
# <a name="managing-passwords-sybasetosql"></a>パスワードの管理 (SybaseToSQL)
このセクションでは、データベースのパスワードをセキュリティで保護する方法と、サーバー間でインポートまたはエクスポートする手順について説明します。

## <a name="securing-password"></a>パスワードのセキュリティ保護  
SSMA を使用すると、データベースのパスワードをセキュリティで保護することができます。  
  
セキュリティで保護された接続を実装するには、次の手順に従います。  
  
次の3つの方法のいずれかを使用して、有効なパスワードを指定します。  
  
1.  **クリアテキスト:** [パスワード] ノードの値属性にデータベースパスワードを入力します。 これは、スクリプトファイルまたはサーバー接続ファイルのサーバーセクションの [サーバー定義] ノードの下にあります。  
  
    クリアテキストのパスワードはセキュリティで保護されていません。 このため、コンソールの出力には、 *"サーバー &lt; サーバー-id パスワードはセキュリティで保護されてい &gt; ないクリアテキスト形式で提供されます。 ssma コンソールアプリケーションは、暗号化によってパスワードを保護するオプションを提供します。詳細については、ssma ヘルプファイルの-securepassword オプションを参照してください。"*  
  
    **暗号化されたパスワード:** この場合、指定されたパスワードは、ProtectedStorage のローカルコンピューター上の暗号化された形式で格納されます。  
  
    -   **パスワードのセキュリティ保護**  
  
        -   を使用してを実行し、 `SSMAforSybaseConsole.exe` `-securepassword` コマンドラインで [サーバーの定義] セクションの [パスワード] ノードを含むサーバー接続またはスクリプトファイルを渡します。  
  
        -   プロンプトが表示されたら、データベースのパスワードを入力して確認します。  
  
            サーバー定義 id とそれに対応する暗号化されたパスワードは、ローカルコンピューター上のファイルに格納されます。  
            
            例 1:  
            
            1. パスワードの指定
                
            2. `C:\SSMA\SSMAforSybaseConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ VariableValueFileSample.xml"`
                
            3. Server_id ' XXX_1 ' のパスワードを入力してください: xxxxxxx
                
            4. Server_id ' XXX_1 ' のパスワードを再入力してください: xxxxxxx
            
            例 2:
            
            1. `C:\SSMA\SSMAforSybaseConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ VariableValueFileSample.xml" -o`
                
            2. Server_id ' source_1 ' のパスワードを入力してください: xxxxxxx
                
            3. Server_id ' source_1 ' のパスワードを再入力してください: xxxxxxx
                
            4. Server_id ' target_1 ' のパスワードを入力してください: xxxxxxx
                
            5. Server_id ' target _1 ' のパスワードを再入力してください: xxxxxxx  
    
    -   **暗号化されたパスワードの削除**  
  
        とを使用してを実行し、 `SSMAforSybaseConsole.exe` `-securepassword` サーバー id を渡してコマンドラインでを実行して、 `-remove` 暗号化されたパスワードをローカルコンピューターに存在する保護されたストレージファイルから削除します。  
  
        例:  
        
        ```console
            C:\SSMA\SSMAforSybaseConsole.EXE -securepassword -remove all
            C:\SSMA\SSMAforSybaseConsole.EXE -securepassword -remove "source_1,target_1"  
        ```
  
    -   **パスワードが暗号化されているサーバー Id を一覧表示する**  
  
        を実行し、 `SSMAforSybaseConsole.exe` `-securepassword` コマンドラインでを実行して、 `-list` パスワードが暗号化されているすべてのサーバー id を一覧表示します。  
  
        例:  

        ```console
            C:\SSMA\SSMAforSybaseConsole.EXE -securepassword -list  
        ```
  
    > [!NOTE]  
    > 1.  スクリプトまたはサーバー接続ファイルで説明されているクリアテキストのパスワードは、セキュリティで保護されたファイルの暗号化されたパスワードよりも優先されます。  
    > 2.  サーバー接続ファイルまたはスクリプトファイルの server セクションにパスワードが存在しない場合、またはローカルコンピューター上でセキュリティ保護されていない場合は、コンソールにパスワードの入力を求めるメッセージが表示されます。  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>暗号化されたパスワードのエクスポートまたはインポート  
SSMA コンソールアプリケーションを使用すると、ローカルコンピューター上のファイルに存在する暗号化されたデータベースパスワードを、セキュリティで保護されたファイルにエクスポートできます。また、その逆も可能です。 暗号化されたパスワードをコンピューターに依存させるのに役立ちます。 エクスポート機能は、ローカルで保護されているストレージからサーバー id とパスワードを読み取り、暗号化されたファイルに情報を保存します。 ユーザーは、セキュリティで保護されたファイルのパスワードを入力するように求められます。 入力したパスワードの長さが8文字以上であることを確認します。 このセキュリティで保護されたファイルは、異なるコンピューター間で移植できます。 インポート機能は、サーバー id とパスワードの情報をセキュリティで保護されたファイルから読み取ります。 ユーザーは、セキュリティで保護されたファイルのパスワードを入力するように求められ、ローカルで保護されているストレージに情報が追加されます。  
  
### <a name="export-example"></a>エクスポートの例:  

1. パスワードのエクスポート
    
2. エクスポートされたファイルを保護するためのパスワードを入力してください
    
3. `C:\SSMA\SSMAforSybaseConsole.EXE -securepassword -export all "machine1passwords.file"`
    
4. エクスポートされたファイルを保護するためのパスワードを入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    
5. パスワードを確認入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    
6. `C:\SSMA\SSMAforSybaseConsole.EXE -p -e "SybaseDB_1_1,Sql_1" "machine2passwords.file"`
    
7. エクスポートされたファイルを保護するためのパスワードを入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    
8. パスワードを確認入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  
  
### <a name="import-example"></a>インポートの例:  

1. 暗号化されたパスワードをインポートする
    
2. インポートされたファイルを保護するためのパスワードを入力してください
    
3. `C:\SSMA\SSMAforSybaseConsole.EXE -securepassword -import all "machine1passwords.file"`
    
4. 暗号化されたファイルからサーバーをインポートするためのパスワードを入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    
5. パスワードを確認入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    
6. `C:\SSMA\SSMAforSybaseConsole.EXE -p -i "SybaseDB_1,Sql_1" "machine2passwords.file"`
    
7. 暗号化されたファイルからサーバーをインポートするためのパスワードを入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    
8. パスワードを確認入力してください: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  
  
## <a name="see-also"></a>参照  
[SSMA コンソール (Sybase) の実行](./executing-the-ssma-console-sybasetosql.md)  
