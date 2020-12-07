---
description: Recordset オブジェクト (ADO)
title: Recordset オブジェクト (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
author: rothja
ms.author: jroth
ms.openlocfilehash: ff23c57ae3ecf25e7328d304f9716ad24f2aba7e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989742"
---
# <a name="recordset-object-ado"></a>Recordset オブジェクト (ADO)
ベーステーブルまたは実行されたコマンドの結果のレコードのセット全体を表します。 **レコードセット**オブジェクトは、常に、セット内の1つのレコードのみを現在のレコードとして参照します。  
  
## <a name="remarks"></a>解説  
 **レコードセット**オブジェクトを使用して、プロバイダーのデータを操作します。 ADO を使用する場合は、 **レコードセット** オブジェクトを使用してほぼ完全にデータを操作します。 すべての **レコードセット** オブジェクトは、レコード (行) とフィールド (列) で構成されます。 プロバイダーでサポートされている機能によっては、一部の **レコードセット** メソッドまたはプロパティを使用できない場合があります。  
  
 ADODB.RECORDSET.レコードセットは、 **レコードセット** オブジェクトを作成するために使用する必要がある ProgID です。 古い ADOR を参照する既存のアプリケーション。レコードセット ProgID は再コンパイルせずに引き続き動作しますが、新しい開発では ADODB を参照する必要があります。レコードセット.  
  
 ADO では、次の4種類のカーソルが定義されています。  
  
-   **動的カーソル** 他のユーザーが追加、変更、および削除を表示できるようにします。ブックマークに依存しない **レコードセット** 内のすべての種類の移動を許可します。とは、プロバイダーがブックマークをサポートしている場合にブックマークを許可します。  
  
-   **Keyset カーソル** は動的カーソルと同様に動作しますが、他のユーザーが追加したレコードを表示できず、他のユーザーが削除したレコードにアクセスできない点が異なります。 他のユーザーによるデータの変更は引き続き表示されます。 ブックマークを常にサポートしているため、 **レコードセット**を通じてすべての種類の移動を許可します。  
  
-   **静的カーソル** データの検索やレポートの生成に使用するレコードセットの静的なコピーを提供します。では常にブックマークが許可されるため、 **レコードセット**内のすべての種類の移動が可能になります。 他のユーザーによる追加、変更、または削除は表示されません。 これは、クライアント側の **レコードセット** オブジェクトを開いたときに許可されるカーソルの唯一の種類です。  
  
-   **順方向専用カーソル****レコードセット**を前方にスクロールするだけです。 他のユーザーによる追加、変更、または削除は表示されません。 これにより、 **レコードセット**を通過する必要がある場合のパフォーマンスが向上します。  
  
 **レコードセット**を開いてカーソルの種類を選択するか、 [Open](./open-method-ado-recordset.md)メソッドを使用して*CursorType*引数を渡す前に、 [CursorType](./cursortype-property-ado.md)プロパティを設定します。 一部のプロバイダーでは、すべてのカーソルの種類がサポートされていません。 プロバイダーのドキュメントを確認してください。 カーソルの種類を指定しない場合、既定では、順方向専用カーソルが開きます。  
  
 [カーソル位置](./cursorlocation-property-ado.md)プロパティを**adUseClient**に設定して**レコードセット**を開く場合、返される**レコードセット**オブジェクトでは[Field](./field-object.md)オブジェクトの**UnderlyingValue**プロパティは使用できません。 一部のプロバイダー (Microsoft SQL Server と共に Microsoft ODBC Provider for OLE DB など) を使用する場合は、 **Open**メソッドを使用して接続文字列を渡すことで、以前に定義した[接続](./connection-object-ado.md)オブジェクトとは別に**レコードセット**オブジェクトを作成できます。 ADO では引き続き [接続](./connection-object-ado.md) オブジェクトが作成されますが、オブジェクトはオブジェクト変数に割り当てられません。 ただし、同じ接続で複数の **レコードセット** オブジェクトを開いている場合は、 **接続** オブジェクトを明示的に作成して開く必要があります。これにより、 **接続** オブジェクトがオブジェクト変数に割り当てられます。 **レコードセット**オブジェクトを開くときにこのオブジェクト変数を使用しない場合、同じ接続文字列を渡す場合でも、ADO は新しい**レコードセット**ごとに新しい**接続**オブジェクトを作成します。  
  
 必要に応じて、複数の **レコードセット** オブジェクトを作成できます。  
  
 **レコードセット**を開くと、現在のレコードが最初のレコード (存在する場合) に配置され、 [BOF](./bof-eof-properties-ado.md)プロパティと[EOF](./bof-eof-properties-ado.md)プロパティが**False**に設定されます。 レコードが存在しない場合、 **BOF** プロパティと **EOF** プロパティの設定は **True**になります。  
  
 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 **MoveLast**、 **MoveNext**、および**MovePrevious**の各メソッドを使用できます。[Move](./move-method-ado.md)メソッド。また、 [AbsolutePosition](./absoluteposition-property-ado.md)、 [AbsolutePage](./absolutepage-property-ado.md)、および[Filter](./filter-property.md)の各プロパティは、プロバイダーが関連する機能をサポートしていることを前提として、現在のレコードの位置を変更します。 前方参照専用の **レコードセット** オブジェクトでは、 [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) メソッドのみがサポートされます。 **Move**メソッドを使用して各レコードにアクセスする (または**レコードセット**を列挙する) 場合、 **BOF**プロパティと**EOF**プロパティを使用して、**レコードセット**の先頭または末尾を超えて移動したかどうかを判断できます。  
  
 **レコードセット**オブジェクトの機能を使用する前に、オブジェクトの**Supports**メソッドを呼び出して、機能がサポートされているか使用可能であることを確認する必要があります。 **サポート**メソッドが false を返す場合は、この機能を使用しないでください。 たとえば、が True を返す場合にのみ、 **MovePrevious**メソッドを使用でき `Recordset.Supports(adMovePrevious)` ます。 **True** それ以外の場合は、エラーが発生します。これは、 **レコードセット** オブジェクトが閉じられていて、インスタンスで使用できない機能が表示されている可能性があるためです。 関心のある機能がサポートされていない場合 **は、も false を返し** ます。 この場合、 **レコードセット** オブジェクトの対応するプロパティまたはメソッドを呼び出さないようにしてください。  
  
 **レコードセット** オブジェクトは、即時およびバッチ処理の2種類の更新をサポートできます。 即時更新では、 [Update](./update-method.md) メソッドを呼び出した後、データへのすべての変更が、基になるデータソースに直ちに書き込まれます。 また、 [AddNew](./addnew-method-ado.md) メソッドおよび **Update** メソッドを使用して値の配列をパラメーターとして渡し、レコード内の複数のフィールドを同時に更新することもできます。  
  
 プロバイダーでバッチ更新がサポートされている場合は、プロバイダーが複数のレコードに対して変更をキャッシュし、それを [UpdateBatch](./updatebatch-method.md) メソッドを使用してデータベースへの1回の呼び出しで送信することができます。 これは、 **AddNew**、 **Update**、および [Delete](./delete-method-ado-recordset.md) の各メソッドを使用して行われた変更に適用されます。 **UpdateBatch**メソッドを呼び出した後、 [Status](./status-property-ado-recordset.md)プロパティを使用して、データの競合を確認して解決することができます。  
  
> [!NOTE]
>  [Command](./command-object-ado.md)オブジェクトを使用せずにクエリを実行するには、クエリ文字列を**レコードセット**オブジェクトの**Open**メソッドに渡します。 ただし、コマンドのテキストを永続化して再実行する場合、またはクエリパラメーターを使用する場合は、 **command** オブジェクトが必要です。  
  
 [Mode](./mode-property-ado.md)プロパティは、アクセス許可を制御します。  
  
 **Fields**コレクションは、**レコードセット**オブジェクトの既定のメンバーです。 その結果、次の2つのコードステートメントは等価です。  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 **レコードセット**オブジェクトが複数のプロセスにわたって渡されると、**行**セットの値のみがマーシャリングされ、**レコードセット**オブジェクトのプロパティは無視されます。 マーシャリング解除中に、新しく作成された**レコードセット**オブジェクトに**行セット**がアンパックされます。これにより、プロパティも既定値に設定されます。  
  
 **レコードセット**オブジェクトは、スクリプトに対して安全です。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Recordset オブジェクトのプロパティ、メソッド、およびイベント](./recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Connection オブジェクト (ADO)](./connection-object-ado.md)   
 [Fields コレクション (ADO)](./fields-collection-ado.md)   
 [Properties コレクション (ADO)](./properties-collection-ado.md)   
 [付録 A: プロバイダー](../../guide/appendixes/appendix-a-providers.md)