---
description: Visual C++ での ADO プログラミング
title: Visual C++ ADO プログラミング |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
author: rothja
ms.author: jroth
ms.openlocfilehash: a2e0284db09672d0e92bb952c9e122a65cb8350b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991833"
---
# <a name="visual-c-ado-programming"></a>Visual C++ での ADO プログラミング
ADO API リファレンスでは、Microsoft Visual Basic と同様の構文を使用した ADO アプリケーションプログラミングインターフェイス (API) の機能について説明します。 すべてのユーザーが対象となりますが、ADO プログラマーは、Visual Basic、Visual C++ ( **#import** ディレクティブを含む)、および Visual J++ (ADO/WFC クラスパッケージを含む) などのさまざまな言語を採用しています。  

> [!NOTE]
> Microsoft は、2004での Visual J++ のサポートを終了しました。

 この多様性に対応するために、 [ADO for Visual C++ 構文のインデックス](./using-ado-with-microsoft-visual-c.md) は、API リファレンスにおける機能、パラメーター、例外的な動作などの一般的な説明へのリンクと共に、言語固有の構文 Visual C++ を提供します。  
  
 ADO は、COM (コンポーネントオブジェクトモデル) インターフェイスを使用して実装されます。 ただし、プログラマは特定のプログラミング言語で COM を使用する方が簡単です。 たとえば、COM を使用する場合の詳細は、ほぼすべての場合に Visual Basic プログラマに対して暗黙的に処理されますが、Visual C++ プログラマはそれらの詳細に参加する必要があります。  
  
 次のセクションでは、ADO と **#import** ディレクティブを使用して、C および C++ プログラマの詳細を要約します。 COM に固有のデータ型 (**Variant**、 **BSTR**、および **SafeArray**) とエラー処理 (_com_error) に焦点を当てています。  
  
## <a name="using-the-import-compiler-directive"></a>#Import コンパイラディレクティブの使用  
 **#Import** Visual C++ コンパイラディレクティブを使用すると、ADO のメソッドとプロパティを簡単に操作できます。 ディレクティブは、ADO .dll (Msado15.dll) などのタイプライブラリを含むファイルの名前を受け取り、typedef 宣言、インターフェイスのスマートポインター、および列挙定数を含むヘッダーファイルを生成します。 各インターフェイスは、クラスにカプセル化またはラップされます。  
  
 クラス内の各操作 (つまり、メソッドまたはプロパティの呼び出し) に対して、操作を直接呼び出す宣言 (つまり、操作の "未加工" の形式) と、操作が正常に実行されなかった場合に COM エラーをスローする宣言があります。 操作がプロパティの場合、通常は、Visual Basic のような構文を持つ操作の代替構文を作成するコンパイラディレクティブがあります。  
  
 プロパティの値を取得する操作には、 **Get**_プロパティ_という形式の名前があります。 プロパティの値を設定する操作には、 **Put**_プロパティ_という形式の名前があります。 ADO オブジェクトへのポインターを使用してプロパティの値を設定する操作には、 **PutRef**_プロパティ_という形式の名前が付けられます。  
  
 次の形式の呼び出しを使用して、プロパティを取得または設定できます。  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>プロパティディレクティブの使用  
 **__Declspec (プロパティ...)** コンパイラディレクティブは、Microsoft 固有の C 言語拡張機能であり、別の構文を使用するためにプロパティとして使用される関数を宣言します。 その結果、Visual Basic に似た方法でプロパティの値を設定または取得できます。 たとえば、次のようにしてプロパティを設定したり取得したりできます。  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 コードを記述する必要がないことに注意してください。  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 コンパイラは、 **Get** _-_ どの代替構文が宣言されているか、およびプロパティが読み取りまたは書き込みのどちらであるかに基づいて、適切な Get、 **Put**、または**PutRef**_プロパティ_の呼び出しを生成します。  
  
 **__Declspec (プロパティ...)** コンパイラディレクティブで宣言できるのは、関数の**get**、 **put**、 **get** 、および**put**の代替構文だけです。 読み取り専用操作には **get** 宣言のみがあります。書き込み専用操作には、 **put** 宣言のみがあります。読み取りと書き込みの両方を行う操作には、 **get** 宣言と **put** 宣言の両方があります。  
  
 このディレクティブでは、2つの宣言のみを実行できます。ただし、各プロパティには、 **Get**_property_、 **Put**_property_、および **PutRef**_プロパティ_という3つのプロパティ関数があります。 その場合、2つの形式のプロパティには、別の構文があります。  
  
 たとえば、 **Command** オブジェクトの **ActiveConnection** プロパティは、 **Get**_ActiveConnection_ と **PutRef**_ActiveConnection_の代替構文を使用して宣言されています。 **PutRef**構文を使用することをお勧めします。実際には、開いている**接続**オブジェクト (つまり、**接続**オブジェクトのポインター) をこのプロパティに配置することをお勧めします。 一方、 **レコードセット** オブジェクトには、 **Get**、 **Put**、および **PutRef**_ActiveConnection_ の各操作がありますが、代替構文はありません。  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>コレクション、GetItem メソッド、Item プロパティ  

 ADO では、 **フィールド**、 **パラメーター**、 **プロパティ**、 **エラー**など、いくつかのコレクションが定義されています。 Visual C++ では、 **GetItem (_index_)** メソッドはコレクションのメンバーを返します。 *インデックス* は **バリアント**で、値はコレクション内のメンバーの数値インデックス、またはメンバーの名前を含む文字列のいずれかになります。  
  
 **__Declspec (プロパティ...)** コンパイラディレクティブは、各コレクションの基本的な**GetItem ()** メソッドの代替構文として**Item**プロパティを宣言します。 代替構文では、角かっこを使用し、配列参照のように表示されます。 一般に、2つの形式は次のようになります。  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 たとえば、 **pubs**データベースの**authors**テーブルから派生した、 **_Rs_** という名前の**レコードセット**オブジェクトのフィールドに値を代入します。 **Item ()** プロパティを使用して、**レコードセット**オブジェクト**フィールド**コレクションの3番目の**フィールド**にアクセスします (コレクションにはゼロからインデックスが付けられます。3番目のフィールドは**_au \_ fname_** という名前であると仮定します)。 次に、 **Field**オブジェクトの**value ()** メソッドを呼び出して、文字列値を割り当てます。  
  
 これは、次の4つの方法で Visual Basic 表現できます (最後の2つの形式は Visual Basic に固有であり、他の言語には同等のものはありません)。  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 上記の最初の2つの形式の Visual C++ に相当するものは次のとおりです。  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 または、( **Value** プロパティの代替構文も表示されます)  
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 コレクションの反復処理の例については、「ADO リファレンス」の「ADO コレクション」セクションを参照してください。  
  
## <a name="com-specific-data-types"></a>COM 固有のデータ型  
 一般に、ADO API リファレンスで見つかった Visual Basic データ型には、同等の Visual C++ があります。 これには、Visual Basic**バイト**の**符号なし char** 、**整数**の**short** 、 **long**の**long**型などの標準データ型が含まれます。 構文 Indexesto を調べて、特定のメソッドまたはプロパティのオペランドに必要なものを正確に確認します。  
  
 この規則の例外は、COM に固有のデータ型である **Variant**、 **BSTR**、および **SafeArray**です。  
  
### <a name="variant"></a>Variant  
 **バリアント**は、値メンバーとデータ型メンバーを含む構造化データ型です。 **バリアント**には、他のさまざまなデータ型を含めることができます。これには、別の VARIANT、BSTR、ブール値、IDispatch または IUnknown ポインター、通貨、日付などが含まれます。 COM には、あるデータ型から別の型への変換を簡単にするためのメソッドも用意されています。  
  
 **_Variant_t**クラスは、 **variant**データ型をカプセル化し、管理します。  
  
 ADO API リファレンスで、メソッドまたはプロパティのオペランドが値を受け取ることが示された場合は、通常、値が **_variant_t**で渡されることを意味します。  
  
 このルールは、ADO API リファレンスのトピックの **Parameters** セクションで、オペランドが **バリアント**であることが示されている場合に明示的に true になります。 1つの例外として、ドキュメントで明示的にオペランドが **Long** 、 **Byte**、enumeration などの標準データ型を受け取る場合があります。 もう1つの例外は、オペランドが **文字列**を受け取る場合です。  
  
### <a name="bstr"></a>BSTR  
 **BSTR** (**B**asic **STR**ing) は、文字列と文字列の長さを含む構造化データ型です。 COM には、 **BSTR**を割り当て、操作、および解放するためのメソッドが用意されています。  
  
 **_Bstr_t**クラスは、 **bstr**データ型をカプセル化し、管理します。  
  
 ADO API リファレンスで、メソッドまたはプロパティが **文字列** 値を受け取ることが示されている場合は、値が **_bstr_t**の形式であることを意味します。  
  
### <a name="casting-_variant_t-and-_bstr_t-classes"></a>_Variant_t と _bstr_t クラスのキャスト  
 多くの場合、 **_variant_t** を明示的にコーディングしたり、引数で操作に **_bstr_t** したりする必要はありません。 **_Variant_t**または **_bstr_t**クラスに引数のデータ型と一致するコンストラクターがある場合、コンパイラは適切な **_variant_t**または **_bstr_t**を生成します。  
  
 ただし、引数があいまいな場合、つまり、引数のデータ型が複数のコンストラクターと一致する場合は、正しいコンストラクターを呼び出すために、適切なデータ型で引数をキャストする必要があります。  
  
 たとえば、 **Recordset:: Open** メソッドの宣言は次のようになります。  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 引数は、 `ActiveConnection` **_variant_t**への参照を受け取ります。これは、接続文字列として、または開いている **接続** オブジェクトへのポインターとしてコーディングすることができます。  
  
 "" などの文字列、または "" などのポインターを渡すと、適切な **_variant_t** が暗黙的に構築され `DSN=pubs;uid=MyUserName;pwd=MyPassword;` `(IDispatch *) pConn` ます。  
  
> [!NOTE]
>  Windows 認証をサポートするデータソースプロバイダーに接続する場合は、接続文字列にユーザー ID とパスワードの情報ではなく、 **Trusted_Connection = yes** または **INTEGRATED Security = SSPI** を指定する必要があります。  
  
 または、"" などのポインターを含む **_variant_t** を明示的にコーディングすることもでき `_variant_t((IDispatch *) pConn, true)` ます。 キャストは、 `(IDispatch *)` IUnknown インターフェイスへのポインターを受け取る別のコンストラクターとのあいまいさを解決します。  
  
 これは非常に重要ですが、ADO は IDispatch インターフェイスであることはほとんどありません。 ADO オブジェクトへのポインターを **バリアント**として渡す必要がある場合は常に、そのポインターを IDispatch インターフェイスへのポインターとしてキャストする必要があります。  
  
 最後の例では、コンストラクターの2番目のブール型引数をオプションの既定値で明示的に指定して `true` います。 この引数を指定すると、 **Variant** コンストラクターは **AddRef**() メソッドを呼び出します。これにより、ado メソッドまたはプロパティの呼び出しが完了すると、 **_variant_t:: Release**() メソッドを自動的に呼び出す ado を補正します。  
  
### <a name="safearray"></a>SafeArray  
 **SafeArray**は、他のデータ型の配列を格納する構造化データ型です。 **SafeArray**は、各配列次元の境界に関する情報を格納し、それらの境界内の配列要素へのアクセスを制限するため、*安全*と呼ばれます。  
  
 ADO API リファレンスで、メソッドまたはプロパティが配列を取得または返すことを示している場合は、メソッドまたはプロパティがネイティブの C/c + + 配列ではなく、 **SafeArray**を取得または返すことを意味します。  
  
 たとえば、 **Connection** オブジェクト **OpenSchema** メソッドの2番目のパラメーターには **Variant** 値の配列が必要です。 これらの **バリアント** 値は、 **safearray**の要素として渡す必要があり、その **safearray** は別の **バリアント**の値として設定する必要があります。 これは、 **OpenSchema**の2番目の引数として渡されるその他の**バリアント**です。  
  
 さらに例として、 **Find**メソッドの最初の引数は、値が1次元の**SafeArray**である**バリアント**です。**AddNew**の1番目と2番目の引数 (省略可能) は、1次元の**SafeArray**です。また、 **GetRows**メソッドの戻り値は、値が2次元の**SafeArray**である**バリアント**です。  
  
## <a name="missing-and-default-parameters"></a>および既定のパラメーターがありません  
 Visual Basic では、メソッドのパラメーターが不足しています。 たとえば、 **Recordset** オブジェクトの **Open** メソッドには5つのパラメーターがありますが、中間パラメーターをスキップし、後続のパラメーターを省略できます。 既定の **BSTR** または **Variant** は、不足しているオペランドのデータ型によって置き換えられます。  
  
 C/c + + では、すべてのオペランドを指定する必要があります。 データ型が文字列である欠落しているパラメーターを指定する場合は、null 文字列を含む **_bstr_t** を指定します。 データ型が **バリアント**である欠落しているパラメーターを指定する場合は、値 DISP_E_PARAMNOTFOUND、VT_ERROR の型を持つ **_variant_t** を指定します。 または、 **#import**ディレクティブによって指定される、同等の **_variant_t**定数である**vtmissing**を指定します。  
  
 3つの方法は、一般的な **Vtmissing**の使用の例外です。 これらは、 **Connection**オブジェクトと**Command**オブジェクトの**Execute**メソッド、および**Recordset**オブジェクトの**NextRecordset**メソッドです。 シグネチャは次のとおりです。  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 Parameters、 *RecordsAffected* 、 *Parameters*は、 **Variant**へのポインターです。 *Parameters* は、実行されるコマンドを変更する1つのパラメーターまたはパラメーターの配列を含む **バリアント** のアドレスを指定する入力パラメーターです。 *RecordsAffected* は、メソッドによって影響を受ける行の数を返す **バリアント**のアドレスを指定する出力パラメーターです。  
  
 **Command**オブジェクトの**Execute**メソッドで、パラメーターを (推奨) または null *Parameters* `&vtMissing` ポインター ( **null**またはゼロ (0)) のいずれかに設定することによって、パラメーターが指定されていないことを示します。 *パラメーター*が null ポインターに設定されている場合、メソッドは、内部的には**vtmissing**に相当する値に置き換えられ、操作が完了します。  
  
 すべてのメソッドで、 *RecordsAffected* を null ポインターに設定することによって、影響を受けるレコードの数を返すことができないことを示します。 この場合、null ポインターは、メソッドが影響を受けるレコードの数を破棄する必要があることを示すために、不足しているパラメーターではありません。  
  
 したがって、次の3つの方法では、次のようなコードを記述することができます。  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>エラー処理  
 COM では、ほとんどの操作は、関数が正常に完了したかどうかを示す HRESULT リターンコードを返します。 **#Import**ディレクティブは、"生の" メソッドまたはプロパティごとにラッパーコードを生成し、返された HRESULT を確認します。 HRESULT が失敗を示している場合、ラッパーコードは、HRESULT リターンコードを引数として _com_issue_errorex () を呼び出すことによって COM エラーをスローします。 COM エラーオブジェクトは**try** - **catch**ブロックでキャッチできます。 (効率を上げるために、 **_com_error** オブジェクトへの参照をキャッチします。)  
  
 これらは ADO エラーであり、ADO 操作が失敗した場合に発生します。 基になるプロバイダーによって返されたエラーは、**接続**オブジェクト**エラー**のコレクションに**エラー**オブジェクトとして表示されます。  
  
 **#Import**ディレクティブは、ADO .dll で宣言されたメソッドとプロパティのエラー処理ルーチンだけを作成します。 ただし、独自のエラーチェックマクロまたはインライン関数を記述することで、この同じエラー処理機構を利用できます。 例については、次のセクションの「 [Visual C++ の拡張機能](./visual-c-extensions-for-ado.md)」または「コード」を参照してください。  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual Basic 規約の Visual C++  
 以下は、ADO ドキュメント内のいくつかの規則の概要であり、Visual Basic でコード化されています。また、Visual C++ でも同様です。  
  
### <a name="declaring-an-ado-object"></a>ADO オブジェクトの宣言  
 Visual Basic では、ADO オブジェクト変数 (この場合は **レコードセット** オブジェクト) は次のように宣言されます。  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 句 " `ADODB.Recordset` " は、レジストリで定義されている **レコードセット** オブジェクトの ProgID です。 **レコード**オブジェクトの新しいインスタンスは、次のように宣言されます。  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 - または -  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 Visual C++ では、 **#import** ディレクティブによって、すべての ADO オブジェクトのスマートポインター型宣言が生成されます。 たとえば、 **_Recordset** オブジェクトを指す変数は **_RecordsetPtr**型で、次のように宣言されています。  
  
```cpp
_RecordsetPtr  rs;  
```
  
 **_Recordset**オブジェクトの新しいインスタンスを指す変数は、次のように宣言されます。  
  
```cpp
_RecordsetPtr  rs("ADODB.Recordset");  
```
  
 \- または -  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```
  
 \- または -  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```
  
 **CreateInstance**メソッドが呼び出された後、変数は次のように使用できます。  
  
```cpp
rs->Open(...);  
```
  
 1つのケースで `.` は、変数がクラスのインスタンス () であるかのように "" 演算子が使用され、 `rs.CreateInstance` 別のケースでは、変数が `->` インターフェイスへのポインター () であるかのように "" 演算子が使用されていることに注意して `rs->Open` ください。  
  
 1つの変数は2つの方法で使用できます `->` 。これは、クラスのインスタンスがインターフェイスへのポインターのように動作するように、"" 演算子がオーバーロードされるためです。 インスタンス変数のプライベートクラスメンバーには、 **_Recordset** インターフェイスへのポインターが含まれています。" `->` " 演算子はそのポインターを返し、返されたポインターは **_Recordset** オブジェクトのメンバーにアクセスします。  
  
### <a name="coding-a-missing-parameter---string"></a>不足しているパラメーター文字列のコーディング  
 Visual Basic で欠落している **文字列** オペランドをコーディングする必要がある場合は、オペランドを省略するだけです。 Visual C++ でオペランドを指定する必要があります。 値として空の文字列を含む **_bstr_t** をコーディングします。  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter---variant"></a>不足しているパラメーターのコーディング-Variant  
 Visual Basic に存在しない **バリアント** オペランドをコーディングする必要がある場合は、オペランドを省略するだけです。 Visual C++ では、すべてのオペランドを指定する必要があります。 **_Variant_t**が特別な値、DISP_E_PARAMNOTFOUND、型、VT_ERROR に設定された、不足している**Variant**パラメーターをコーディングします。 または、[ **Vtmissing**] を指定します。これは、 **#import** ディレクティブによって提供される同等の定義済み定数です。  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 -またはを使用します。  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>バリアントの宣言  
 Visual Basic では、次のように**Dim**ステートメントを使用して**バリアント**が宣言されます。  
  
```vb
Dim VariableName As Variant  
```
  
 Visual C++ で、変数を型 **_variant_t**として宣言します。 いくつかの **_variant_t** 宣言を次に示します。  
  
> [!NOTE]
>  これらの宣言によって、自分のプログラムでコードを記述することがわかります。 詳細については、次の例と Visual C + + のドキュメントを参照してください。  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>バリアントの配列の使用  
 Visual Basic では、 **variant** の配列を **Dim** ステートメントでコーディングできます。また、次のコード例に示すように、 **配列** 関数を使用することもできます。  
  
```vb
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```
  
 次の Visual C++ 例は、 **_variant_t**で使用される**SafeArray**の使用方法を示しています。  
  
#### <a name="notes"></a>メモ  
 次の注意事項は、コード例のコメント部分に対応しています。  
  
1.  ここでも、既存のエラー処理メカニズムを利用するために、TESTHR () インライン関数が定義されています。  
  
2.  必要なのは1次元配列だけであるため、汎用**SAFEARRAYBOUND**宣言および**SafeArrayCreate**関数の代わりに**SafeArrayCreateVector**を使用できます。 **SafeArrayCreate**を使用すると、コードは次のようになります。  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  列挙定数 **adSchemaColumns**によって識別されるスキーマは、TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、および COLUMN_NAME の4つの制約列に関連付けられています。 したがって、4つの要素を持つ **バリアント** 値の配列が作成されます。 次に、3番目の列 TABLE_NAME に対応する制約値を指定します。  
  
     返される **レコードセット** は複数の列で構成され、そのサブセットは制約列です。 返される各行の制約列の値は、対応する制約値と同じである必要があります。  
  
4.  **Safearray**に慣れている方は、 **SafeArrayDestroy**() が終了前に呼び出されないことに驚かされるかもしれません。 実際、この場合、 **SafeArrayDestroy**() を呼び出すと、実行時例外が発生します。 その理由は、 `vtCriteria` **_variant_t**がスコープ外に出ると、のデストラクターは**VariantClear**() を呼び出すことになります。これにより、 **SafeArray**が解放されます。 **_Variant_t**を手動でクリアせずに**SafeArrayDestroy**を呼び出すと、デストラクターは無効な**SafeArray**ポインターをクリアしようとします。  
  
     **SafeArrayDestroy**が呼び出された場合、コードは次のようになります。  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     ただし、 **_variant_t** が **SafeArray**を管理できるようにする方がはるかに簡単です。  
  
```cpp
// Visual_CPP_ADO_Prog_1.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Note 1  
inline void TESTHR( HRESULT _hr ) {   
   if FAILED(_hr)   
      _com_issue_error(_hr);   
}  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      _ConnectionPtr pCn("ADODB.Connection");  
      _variant_t vtTableName("authors"), vtCriteria;  
      long ix[1];  
      SAFEARRAY *pSa = NULL;  
  
      pCn->Provider = "sqloledb";  
      pCn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
      // Note 2, Note 3  
      pSa = SafeArrayCreateVector(VT_VARIANT, 1, 4);  
      if (!pSa)   
         _com_issue_error(E_OUTOFMEMORY);  
  
      // Specify TABLE_NAME in the third array element (index of 2).   
      ix[0] = 2;        
      TESTHR(SafeArrayPutElement(pSa, ix, &vtTableName));  
  
      // There is no Variant constructor for a SafeArray, so manually set the   
      // type (SafeArray of Variant) and value (pointer to a SafeArray).  
  
      vtCriteria.vt = VT_ARRAY | VT_VARIANT;  
      vtCriteria.parray = pSa;  
  
      pRs = pCn->OpenSchema(adSchemaColumns, vtCriteria, vtMissing);  
  
      long limit = pRs->GetFields()->Count;  
      for ( long x = 0 ; x < limit ; x++ )  
         printf( "%d: %s\n", x + 1, ((char*) pRs->GetFields()->Item[x]->Name) );  
      // Note 4  
      pRs->Close();  
      pCn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Code meaning = %s\n", (char*) e.ErrorMessage());  
      printf("Source = %s\n", (char*) e.Source());  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   CoUninitialize();  
}  
```
  
### <a name="using-property-getputputref"></a>Property Get/Put/PutRef を使用する  
 Visual Basic では、プロパティの名前は、参照を取得、割り当て、または割り当てられているかどうかによって修飾されません。  
  
```vb
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```
  
 この Visual C++ の例では、 **Get** / **Put** / **PutRef**_プロパティ_を示します。  
  
#### <a name="notes"></a>メモ  
 次の注意事項は、コード例のコメント部分に対応しています。  
  
1.  この例では、省略された文字列引数の2つの形式を使用します。明示的な定数、 **Strmissing**、およびコンパイラが**Open**メソッドのスコープに存在する一時 **_bstr_t**を作成するために使用する文字列です。  
  
2.  `rs->PutRefActiveConnection(cn)` `(IDispatch *)` オペランドの型が既に存在するため、のオペランドをにキャストする必要はありません `(IDispatch *)` 。  
  
```cpp
// Visual_CPP_ado_prog_2.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _bstr_t strMissing(L"");  
      long oldPgSz = 0, newPgSz = 5;  
  
      // Note 1  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", strMissing, "", adConnectUnspecified);  
  
      oldPgSz = rs->GetPageSize();  
      // -or-  
      // oldPgSz = rs->PageSize;  
  
      rs->PutPageSize(newPgSz);  
      // -or-  
      // rs->PageSize = newPgSz;  
  
      // Note 2  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockReadOnly, adCmdTable);  
      printf("Original pagesize = %d, new pagesize = %d\n", oldPgSz, rs->GetPageSize());  
      rs->Close();  
      cn->Close();  
  
   }  
   catch (_com_error &e) {  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="using-getitemx-and-itemx"></a>GetItem (x) と Item [x] の使用  
 この Visual Basic の例は、 **Item**() の標準構文と代替構文を示しています。  
  
```vb
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```
  
 この Visual C++ の例は、 **Item**を示しています。  
  
> [!NOTE]
>  次の注意事項は、コード例のコメント付きセクションに対応しています。 **Item**を使用してコレクションにアクセスする場合、インデックス **2**が **long** にキャストされる必要があるため、適切なコンストラクターが呼び出されます。  
  
```cpp
// Visual_CPP_ado_prog_3.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
void main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _variant_t vtFirstName;  
  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", "", "", adConnectUnspecified);  
  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockOptimistic, adCmdTable);  
      rs->MoveFirst();  
  
      // Note 1. Get a field.  
      vtFirstName = rs->Fields->GetItem((long)2)->GetValue();  
      // -or-  
      vtFirstName = rs->Fields->Item[(long)2]->Value;  
  
      printf( "First name = '%s'\n", (char*)( (_bstr_t)vtFirstName) );  
  
      rs->Fields->GetItem((long)2)->Value = L"TEST";  
      rs->Update(vtMissing, vtMissing);  
  
      // Restore name  
      rs->Fields->GetItem((long)2)->PutValue(vtFirstName);  
      // -or-  
      rs->Fields->GetItem((long)2)->Value = vtFirstName;  
      rs->Update(vtMissing, vtMissing);  
      rs->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>ADO オブジェクトポインターを (IDispatch *) でキャストする  
 次の Visual C++ 例では、(IDispatch *) を使用して ADO オブジェクトポインターをキャストする方法を示します。  
  
#### <a name="notes"></a>メモ  
 次の注意事項は、コード例のコメント部分に対応しています。  
  
1.  明示的にコード化された**バリアント**で開いている**接続**オブジェクトを指定します。 正しいコンストラクターが呼び出されるように、(IDispatch) を使用してキャスト \* します。 また、2番目の **_variant_t** パラメーターを明示的に **true**に設定して、 **Recordset:: Open** 操作が終了したときにオブジェクト参照カウントが正しくなるようにします。  
  
2.  式は `(_bstr_t)` キャストではなく、**値**によって返される**variant**から **_bstr_t**の文字列を抽出する **_variant_t**演算子です。  
  
 式は `(char*)` キャストではなく、 **_bstr_t**オブジェクト内のカプセル化された文字列へのポインターを抽出する **_bstr_t**演算子です。  
  
 このコードのセクションでは、 **_variant_t** と **_bstr_t** 演算子の便利な動作の一部を示します。  
  
```cpp
// Visual_CPP_ado_prog_4.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr pConn("ADODB.Connection");  
      _RecordsetPtr pRst("ADODB.Recordset");  
  
      pConn->Provider = "sqloledb";  
      pConn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
  
      // Note 1.  
      pRst->Open("authors", _variant_t((IDispatch *) pConn, true), adOpenStatic, adLockReadOnly, adCmdTable);  
      pRst->MoveLast();  
  
      // Note 2.  
      printf("Last name is '%s %s'\n",   
         (char*) ((_bstr_t) pRst->GetFields()->GetItem("au_fname")->GetValue()),  
         (char*) ((_bstr_t) pRst->Fields->Item["au_lname"]->Value));  
  
      pRst->Close();  
      pConn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }     
   ::CoUninitialize();  
}  
```