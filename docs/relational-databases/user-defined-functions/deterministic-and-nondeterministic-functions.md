---
description: 決定的関数と非決定的関数
title: 決定的関数と非決定的関数 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- built-in functions [SQL Server]
- nondeterministic functions
- extended stored procedures [SQL Server], functions that call
- deterministic functions
- user-defined functions [SQL Server], deterministic
ms.assetid: 2f3ce5f5-c81c-4470-8141-8144d4f218dd
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2665ab9b5a30209a123056664921334ce3c8367
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485308"
---
# <a name="deterministic-and-nondeterministic-functions"></a>決定的関数と非決定的関数
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  決定的関数は、一連の特定の入力値で呼び出され、かつデータベースの状態が同じ場合は、必ず同じ結果を返します。 非決定的関数は、アクセスするデータベースの状態が同じ場合でも、一連の特定の入力値で呼び出すたびに、異なる結果を返すことがあります。 たとえば、AVG 関数は、上記の制限を前提として常に同じ結果を返しますが、現在の datetime 値を返す GETDATE 関数によって返される結果は常に異なります。  
  
 ユーザー定義関数には、関数を呼び出す計算列のインデックスを使用するか、または関数を参照するインデックス付きビューを使用して、関数の結果にインデックスを作成する [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の機能を決定する複数のプロパティがあります。 関数の決定性は、このようなプロパティの 1 つです。 たとえば、ビューがなんらかの非決定的関数を参照している場合、そのビューにはクラスター化インデックスを作成できません。 関数の決定性など、関数のプロパティの詳細については、「 [ユーザー定義関数](../../relational-databases/user-defined-functions/user-defined-functions.md)」を参照してください。  
  
 このトピックでは、組み込みのシステム関数の決定性について説明し、ユーザー定義関数の決定的なプロパティに拡張ストアド プロシージャへの呼び出しが含まれている場合のこのプロパティへの影響を確認します。  
  
## <a name="built-in-function-determinism"></a>組み込み関数の決定性  
 組み込み関数の決定性には、影響を与えることができません。 各組み込み関数が決定的であるか非決定的であるかは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]による関数の実装方法に基づきます。 たとえば、クエリに ORDER BY 句を指定しても、そのクエリで使用される関数の決定性は変わりません。  
  
 [FORMAT](../../t-sql/functions/format-transact-sql.md) を除き、組み込みの文字列関数はすべて決定的関数になります。 文字列関数の一覧については、「[文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)」を参照してください。  
  
 文字列関数以外のカテゴリに属する次の組み込み関数は、常に決定的関数になります。  
  
:::row:::
    :::column:::
        ABS
    :::column-end:::
    :::column:::
        DATEDIFF
    :::column-end:::
    :::column:::
        POWER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ACOS
    :::column-end:::
    :::column:::
        DAY
    :::column-end:::
    :::column:::
        RADIANS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ASIN
    :::column-end:::
    :::column:::
        DEGREES
    :::column-end:::
    :::column:::
        ROUND
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ATAN
    :::column-end:::
    :::column:::
        EXP
    :::column-end:::
    :::column:::
        SIGN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ATN2
    :::column-end:::
    :::column:::
        FLOOR
    :::column-end:::
    :::column:::
        SIN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CEILING
    :::column-end:::
    :::column:::
        ISNULL
    :::column-end:::
    :::column:::
        SQUARE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COALESCE
    :::column-end:::
    :::column:::
        ISNUMERIC
    :::column-end:::
    :::column:::
        SQRT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COS
    :::column-end:::
    :::column:::
        LOG
    :::column-end:::
    :::column:::
        TAN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COT
    :::column-end:::
    :::column:::
        LOG10
    :::column-end:::
    :::column:::
        YEAR
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DATALENGTH
    :::column-end:::
    :::column:::
        MONTH
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [DATEADD]
    :::column-end:::
    :::column:::
        NULLIF
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
 次の関数は必ず決定的関数になるとは限りませんが、決定的な方法で指定されている場合は、インデックス付きビューまたは計算列のインデックスで使用できます。  
  
|機能|説明|  
|--------------|--------------|  
|すべての集計関数|OVER 句および ORDER BY 句で指定されていない限り、集計関数はすべて決定的です。 集計関数の一覧については、「[集計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)」を参照してください。|  
|CAST|**datetime**、 **smalldatetime**、または **sql_variant**と共に使用しない場合は、決定的関数になります。|  
|CONVERT|以下の条件に該当しない場合は決定的関数になります。<br /><br /> <br /><br /> ソースの型が **sql_variant**であること。<br /><br /> 変換先の型が **sql_variant** であり、変換元の型が非決定的であること。<br /><br /> 変換元または変換先の型が **datetime** または **smalldatetime**であり、他の変換元または変換先の型が文字列で、非決定的スタイルが指定されていること。 決定的にするには、スタイル パラメーターを定数にする必要があります。 また、スタイルが 20 および 21 以外で 100 以下の場合は非決定的です。 スタイルが 101 以上で、106、107、109、113 以外の場合は決定的です。|  
|CHECKSUM|CHECKSUM(*) を除き、決定的関数になります。|  
|ISDATE|CONVERT 関数と共に使用され、CONVERT スタイル パラメーターが指定されており、スタイルが 0、100、9、または 109 と等しくない場合にのみ決定的関数になります。|  
|RAND|RAND は、 *seed* パラメーターが指定されている場合にのみ決定的です。|  
  
 構成、カーソル、メタデータ、セキュリティ、およびシステム統計関数はすべて、非決定的関数です。 これらの関数の一覧については、「[構成関数 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)」、「[カーソル関数 &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)」、「[メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)」、「[セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)」、「[システム統計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)」を参照してください。  
  
 他のカテゴリに属する次の組み込み関数は、常に非決定的関数になります。  
  
:::row:::
    :::column:::
        @@CONNECTIONS
    :::column-end:::
    :::column:::
        GETDATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@CPU_BUSY
    :::column-end:::
    :::column:::
        GETUTCDATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@DBTS
    :::column-end:::
    :::column:::
        GET_TRANSMISSION_STATUS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IDLE
    :::column-end:::
    :::column:::
        LAG
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IO_BUSY
    :::column-end:::
    :::column:::
        LAST_VALUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@MAX_CONNECTIONS
    :::column-end:::
    :::column:::
        LEAD
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACK_RECEIVED
    :::column-end:::
    :::column:::
        MIN_ACTIVE_ROWVERSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACK_SENT
    :::column-end:::
    :::column:::
        NEWID
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACKET_ERRORS
    :::column-end:::
    :::column:::
        NEWSEQUENTIALID
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TIMETICKS
    :::column-end:::
    :::column:::
        NEXT VALUE FOR
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_ERRORS
    :::column-end:::
    :::column:::
        NTILE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_READ
    :::column-end:::
    :::column:::
        PARSENAME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_WRITE
    :::column-end:::
    :::column:::
        PERCENTILE_CONT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        AT TIME ZONE
    :::column-end:::
    :::column:::
        PERCENTILE_DISC
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CUME_DIST
    :::column-end:::
    :::column:::
        PERCENT_RANK
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CURRENT_TIMESTAMP
    :::column-end:::
    :::column:::
        RAND
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DENSE_RANK
    :::column-end:::
    :::column:::
        RANK
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        FIRST_VALUE
    :::column-end:::
    :::column:::
        ROW_NUMBER
    :::column-end:::
:::row-end:::   
:::row:::
    :::column:::
        FORMAT
    :::column-end:::
    :::column:::
        TEXTPTR
    :::column-end:::
:::row-end:::
 
## <a name="calling-extended-stored-procedures-from-functions"></a>関数からの拡張ストアド プロシージャ呼び出し  
 拡張ストアド プロシージャはデータベースに副作用を及ぼす可能性があるため、拡張ストアド プロシージャを呼び出す関数は非決定的関数です。 副作用とはデータベースのグローバル状態の変更を指し、たとえば、テーブルの更新や、ファイルやネットワークなどの外部リソースの更新 (ファイルの変更、電子メール メッセージの送信) などが挙げられます。 ユーザー定義関数から拡張ストアド プロシージャを実行した場合は、一貫性のある結果セットが返される保証はありません。 データベースに副作用を与えるユーザー定義関数の使用はお勧めしません。  
  
 拡張ストアド プロシージャは、関数の中から呼び出されると、クライアントに結果セットを返すことができません。 クライアントに結果セットを返すすべてのオープン データ サービス API のリターン コードは、FAIL になります。  
  
 拡張ストアド プロシージャは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続し直すことができますが、 その拡張ストアド プロシージャを呼び出した元の関数と同じトランザクションに参加することはできません。  
  
 拡張ストアド プロシージャは、バッチまたはストアド プロシージャから呼び出された場合と同様に、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] を実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows セキュリティ アカウントのコンテキストで実行されます。 拡張ストアド プロシージャの所有者は、プロシージャを実行する権限を他のユーザーに許可するときに、このセキュリティ コンテキストのアクセス許可を考慮する必要があります。  
  
  
