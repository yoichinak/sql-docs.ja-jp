---
title: 手順 3:Node.js を使用して SQL に接続する
description: この例は、node.js を使用して SQL に接続する方法を示す概念実証と考える必要があり、わかりやすくするために簡略化されています。
ms.custom: ''
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5d5b41b6-129a-40b1-af8b-7e8fbd4a84bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e14732ac763271b867482f4b127c8c69ec1673a
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100347012"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-nodejs"></a>手順 3:Node.js を使用した SQL への接続を概念実証する

![ダウンロード-ダウン矢印-](../../ssms/media/download-icon.png)[NODE.JS SQL ドライバーをダウンロードする](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

この例は概念実証としてのみ検討してください。  わかりやすさのためにサンプル コードは簡略化されており、Microsoft が推奨するベスト プラクティスを表しているとは限りません。 GitHub には、同じ重要な機能を使用する他の例があります。

- [https://github.com/tediousjs/tedious/blob/master/examples/](https://github.com/tediousjs/tedious/blob/master/examples/)
  
## <a name="step-1-connect"></a>手順 1:接続する  
  
**新しい Connection** 関数は、SQL Database に接続するために使用します。  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        server: 'your_server.database.windows.net',  //update me
        authentication: {
            type: 'default',
            options: {
                userName: 'your_username', //update me
                password: 'your_password'  //update me
            }
        },
        options: {
            // If you are on Microsoft Azure, you need encryption:
            encrypt: true,
            database: 'your_database'  //update me
        }
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.
        console.log("Connected");  
    });
    
    connection.connect();

```  
  
## <a name="step-2--execute-a-query"></a>手順 2:クエリを実行する  
  
  
**新しい Request()** 関数 を使用して、すべての SQL ステートメントが実行されます。 ステートメントが SELECT ステートメントなどの行を返す場合は、**request.on()** 関数を使用してそれらを取得することができます。 行が存在しない場合、request.on() 関数からは空のリストが返されます。  
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        server: 'your_server.database.windows.net',  //update me
        authentication: {
            type: 'default',
            options: {
                userName: 'your_username', //update me
                password: 'your_password'  //update me
            }
        },
        options: {
            // If you are on Microsoft Azure, you need encryption:
            encrypt: true,
            database: 'your_database'  //update me
        }
    }; 
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement();  
    });  
    
    connection.connect();
  
    var Request = require('tedious').Request;  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement() {  
        request = new Request("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;", function(err) {  
        if (err) {  
            console.log(err);}  
        });  
        var result = "";  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                result+= column.value + " ";  
              }  
            });  
            console.log(result);  
            result ="";  
        });  
  
        request.on('done', function(rowCount, more) {  
        console.log(rowCount + ' rows returned');  
        });  
        connection.execSql(request);  
    }  
```  
  
## <a name="step-3-insert-a-row"></a>手順 3:行を挿入する  
  
この例では、[SQL インジェクション](../../relational-databases/security/sql-injection.md)の値からアプリケーションを保護するパラメーターを渡して、[INSERT](../../t-sql/statements/insert-transact-sql.md) ステートメントを安全に実行する方法を示します。    
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        server: 'your_server.database.windows.net',  //update me
        authentication: {
            type: 'default',
            options: {
                userName: 'your_username', //update me
                password: 'your_password'  //update me
            }
        },
        options: {
            // If you are on Microsoft Azure, you need encryption:
            encrypt: true,
            database: 'your_database'  //update me
        }
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement1();  
    });
    
    connection.connect();
    
    var Request = require('tedious').Request  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement1() {  
        request = new Request("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES (@Name, @Number, @Cost, @Price, CURRENT_TIMESTAMP);", function(err) {  
         if (err) {  
            console.log(err);}  
        });  
        request.addParameter('Name', TYPES.NVarChar,'SQL Server Express 2014');  
        request.addParameter('Number', TYPES.NVarChar , 'SQLEXPRESS2014');  
        request.addParameter('Cost', TYPES.Int, 11);  
        request.addParameter('Price', TYPES.Int,11);  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                console.log("Product id of inserted item is " + column.value);  
              }  
            });  
        });       
        connection.execSql(request);  
    }  
```  
