---
description: sp_OAGetErrorInfo (Transact-sql)
title: sp_OAGetErrorInfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 89bb7dff2131d8463e26754148aa6e8032503fd7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546018"
---
# <a name="sp_oageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  OLE オートメーションのエラー情報を取得します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_OAGetErrorInfo [ objecttoken ]  
    [ , source OUTPUT ]   
    [ , description OUTPUT ]   
    [ , helpfile OUTPUT ]   
    [ , helpid OUTPUT ]   
```  
  
## <a name="arguments"></a>引数  
 *objecttoken*  
 は、以前に **sp_OACreate** を使用して作成された OLE オブジェクトのオブジェクトトークンであるか、または NULL です。 *Objecttoken*が指定されている場合、そのオブジェクトのエラー情報が返されます。 NULL が指定されている場合は、バッチ全体のエラー情報が返されます。  
  
 _ソース_**出力**  
 エラー情報のソースです。 指定する場合は、ローカルの **char**、 **nchar**、 **varchar**、または **nvarchar** 変数である必要があります。 戻り値は、必要に応じて、ローカル変数に合うように切り捨てられます。  
  
 _説明_の **出力**  
 エラーの説明を示します。 指定する場合は、ローカルの **char**、 **nchar**、 **varchar**、または **nvarchar** 変数である必要があります。 戻り値は、必要に応じて、ローカル変数に合うように切り捨てられます。  
  
 _helpfile_の **出力**  
 OLE オブジェクトのヘルプ ファイルです。 指定する場合は、ローカルの **char**、 **nchar**、 **varchar**、または **nvarchar** 変数である必要があります。 戻り値は、必要に応じて、ローカル変数に合うように切り捨てられます。  
  
 _helpid_の **出力**  
 ヘルプファイルのコンテキスト ID を示します。 指定する場合は、ローカルの **int** 変数である必要があります。  
  
> [!NOTE]  
>  このストアドプロシージャのパラメーターは、名前ではなく位置によって指定されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0以外の数 (失敗)。これは、OLE オートメーションオブジェクトによって返される HRESULT の整数値です。  
  
 HRESULT のリターンコードの詳細については、「 [OLE オートメーションのリターンコードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)」を参照してください。  
  
## <a name="result-sets"></a>結果セット  
 出力パラメーターを指定しない場合、エラー情報は結果セットとしてクライアントに返されます。  
  
|列名|データ型|説明|  
|------------------|---------------|-----------------|  
|**Error**|**バイナリ (4)**|エラー番号のバイナリ表現。|  
|**ソース**|**nvarchar (nn)**|エラーのソース。|  
|**説明**|**nvarchar (nn)**|エラーの説明。|  
|**ヘルプ**|**nvarchar (nn)**|ソースのヘルプファイルです。|  
|**HelpID**|**int**|ヘルプソースファイル内のヘルプコンテキスト ID。|  
  
## <a name="remarks"></a>解説  
 OLE オートメーションストアドプロシージャを呼び出すたびに ( **sp_OAGetErrorInfo**を除く)、エラー情報がリセットされます。したがって、 **sp_OAGetErrorInfo** は、最新の OLE オートメーションストアドプロシージャ呼び出しのエラー情報のみを取得します。 **Sp_OAGetErrorInfo**によってエラー情報がリセットされないため、同じエラー情報を取得するために複数回呼び出すことができます。  
  
 次の表は、OLE オートメーション エラーと一般的な原因の一覧です。  
  
|エラーおよび HRESULT|一般的な原因|  
|-----------------------|------------------|  
|**変数型が不正です&amp;#x2028;(0x80020008)**|メソッドパラメーター [!INCLUDE[tsql](../../includes/tsql-md.md)] として渡された値のデータ型が、メソッドパラメーターのデータ型と一致しなかった [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] か、またはメソッドパラメーターとして NULL 値が渡されました。|  
|**不明な名前です&amp;#x2028;(0x8002006)**|指定したプロパティ名またはメソッド名が、指定したオブジェクトに見つかりませんでした。|  
|**無効なクラス文字列です&amp;#x2028;(0x800401f3)**|指定した ProgID または CLSID は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに OLE オブジェクトとして登録されていません。 **Sp_OACreate**を使用してインスタンス化するには、事前にカスタム OLE オートメーションサーバーを登録しておく必要があります。 これを行うには、インプロセス (.dll) サーバーの場合は Regsvr32.exe ユーティリティを使用し、ローカル (.exe) サーバーの場合 **はコマンドライン** スイッチを使用します。|  
|**サーバーの実行に失敗しました (0x80080005)**|指定した OLE オブジェクトは、ローカル OLE サーバー (.exe ファイル) として登録されていますが、.exe ファイルが見つからないか、起動できません。|  
|**指定されたモジュールが見つかりませんでした&amp;#x2028;(0x8007007e)**|指定された OLE オブジェクトは、インプロセス OLE サーバー (.dll ファイル) として登録されていますが、.dll ファイルが見つからないか、または読み込めませんでした。|  
|**型が一致しません&amp;#x2028;(0x80020005)**|プロパティ値またはメソッドの戻り値を格納するために使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] ローカル変数のデータ型が、プロパティ値またはメソッドの戻り値の [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] データ型と一致しません。 または、プロパティやメソッドの戻り値を要求しましたが、そのプロパティやメソッドで戻り値が返されません。|  
|**Sp_OACreate の ' context ' パラメーターのデータ型または値が無効です。(0x8004275B)**|コンテキスト パラメーターの値は 1、4、5 のいずれかであることが必要です。|  
  
 HRESULT のリターンコードの処理の詳細については、「 [OLE オートメーションのリターンコードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバーシップ、またはこのストアドプロシージャに対して直接実行権限が必要です。 `Ole Automation Procedures` OLE オートメーションに関連するシステムプロシージャを使用するには、構成を **有効** にする必要があります。  
  
## <a name="examples"></a>例  
 次の例では、OLE オートメーションのエラー情報を表示します。  
  
```  
DECLARE @output varchar(255);  
DECLARE @hr int;  
DECLARE @source varchar(255);  
DECLARE @description varchar(255);  
PRINT 'OLE Automation Error Information';  
EXEC @hr = sp_OAGetErrorInfo @object, @source OUT, @description OUT;  
IF @hr = 0  
BEGIN  
    SELECT @output = '  Source: ' + @source  
    PRINT @output  
    SELECT @output = '  Description: ' + @description  
    PRINT @output  
END  
ELSE  
BEGIN  
    PRINT '  sp_OAGetErrorInfo failed.'  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;の OLE オートメーションストアドプロシージャ ](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
