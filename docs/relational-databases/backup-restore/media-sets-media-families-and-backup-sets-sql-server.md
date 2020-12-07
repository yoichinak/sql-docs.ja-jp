---
title: メディア セット、メディア ファミリ、およびバックアップ セット
description: この記事では、SQL Server でのバックアップと復元で使用される、メディア セット、メディア ファミリ、およびバックアップ セットの概要について説明します。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod_service: backup-restore
ms.reviewer: ''
ms.prod: sql
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- media sets [SQL Server], about media sets
- backup media [SQL Server], about backup media
- backups [SQL Server], media sets
- media sets [SQL Server]
- media headers [SQL Server]
- backup sets [SQL Server], about backup sets
- backup media [SQL Server], media sets
- backups [SQL Server], media families
- backup media [SQL Server], media families
- media families [SQL Server]
- backups [SQL Server], backup sets
- backup sets [SQL Server]
ms.assetid: 2b8f19a2-ee9d-4120-b194-fbcd2076a489
author: cawrites
ms.author: chadam
ms.openlocfilehash: d9a264d6b5248f4033dd1bd3e282de4872cd2eb6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130395"
---
# <a name="media-sets-media-families-and-backup-sets-sql-server"></a>メディア セット、メディア ファミリ、およびバックアップ セット (SQL Server)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を初めて使用するユーザーを対象とし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のバックアップと復元で使用する基本的なバックアップ メディア用語を紹介します。** 
  
  ここでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でバックアップ メディアに使用する形式、バックアップ メディアとバックアップ デバイス間の対応付け、バックアップ メディアでのバックアップの構成、メディア セットとメディア ファミリに関するいくつかの注意点について説明します。 古いメディア セットを新しいメディア セットと交換する前に行うバックアップ メディアの初期化およびフォーマット処理の手順、メディア セット内の古いバックアップ セットを上書きする方法、新しいバックアップ セットをメディア セットに追加する方法についても説明します。  
  
>**注:** Azure Blob Storage サービスへの SQL Server のバックアップについて詳しくは、「[Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」をご覧ください。  
   
##  <a name="terms"></a><a name="TermsAndDefinitions"></a> 用語  
 **メディア セット (media set)**  
 テープやディスク ファイルなどのバックアップ メディアに順番を付けてまとめたもの。バックアップ メディアには、1 回以上のバックアップ操作によって、固定型の複数のバックアップ デバイスを使用して書き込まれます。  
  
 **メディア ファミリ (media family)**  
 ミラー化されていない単一のデバイスまたはメディア セット内のミラー化されている一連のデバイスで作成されたバックアップ。  
  
**バックアップ セット (backup set)**  
 正常に完了したバックアップ操作によってメディア セットに追加されるバックアップ コンテンツ。  
  

##  <a name="overview-of-media-sets-media-families-and-backup-sets"></a><a name="OvMediaSetsFamiliesBackupSets"></a> メディア セット、メディア ファミリ、およびバックアップ セットの概要  
 1 つまたは複数の一連のバックアップ メディアにあるバックアップによって、1 つのメディア セットが構成されます。 *"メディア セット"* とは、テープやディスク ファイル、Azure BLOB などの *"バックアップ メディア"* の順序付きコレクションのことです。バックアップ メディアは、1 つまたは複数のバックアップ操作によって、固定型の多数のバックアップ デバイスを使用して書き込まれています。 1 つのメディア セットでは、テープ ドライブ、ディスク ドライブ、または Azure BLOB を使用しますが、これらの複数を組み合わせることはありません。 
 
**例:** あるメディア セットに関連付けられているバックアップ デバイスが、`\\.\TAPE0`、`\\.\TAPE1`、`\\.\TAPE2` という 3 台のテープ ドライブである場合を想定します。 このメディア セットにはテープのみが含まれます。テープの数は最低 3 本です (デバイスごとに 1 本)。 バックアップ デバイスの種類と台数はメディア セットの作成時に決定され、変更できません。 ただし、必要に応じて、バックアップ操作と復元操作の間に特定のデバイスを同じ種類のデバイスと交換できます。  
  
 メディア セットは、バックアップ メディアをフォーマットすることによって、バックアップ操作中にバックアップ メディア上に作成されます。 詳細については、このトピックの「 [新しいメディア セットの作成](#CreatingMediaSet)」をご覧ください。 フォーマットが終了すると、各ファイルまたはテープにメディア セット用のメディア ヘッダーが書き込まれ、バックアップ コンテンツの受け入れ準備が整います。 ヘッダーが書き込まれると、バックアップ操作用に指定されているすべてのバックアップ デバイス上のバックアップ メディアに指定のデータをバックアップする作業に進みます。  
  
> **注:** メディア セットは、メディア ボリューム (テープまたはディスク ファイル) の破損に備えてミラー化できます。 詳細については、「 [ミラー化バックアップ メディア セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)」を参照してください。  
  
 圧縮されたバックアップと圧縮されていないバックアップを 1 つのメディア セット内で同時に作成することはできません。 圧縮されたバックアップは、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のどのエディションでも読み取ることができます。 詳細については、「[バックアップの圧縮 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)」を参照してください。  

  
## <a name="media-families"></a>メディア ファミリ  
 *メディア ファミリ* とは、ミラー化されていない単一のデバイスまたはメディア セット内のミラー化されている一連のデバイスで作成されたバックアップの集合です。 メディア セット用に使用されているバックアップ デバイスの数によって、メディア セット内のメディア ファミリの数が決まります。 たとえば、ミラー化されていない 2 つのバックアップ デバイスを使用しているメディア セットには、2 つのメディア ファミリが含まれます。  
  
ミラー化メディア セットでは、各メディア ファミリがミラー化されます。 たとえば、6 つのバックアップ デバイスを使用して 1 つのメディア セットをフォーマットし、そのメディア セットで 2 つのミラーが使用されている場合は、3 つのメディア ファミリがあります。各ファミリには、2 つの同等のバックアップ データ コピーが含まれています。 ミラー化メディア セットの詳細については、[ミラー化バックアップ メディア セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)」を参照してください。  
  
 メディア ファミリ内の各テープまたはディスクには、 *メディア シーケンス番号* が割り当てられています。 ディスクのメディア シーケンス番号は常に 1 です。 テープ メディア ファミリでは、先頭テープのシーケンス番号が 1、2 番目のテープのシーケンス番号が 2 のように割り当てられます。 詳細については、このトピックの「 [メディア セット、メディア ファミリ、およびバックアップ セット (SQL Server)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。
  
## <a name="the-media-header"></a>メディア ヘッダー  
 バックアップ メディアの各ボリューム (ディスク ファイルまたはテープ) には、メディア ヘッダーが含まれています。メディア ヘッダーは、そのテープ (またはディスク) を使用する最初のバックアップ操作によって作成されます。 このヘッダーは、メディアが再フォーマットされるまでそのままの状態で維持されます。  
  
 メディア ヘッダーには、メディア (ディスク ファイルまたはテープ) を識別するために必要な情報と、そのメディアが属するメディア ファミリ内での位置を識別するために必要な情報がすべて含まれています。 次の情報が表示されます。  
  
-   メディア名。  
  
     メディア名は省略可能ですが、メディアを明確に識別するためにメディア名を常に使用することをお勧めします。 メディア名は、そのメディアをフォーマットしたユーザーが指定します。  
  
-   メディア セットの一意の識別番号。  
  
-   メディア セット内のメディア ファミリの数。  
  
-   このメディアを含んでいるメディア ファミリのシーケンス番号。  
  
-   メディア ファミリの一意の識別番号。  
  
-   メディア ファミリ内でのこのメディアのシーケンス番号。 ディスク ファイルの場合、この値は常に 1 になります。  
  
-   メディアの説明に MTF メディア ラベルまたはメディアの説明が含まれているかどうか。  
  
    >**注:** バックアップ操作または復元操作で使用するすべてのメディアには、MTF ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format) という標準のバックアップ形式が使用されます。 MTF が使用されていると、ユーザーは、MTF 固有の説明が含まれたテープ ラベルを指定できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、他のアプリケーションが書き込んだ MTF メディア ラベルが保持されますが、MTF メディア ラベルの書き込みは行われません。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format メディア ラベルまたはメディアの説明 (自由な形式のテキスト)。  
  
-   ラベルを作成したバックアップ ソフトウェアの名前。  
  
-   メディアをフォーマットしたソフトウェア ベンダーの一意のベンダー識別番号。  
  
-   ラベルが作成された日時。  
  
-   セット内のミラーの数 (1 ～ 4)。1 はミラー化されていないデバイスを示します。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でフォーマットされたメディアを処理できます。  
  
## <a name="backup-sets"></a>[バックアップ セット]  
 バックアップ操作が正常に行われると、メディア セットに 1 つの *バックアップ セット* が追加されます。 バックアップ セットは、バックアップが属するメディア セットの観点から表現されます。 バックアップ メディアにメディア ファミリが 1 つしかない場合は、そのファミリにバックアップ セット全体が含まれます。 バックアップ メディアが複数のメディア ファミリで構成されている場合、バックアップ セットはこれらのファミリ間で分散されます。 各メディアのバックアップ セットには、そのバックアップ セットを説明するヘッダーが含まれています。  
  
 この例は、バックアップ デバイスとして 3 つのテープ ドライブを使用し、 [!INCLUDE[tsql](../../includes/tsql-md.md)] データベース用に `MyAdvWorks_MediaSet_1` というメディア セットを作成する [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ステートメントを示しています。  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1', TAPE = '\\.\tape2'  
WITH   
   FORMAT,  
   MEDIANAME = 'MyAdvWorks_MediaSet_1'  
```  
  
 このバックアップ操作が正常に実行されると、新しいメディア ヘッダーを含む 1 つの新しいメディア セットと、3 つのテープに分散されている 1 つのバックアップ セットが作成されます。 次の図は、この結果を示しています。  
  
 ![メディア ヘッダーと最初のバックアップ セットを 3 つのテープに記録](../../relational-databases/backup-restore/media/bnr-mediaset-new.gif "メディア ヘッダーと最初のバックアップ セットを 3 つのテープに記録")  
  
 通常、メディア セットが作成されると、その後のバックアップ操作では、そのメディア セットにバックアップ セットが 1 つずつ追加されます。 関連するメディアまたはバックアップ デバイスの数にかかわらず、バックアップ セットで使用されるすべてのメディアによってメディア セットが構成されます。 バックアップ セットは、メディア セット内での位置に従ってシーケンス番号が付けられています。この番号により、どのバックアップ セットを復元するかを指定できます。  
  
 メディア セットに対するすべてのバックアップ操作で、同じ数および種類のバックアップ デバイスに書き込みを行う必要があります。 複数のデバイスがある場合は、最初のバックアップ セットと同様に、後続のすべてのバックアップ セットの内容が、すべてのデバイス上のバックアップ メディアに分散されます。 上記の例を続行するには、2 番目のバックアップ操作 (差分バックアップ) で同じメディア セットに情報を追加します。  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1', TAPE = '\\.\tape2'  
WITH   
   NOINIT,  
   MEDIANAME = 'AdventureWorksMediaSet1',  
   DIFFERENTIAL  
```  
  
> **注:** NOINIT オプションは既定ですが、わかりやすくするために含まれています。  
  
 2 番目のバックアップ操作が正常に終了すると、次のようにバックアップ内容を分散して、2 番目のバックアップ セットがメディア セットに書き込まれます。  
  
 ![2 つ目のバックアップ セットを 3 つのメディア セット テープにまたがって記録](../../relational-databases/backup-restore/media/bnr-mediaset-appendedto.gif "2 つ目のバックアップ セットを 3 つのメディア セット テープにまたがって記録")  
  
 バックアップを復元するとき、使用するバックアップを FILE オプションで指定できます。 次の例は、 **=** _データベースの完全バックアップを復元した後、同じメディア セットで差分バックアップを行う場合の FILE_ backup_set_file_number [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 句の使用法を示しています。 メディア セットでは 3 つのバックアップ テープが使用されます。テープが装着されているテープ ドライブは `\\.\tape0`、 `tape1`、および `tape2`です。  
  
```  
RESTORE DATABASE AdventureWorks2012 FROM TAPE = '\\.\tape0', TAPE = '\\.\tape1', TAPE = '\\.\tape2'  
   WITH   
   MEDIANAME = 'AdventureWorksMediaSet1',  
   FILE=1,   
   NORECOVERY;  
RESTORE DATABASE AdventureWorks2012 FROM TAPE = '\\.\tape0', TAPE = '\\.\tape1', TAPE = '\\.\tape2'   
   WITH   
   MEDIANAME = 'AdventureWorksMediaSet1',  
   FILE=2,   
   RECOVERY;  
GO  
```  
  
 メディア セット、メディア ファミリ、およびバックアップ セットに関する情報が保存される履歴テーブルの詳細については、[バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)」を参照してください。  
  
 メディア セット内のバックアップ メディアの数は、次のような要因によって決まります。  
  
-   バックアップ デバイスの数  
  
-   バックアップ デバイスの種類  
  
-   バックアップ セットの数  

  
##  <a name="creating-a-new-media-set"></a><a name="CreatingMediaSet"></a> Creating a new media set  
 新しいメディア セットを作成するには、バックアップ メディア (テープまたはディスク ファイル) をフォーマットする必要があります。 フォーマットを実行すると、バックアップ メディアが次のように変化します。  
  
1.  古いヘッダー (存在する場合) が削除され、その結果バックアップ メディアの以前の内容が削除されます。  
  
     テープ デバイスをフォーマットすると、現在マウントされているテープの以前の内容がすべて削除されます。 ディスクをフォーマットするときは、バックアップ操作に指定したファイルのみが影響を受けます。  
  
2.  各バックアップ デバイスのバックアップ メディア (テープまたはディスク ファイル) に新しいメディア ヘッダーが書き込まれます。  

  
##  <a name="backing-up-to-an-existing-media-set"></a><a name="UseExistingMediaSet"></a> 既存のメディア セットへのバックアップ  
 既存のメディア セットにバックアップする場合、次の 2 つの方法があります。  
  
-   既存のバックアップ セットに追加します。  
  
     使用可能な領域を最大限に使用するには、一般に、新しいバックアップ セットを既存のメディア セットに追加します。 新しいバックアップ セットを追加した場合も、以前のバックアップはすべて保持されます。 詳細については、このセクションの「 [既存のバックアップ セットへの追加](#Appending)」をご覧ください。  

追加は BACKUP ステートメントの既定の動作ですが、NOINIT オプションを使用して明示的に指定することもできます。  
  
-   既存のすべてのバックアップ セットを現在のバックアップで上書きします。現在のメディア ヘッダーはそのまま残します。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップには、メディアを間違って上書きしないための保護手段が備えられています。 ただし、あらかじめ定義した有効期限に達したバックアップ セットは、バックアップ操作により自動的に上書きできます。  
  
     テープ ヘッダーの場合は、ヘッダーをそのまま残すことに意味があります。 詳細については、このセクションの「 [バックアップ セットの上書き](#Overwriting)」をご覧ください。  

    >  既存のバックアップ セットの上書きは、BACKUP ステートメントの INIT オプションを使用して指定します。  
  
##  <a name="appending-to-existing-backup-sets"></a><a name="Appending"></a> Appending to existing backup sets  
 異なる時間に作成されたバックアップは、同じデータベースでも異なるデータベースでも同じメディアに記憶できます。 他のバックアップ セットを既存のメディアに追加すると、メディアの既存のコンテンツはそのまま保持され、メディア上の最後のバックアップの後に新しいバックアップが書き込まれます。  
  
 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により常に新しいバックアップがメディアに追加されます。 追加は、必ずメディアの最後に行われます。 たとえば、メディア ボリュームに 5 個のバックアップ セットが含まれている場合、最初の 3 個のバックアップ セットをスキップして、4 番目のバックアップ セットに新しいバックアップ セットを上書きすることはできません。  
  
 テープ バックアップに BACKUP WITH NOREWIND を使用すると、操作の最後にテープは開いたままになります。 その結果、テープを巻き戻し、再び前方向にスキャンして最後のバックアップ セットを見つける必要なく、テープにバックアップをさらに追加することができます。 **sys.dm_io_backup_tapes** 動的管理ビューで、開いているテープ ドライブの一覧を検索できます。詳細については、[sys.dm_io_backup_tapes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) をご覧ください。  
  
 Microsoft Windows バックアップと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップでは同じメディアを共有できますが、同時には使用できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップは、Windows データをバックアップできません。  
  
> **重要:** 圧縮されたバックアップと圧縮されていないバックアップを 1 つのメディア セット内で同時に作成することはできません。 圧縮されたバックアップは、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンのどのエディションでも読み取ることができます。 詳細については、「[バックアップの圧縮 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)」を参照してください。  
  
 
##  <a name="overwriting-backup-sets"></a><a name="Overwriting"></a> Overwriting backup sets  
 既存のバックアップ セットの上書きは、BACKUP ステートメントの INIT オプションを使用して指定します。 このオプションでは、メディア上のすべてのバックアップ セットが上書きされ、メディア ヘッダーがある場合は保持されます。 メディア ヘッダーが存在しない場合は作成されます。  
  
 テープ ヘッダーの場合は、ヘッダーをそのまま残すことに意味があります。 ディスク バックアップ メディアの場合、バックアップ操作で指定されたバックアップ デバイスが使用したファイルだけが上書きされます。ディスク上のそれ以外のファイルは上書きされません。 バックアップを上書きする場合、既存のメディア ヘッダーを保持し、新しいバックアップをバックアップ デバイスの初めてのバックアップとして作成できます。 既存のメディア ヘッダーがない場合、関連付けられたメディア名とメディアの説明が入った有効なメディア ヘッダーが自動的に書き込まれます。 既存のメディア ヘッダーが無効な場合、バックアップ操作は終了します。 メディアが空の場合、MEDIANAME、MEDIAPASSWORD、および MEDIADESCRIPTION が指定されていれば、それらを使用して新しいメディア ヘッダーが生成されます。  
  
 
 次のいずれかの条件が存在する場合、バックアップ メディアは上書きされません。  
  
-   メディア上の既存のバックアップ セットが失効していない (SKIP が指定されている場合、有効期限はチェックされません)。  
  
     有効期限は、バックアップの有効期間の完了日を指定しており、期限を過ぎると別のバックアップで上書きできるようになります。 有効期限はバックアップの作成時に指定できます。 既定では、有効期限は **sp_configure** で設定された **media retention** オプションによって決まります。 詳細については、「 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)」を参照してください。  
  
-   メディア名が指定されても、バックアップ メディア上の名前とは一致していない。  
  
     メディア名は、メディアを識別しやすくするためのわかりやすい名前です。  
  
 ただし、テープ上のバックアップが不要になったことがわかっているなど、既存のメディアに上書きできることが確かな場合は、このチェックを明示的にスキップできます。  
  
 バックアップ メディアが Microsoft Windows によってパスワードで保護されている場合、Microsoft SQL Server からメディアに書き込まれません。 パスワードで保護されたメディアに上書きするには、メディアを再初期化する必要があります。  
  

  
##  <a name="sequence-numbers"></a><a name="SequenceNumbers"></a> シーケンス番号  
 メディア セット内の複数のメディア ファミリ、またはメディア ファミリ内の複数のバックアップ メディアは、正しい順序で配置することが重要です。 このため、バックアップ時に次のようにシーケンス番号が割り当てられます。  
  
-   メディア セット内のシーケンシャル メディア ファミリ  
  
     メディア セット内のメディア ファミリには、メディア セット内の位置に応じて連番が割り当てられます。 メディア ファミリ番号は、 **backupmediafamily** テーブルの **family_sequence_number** 列に記録されます。  
  
-   メディア ファミリ内の物理メディア  
  
     メディア シーケンス番号は、メディア ファミリ内の物理メディアの順序を示しています。 先頭のバックアップ メディアのシーケンス番号は 1 なので、 1 が割り当てられます。2 番目のメディア、つまり最初の後続テープには 2 が割り当てられます。 バックアップ セットを復元するとき、このメディア シーケンス番号によって、オペレーターは適切なメディアを正しい順序でマウントできます。  
  
###  <a name="multiple-devices"></a><a name="MultipleDevices"></a> 複数のデバイス  
 複数のテープ ドライブまたはディスク ファイルを使用する場合は、次の点に注意してください。  
  
-   バックアップの場合  
  
     後続のバックアップ操作では、最初のバックアップ操作で作成したメディア セット全体を使用する必要があります。 たとえば、2 つのテープ バックアップ デバイスを使用して 1 つのメディア セットを作成した場合、同じメディア セットに関連した後続のすべてのバックアップ操作でも 2 つのバックアップ デバイスを使用する必要があります。  
  
-   復元の場合  
  
     ディスク バックアップからの復元とオンライン復元の場合、すべてのメディア ファミリを同時にマウントする必要があります。 テープ バックアップからのオフライン復元の場合は、ディスクの場合よりも少数のバックアップ デバイスを使用してメディア ファミリを処理できます。 1 つのメディア ファミリの処理が完了してから、別のメディア ファミリを処理する必要があります。 1 台のデバイスで復元する場合を除き、メディア ファミリは常に並列処理されます。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
 **新しいメディア セットを作成する**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md) ( **[新しいメディア セットにバックアップし、すべての既存のバックアップ セットを消去する]** オプション)  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md) (FORMAT オプション)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.FormatMedia%2A>  
  
 **新しいバックアップを既存のメディアに追加する**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md) ( **[既存のバックアップ セットに追加する]** オプション)  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md) (NOINIT オプション)  
  
 **既存のバックアップ セットを上書きする**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md) ( **[既存のすべてのバックアップ セットを上書きする]** オプション)  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md) (INIT オプション)  
  
 **有効期限を設定する**  
  
-   [バックアップの有効期限の設定 &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
 **メディア シーケンス番号およびファミリ シーケンス番号を表示する**  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md) (**family_sequence_number** 列)  
  
 **特定のバックアップ デバイス上のバックアップ セットを表示する**  
  
-   [バックアップ セットに含まれているデータ ファイルおよびログ ファイルの表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
 **バックアップ デバイス上のメディアのメディア ヘッダーを読み取る**  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
 
  
## <a name="see-also"></a>関連項目  
 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [Mirrored Backup Media Sets &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
