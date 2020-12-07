---
description: ストアド プロシージャから返される配列パラメーター
title: ストアドプロシージャから配列パラメーターを返す |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 2018069b-da5d-4cee-a971-991897d4f7b5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6b18921e027e16f322c47da9757ef9c8ee7f1aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449284"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>ストアド プロシージャから返される配列パラメーター
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 Oracle 7.3 では、pl/sql プログラム以外の種類の PL/SQL レコードにアクセスする方法はありません。 パッケージ化されたプロシージャまたは関数に仮引数が PL/SQL レコード型として定義されている場合、その仮引数をパラメーターとしてバインドすることはできません。 Microsoft ODBC Driver for Oracle の PL/SQL テーブル型を使用して、正しいエスケープシーケンスを含むプロシージャから配列パラメーターを呼び出します。  
  
 プロシージャを呼び出すには、次の構文を使用します。  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  パラメーターには、 \<max-records-requested> 結果セットに含まれる行数以上の値を指定する必要があります。 それ以外の場合、Oracle は、ドライバーによってユーザーに渡されるエラーを返します。  
>   
>  PL/SQL レコードを配列パラメーターとして使用することはできません。 各配列パラメーターは、データベーステーブルの1つの列のみを表すことができます。  
  
 次の例では、異なる結果セットを返す2つのプロシージャを含むパッケージを定義し、パッケージから結果セットを返す2つの方法を提供します。  
  
## <a name="package-definition"></a>パッケージ定義:  
  
```  
CREATE OR REPLACE PACKAGE SimplePackage AS  
  
TYPE t_id is TABLE of  NUMBER(5)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Course is TABLE of VARCHAR2(10)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Dept is TABLE of VARCHAR2(5)  
    INDEX BY BINARY_INTEGER;  
  
PROCEDURE proc1  
   (  
   o_id             OUT    t_id,  
   ao_course       OUT    t_Course,  
   ao_dept         OUT    t_Dept  
   );  
  
TYPE t_pk1Type1 IS TABLE OF VARCHAR2(100) INDEX BY BINARY_INTEGER;  
TYPE t_pk1Type2 IS TABLE OF NUMBER INDEX BY BINARY_INTEGER;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   );  
  
END SimplePackage;  
  
CREATE OR REPLACE PACKAGE BODY SimplePackage AS  
    PROCEDURE  proc1 ( o_id OUT t_id,  
    ao_course OUT t_Course, ao_dept OUT t_Dept   ) AS  
    BEGIN  
          o_id(1):= 200;  
          ao_course(1) :=  'M101';  
          ao_dept(1) :=  'EEE' ;  
  
          o_id(2) := 201;  
          ao_course(2) :=  'PHY320';  
          ao_dept(2) :=  'ECE' ;  
  
     END proc1;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   )  
AS  
   i   NUMBER;  
BEGIN  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg2(i) := 'Row Number ' || to_char(i);  
   END LOOP;  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg3(i) := i;  
   END LOOP;  
END proc2;  
END SimplePackage;  
```  
  
#### <a name="to-invoke-procedure-proc1"></a>プロシージャ手順1を呼び出すには  
  
1.  1つの結果セット内のすべての列を返します。  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  各列を1つの結果セットとして返します。  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     これにより、各列に1つずつ、3つの結果セットが返されます。  
  
#### <a name="to-invoke-procedure-proc2"></a>プロシージャ手順2を呼び出すには  
  
1.  1つの結果セット内のすべての列を返します。  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  各列を1つの結果セットとして返します。  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 [Sqlmoreresults](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) API を使用して、アプリケーションがすべての結果セットをフェッチするようにします。 詳細については、 *ODBC プログラマーズリファレンス*を参照してください。  
  
> [!NOTE]  
>  ODBC Driver for Oracle version 2.0 では、PL/SQL 配列を返す Oracle 関数を使用して結果セットを返すことはできません。
