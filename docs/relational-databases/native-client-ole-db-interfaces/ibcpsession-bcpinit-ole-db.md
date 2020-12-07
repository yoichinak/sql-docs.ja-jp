---
description: 'IBCPSession:: BCPInit (Native Client OLE DB provider)'
title: 'IBCPSession:: BCPInit (Native Client OLE DB provider) |Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IBCPSession::BCPInit (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPInit method
ms.assetid: 583096d7-da34-49be-87fd-31210aac81aa
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d6d603ccad5effd5e7955007fd79d2386a3709af
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081641"
---
# <a name="ibcpsessionbcpinit-native-client-ole-db-provider"></a>IBCPSession:: BCPInit (Native Client OLE DB Provider)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  一括コピー構造を初期化し、エラー チェックを実行して、データ ファイルとフォーマット ファイルの名前が正しいことを確認します。その後、それらのファイルを開きます。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT BCPInit(   
      const wchar_t *pwszTable,  
      const wchar_t *pwszDataFile,  
      const wchar_t *pwszErrorFile,  
      int eDirection);  
```  
  
## <a name="remarks"></a>解説  
 **BCPInit** メソッドは、他のすべての一括コピー メソッドの前に呼び出す必要があります。 **BCPInit** メソッドにより、ワークステーションと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との間のデータの一括コピーに必要な初期化が実行されます。  
  
 **BCPInit** メソッドは、データ ファイルではなく、データベースのコピー元テーブルまたはコピー先テーブルの構造を調べます。 また、データベース テーブル、ビュー、または SELECT 結果セット内の各列に基づいてデータ ファイルのデータ形式値を指定します。 このデータ形式値には、各列のデータ型、長さや NULL のインジケーターとターミネータのバイト文字列がデータ内に存在するかどうか、および固定長データ型の幅の指定などが含まれます。 **BCPInit** メソッドでは、これらの値を次のように設定します。  
  
-   指定するデータ型は、データベース テーブル、ビュー、または SELECT 結果セット内の列のデータ型です。 データ型は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native Client ヘッダーファイル (sqlncli) で指定されたネイティブデータ型によって列挙されます。 列挙される値の形式は、BCP_TYPE_XXX です。 データはそのコンピューターの形式で表されます。 つまり、integer データ型の列のデータは、データ ファイルを作成したコンピューターに基づいて、ビッグ エンディアンまたはリトル エンディアンの 4 バイト シーケンスで表されます。  
  
-   データベースのデータ型が固定長の場合は、データ ファイルのデータも固定長になります。 データを処理する一括コピー メソッド ([IBCPSession::BCPExec](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md) など) では、データ行が解析されます。データ ファイル内のデータの長さは、データベース テーブル、ビュー、または SELECT 列リスト内で指定されるデータの長さと同じでなければなりません。 たとえば、`char(13)` で定義されているデータベース列のデータは、ファイル内の各データ行に 13 文字で表す必要があります。 データベース列で NULL 値を許容する場合は、固定長データにプレフィックスとして NULL インジケーターを付けることができます。  
  
-   データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にコピーするときは、データ ファイルにデータベース テーブル内の各列に格納するデータが含まれている必要があります。 データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からコピーするときは、データベース テーブル、ビュー、または SELECT 結果セット内のすべての列のデータがデータ ファイルにコピーされます。  
  
-   データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にコピーするときは、データ ファイル内の列の序数位置がデータベース テーブル内の列の序数位置と同じであることが必要です。 データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からコピーするときは、**BCPExec** メソッドによりデータベース テーブル内の列の序数位置に基づいてデータが配置されます。  
  
-   データベースのデータ型が可変長 (`varbinary(22)` など) の場合、またはデータベース列に NULL 値を格納できる場合は、データ ファイル内のデータにプレフィックスとして長さのインジケーターや NULL インジケーターを付けることができます。 インジケーターの幅は、データ型と一括コピーのバージョンによって異なります。 [IBCPSession::BCPControl](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) メソッドのオプションである BCP_OPTION_FILEFMT では、データ内のインジケーターの幅が必要な幅より狭くなる時点を示すことで、以前の一括コピー データ ファイルと最新バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているサーバーとの間の互換性を確保しています。  
  
> [!NOTE]  
>  データ ファイルに指定したデータ形式値を変更するには、[IBCPSession::BCPColumns](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) メソッドと [IBCPSession::BCPColFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) メソッドを使用します。  
  
 テーブルにインデックスが含まれていない場合は、データベース オプション **select into/bulkcopy** を設定することにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への一括コピーを最適化できます。  
  
## <a name="arguments"></a>引数  
 *pwszTable*[in]  
 コピー操作の対象になるデータベース テーブルの名前を指定します。 名前には、データベース名や所有者名を含めることができます。 たとえば、"pubs.username.titles"、"pubs..titles"、"username.titles" のように指定できます。  
  
 eDirection 引数を BCP_DIRECTION_OUT に設定すると、pwszTable 引数をデータベース ビューの名前にすることができます。  
  
 eDirection 引数を BCP_DIRECTION_OUT に設定し、**BCPExec** メソッドを呼び出す前に **BCPControl** メソッドを使用して SELECT ステートメントを指定する場合は、*pwszTable* 引数に NULL を設定する必要があります。  
  
 *pwszDataFile*[in]  
 コピー操作の対象になるユーザー ファイルの名前を指定します。  
  
 *pwszErrorFile*[in]  
 進行状況メッセージ、エラー メッセージ、およびユーザー ファイルからテーブルにコピーできなかった行のコピーを格納するエラー ファイルの名前を指定します。 *pwszErrorFile* 引数に NULL を設定すると、エラー ファイルが使用されません。  
  
 *eDirection*[in]  
 コピー操作の方向として、BCP_DIRECTION_IN か BCP_DIRECTION _OUT のいずれかを設定します。 BCP_DIRECTION _IN はユーザー ファイルからデータベース テーブルへのコピーを示します。BCP_DIRECTION _OUT はデータベース テーブルからユーザー ファイルへのコピーを示します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。詳細を確認するには、[ISQLServerErrorInfo](isqlservererrorinfo-geterrorinfo-ole-db.md) インターフェイスを使用してください。  
  
 E_OUTOFMEMORY  
 メモリ不足エラーです。  
  
 E_INVALIDARG  
 1 つ以上の引数が正しく指定されませんでした。 たとえば、無効なファイル名が指定されました。  
  
## <a name="see-also"></a>参照  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [一括コピー操作の実行](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
