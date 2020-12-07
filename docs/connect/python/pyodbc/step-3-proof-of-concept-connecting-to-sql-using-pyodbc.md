---
title: 手順 3:pyodbc を使用して SQL に接続する
description: 手順 3 は概念実証であり、Python と pyODBC を使用して SQL Server に接続する方法がわかります。 基本的な例で、データの選択と挿入が示されます。
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26cbdea53547f30a59dc6953d7bf68bddc712164
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807035"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>手順 3:pyodbc を使用した SQL への接続を概念実証する

この例は、概念実証です。 わかりやすさのためにサンプル コードは簡略化されており、Microsoft が推奨するベスト プラクティスを表しているとは限りません。  

開始するには、次のサンプル スクリプトを実行します。 test.py という名前のファイルを作成し、各コード スニペットを追加していきます。 

```
> python test.py
```
  
## <a name="connect"></a>接続する  
  
```python
import pyodbc 
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="run-query"></a>Run query  
  
Cursor.execute 関数は、SQL Database に対するクエリから結果セットを取得するために使用できます。 この関数はクエリを受け取り、cursor.fetchone() を使用して反復処理できる結果セットを返します。
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="insert-a-row"></a>行を挿入する  
  
この例からは、[INSERT](../../../t-sql/statements/insert-transact-sql.md) ステートメントを安全に実行し、パラメーターを渡す方法がわかります。 パラメーターにより、アプリケーションは [SQL インジェクション](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)から保護されます。    
  
  
```python
#Sample insert query
cursor.execute("""
INSERT INTO SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) 
VALUES (?,?,?,?,?)""",
'SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP) 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print('Inserted Product key is ' + str(row[0]))
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-and-the-connection-string"></a>Azure Active Directory と接続文字列

pyODBC では、Microsoft ODBC Driver for SQL Server が使用されます。
ODBC ドライバーのバージョンが 17.1 以降の場合は、pyODBC を通じて Azure Active Directory 対話型モードの ODBC ドライバーを使用できます。
この対話型オプションは、Python と pyODBC によって ODBC ドライバーでのダイアログの表示が許可されている場合に機能します。 このオプションは、Windows オペレーティング システムでのみ使用できます。 

### <a name="example-connection-string-for-azure-active-directory-interactive-authentication"></a>Azure Active Directory 対話型認証の接続文字列の例

次の例は、Azure Active Directory 対話型認証を指定する ODBC 接続文字列を提供します。

`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

ODBC ドライバーの認証オプションの詳細については、「[ODBC ドライバーでの Azure Active Directory の使用](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords)」を参照してください。

## <a name="next-steps"></a>次のステップ
  
詳細については、 [Python デベロッパー センター](https://azure.microsoft.com/develop/python/)を参照してください。
