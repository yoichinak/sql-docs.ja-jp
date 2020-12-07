---
description: sp_refresh_parameter_encryption (Transact-sql)
title: sp_refresh_parameter_encryption (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_refresh_parameter_encryption
- sp_refresh_parameter_encryption_TSQL
- sys.sp_refresh_parameter_encryption
- sys.sp_refresh_parameter_encryption_TSQL
helpviewer_keywords:
- sp_refresh_parameter_encryption
- Always Encrypted, sp_refresh_parameter_encryption
ms.assetid: 00b44baf-fcf0-4095-aabe-49fa87e77316
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b2172c7d17d9c3d9ebb6680fc7af0212c0a01e12
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526187"
---
# <a name="sp_refresh_parameter_encryption-transact-sql"></a>sp_refresh_parameter_encryption (Transact-sql)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

現在のデータベースのスキーマバインドされていないストアドプロシージャ、ユーザー定義関数、ビュー、DML トリガー、データベースレベルの DDL トリガー、またはサーバーレベルの DDL トリガーのパラメーターの Always Encrypted メタデータを更新します。 

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.sp_refresh_parameter_encryption [ @name = ] 'module_name' 
    [ , [ @namespace = ] '<class>' ]
[ ; ]

<class> ::=
{ DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER }
```

## <a name="arguments"></a>引数

`[ @name = ] 'module_name'` ストアドプロシージャ、ユーザー定義関数、ビュー、DML トリガー、データベースレベルの DDL トリガー、またはサーバーレベルの DDL トリガーの名前を指定します。 *module_name* を共通言語ランタイム (clr) ストアドプロシージャまたは clr 関数にすることはできません。 *module_name* をスキーマバインドにすることはできません。 の*module_name*はで `nvarchar` 、既定値はありません。 *module_name* にはマルチパート識別子を指定できますが、参照できるのは現在のデータベース内のオブジェクトだけです。

`[ @namespace = ] ' < class > '` は、指定されたモジュールのクラスです。 *Module_name*が DDL トリガーである場合 `<class>` は、が必要です。 `<class>` が `nvarchar(20)`です。 有効な入力値は `DATABASE_DDL_TRIGGER` 、と `SERVER_DDL_TRIGGER` です。    

## <a name="return-code-values"></a>リターン コードの値  

0 (成功) または0以外の数値 (失敗)


## <a name="remarks"></a>解説

次の場合、モジュールのパラメーターの暗号化メタデータが古くなる可能性があります。   
* モジュールが参照しているテーブル内の列の暗号化プロパティが更新されました。 たとえば、列が削除され、同じ名前の新しい列が存在しますが、別の暗号化の種類、暗号化キー、または暗号化アルゴリズムが追加されています。  
* モジュールは、古いパラメーター暗号化メタデータを使用して別のモジュールを参照しています。  

テーブルの暗号化プロパティが変更された場合、は、 `sp_refresh_parameter_encryption` 直接または間接的にテーブルを参照しているモジュールに対して実行する必要があります。 このストアドプロシージャは、これらのモジュールで任意の順序で呼び出すことができます。ユーザーは、最初に内部モジュールを更新してから呼び出し元に移動する必要がありません。

`sp_refresh_parameter_encryption` は、 `SET` オブジェクトに関連付けられている権限、拡張プロパティ、またはオプションには影響しません。 

サーバーレベルの DDL トリガーを更新するには、任意のデータベースのコンテキストからこのストアドプロシージャを実行します。

> [!NOTE]
>  オブジェクトに関連付けられている署名は、の実行時に削除され `sp_refresh_parameter_encryption` ます。

## <a name="permissions"></a>アクセス許可

`ALTER`モジュールに対する権限と `REFERENCES` 、オブジェクトによって参照される CLR ユーザー定義型および XML スキーマコレクションに対する権限が必要です。   

指定されたモジュールがデータベースレベルの DDL トリガーである場合は、現在のデータベースの権限が必要です `ALTER ANY DATABASE DDL TRIGGER` 。    

指定されたモジュールがサーバーレベルの DDL トリガーである場合は、権限が必要 `CONTROL SERVER` です。

句を使用して定義されているモジュールの場合 `EXECUTE AS` 、 `IMPERSONATE` 指定されたプリンシパルに対する権限が必要です。 一般に、オブジェクトを更新してもプリンシパルは変更されません `EXECUTE AS` 。ただし、モジュールがで定義されていて、 `EXECUTE AS USER` プリンシパルのユーザー名が、モジュールが作成されたときとは別のユーザーに解決されるようになった場合を除きます。
 
## <a name="examples"></a>例

次の例では、テーブルと、テーブルを参照するプロシージャを作成し、Always Encrypted を構成して、テーブルを変更してプロシージャを実行する方法を示し `sp_refresh_parameter_encryption` ます。  

まず、最初のテーブルと、テーブルを参照するストアドプロシージャを作成します。
```sql
CREATE TABLE [Patients]([PatientID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11), 
    [FirstName] [nvarchar](50) NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [MiddleName] [nvarchar](50) NULL,
    [StreetAddress] [nvarchar](50) NOT NULL,
    [City] [nvarchar](50) NOT NULL,
    [ZipCode] [char](5) NOT NULL,
    [State] [char](2) NOT NULL,
    [BirthDate] [date] NOT NULL,
 CONSTRAINT [PK_Patients] PRIMARY KEY CLUSTERED 
(
    [PatientID] ASC
) WITH 
    (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, 
     IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, 
     ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY];
GO

CREATE PROCEDURE [find_patient] @SSN [char](11)
AS
BEGIN
    SELECT * FROM [Patients] WHERE SSN=@SSN
END;
GO
```

次に、Always Encrypted キーを設定します。
```sql
CREATE COLUMN MASTER KEY [CMK1]
WITH
(
       KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305'
);
GO

CREATE COLUMN ENCRYPTION KEY [CEK1]
WITH VALUES
(
       COLUMN_MASTER_KEY = [CMK1],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 
       0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085
);
GO
```


最後に、SSN 列を暗号化された列に置き換え、プロシージャを実行して `sp_refresh_parameter_encryption` Always Encrypted コンポーネントを更新します。
```sql
ALTER TABLE [Patients] DROP COLUMN [SSN];
GO

ALTER TABLE [Patients] 
    ADD [SSN] [char](11) COLLATE Latin1_General_BIN2 
    ENCRYPTED WITH 
        (COLUMN_ENCRYPTION_KEY = [CEK1], 
        ENCRYPTION_TYPE = Deterministic, 
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') 
    NOT NULL;
GO

EXEC sp_refresh_parameter_encryption [find_patient];
GO
```

## <a name="see-also"></a>参照 

[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Always Encrypted ウィザード](../../relational-databases/security/encryption/always-encrypted-wizard.md)   

