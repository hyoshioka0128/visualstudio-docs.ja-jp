---
title: マネージド コードの "基本デザイン ガイドライン規則" 規則セット
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 7eb384f5-f961-400b-b151-115d92addc6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: cf30e3294c1a96e64efd47ffd14f03328ebec62c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75573185"
---
# <a name="basic-design-guideline-rules-rule-set-for-managed-code"></a>マネージド コードの "基本デザイン ガイドライン規則" 規則セット

Microsoft の "基本デザインガイドライン規則" 規則セットを使用して、コードの理解と使用を容易にすることができます。 この規則セットは、プロジェクトにライブラリコードが含まれている場合や、保守が簡単なコードにベストプラクティスを適用する場合に使用してください。

基本的な設計ガイドライン規則には、" [マネージ推奨規則](managed-recommended-rules-rule-set-for-managed-code.md) " 規則セット内のすべての規則が含まれます。

次の表では、Microsoft 基本デザインガイドライン規則の規則セットに含まれるすべての規則について説明します。

|ルール|説明|
|----------|-----------------|
|[CA1000](../code-quality/ca1000.md)|ジェネリック型の静的メンバーを宣言しません|
|[CA1001](../code-quality/ca1001.md)|破棄可能なフィールドを所有する型は、破棄可能でなければなりません|
|[CA1002](../code-quality/ca1002.md)|ジェネリック リストを公開しません|
|[CA1003](../code-quality/ca1003.md)|汎用イベント ハンドラーのインスタンスを使用します|
|[CA1004](../code-quality/ca1004.md)|ジェネリック メソッドは型パラメーターを指定しなければなりません|
|[CA1005](../code-quality/ca1005.md)|ジェネリック型でパラメーターを使用しすぎないでください|
|[CA1006](../code-quality/ca1006.md)|ジェネリック型をメンバー シグネチャ内で入れ子にしません|
|[CA1007](../code-quality/ca1007.md)|適切な場所にジェネリックを使用します|
|[CA1008](../code-quality/ca1008.md)|Enums は 0 値を含んでいなければなりません|
|[CA1009](../code-quality/ca1009.md)|イベント ハンドラーを正しく宣言します|
|[CA1010](../code-quality/ca1010.md)|コレクションは、ジェネリック インターフェイスを実装しなければなりません|
|[CA1011](../code-quality/ca1011.md)|基本型をパラメーターとして渡すことを考慮します|
|[CA1012](../code-quality/ca1012.md)|抽象型にはコンストラクターを含めません|
|[CA1013](../code-quality/ca1013.md)|オーバーロードする加算および減算で、演算子 equals をオーバーロードします|
|[CA1014](../code-quality/ca1014.md)|アセンブリに CLSCompliantAttribute を設定します|
|[CA1016](../code-quality/ca1016.md)|アセンブリに AssemblyVersionAttribute を設定します|
|[CA1017](../code-quality/ca1017.md)|アセンブリに ComVisibleAttribute を設定します|
|[CA1018](../code-quality/ca1018.md)|属性を AttributeUsageAttribute に設定します|
|[CA1019](../code-quality/ca1019.md)|属性引数にアクセサーを定義します|
|[CA1023](../code-quality/ca1023.md)|インデクサーを多次元にすることはできません|
|[CA1024](../code-quality/ca1024.md)|適切な場所にプロパティを使用します|
|[CA1025](../code-quality/ca1025.md)|反復する引数を params 配列で置き換えます|
|[CA1026](../code-quality/ca1026.md)|既定パラメーターを使用することはできません|
|[CA1027](../code-quality/ca1027.md)|列挙型を FlagsAttribute に設定します|
|[CA1028](../code-quality/ca1028.md)|列挙ストレージは Int32 でなければなりません|
|[CA1030](../code-quality/ca1030.md)|適切な場所にイベントを使用します|
|[CA1031](../code-quality/ca1031.md)|一般的な例外の種類はキャッチしません|
|[CA1032](../code-quality/ca1032.md)|標準例外コンストラクターを実装します|
|[CA1033](../code-quality/ca1033.md)|インターフェイス メソッドは、子型によって呼び出し可能でなければなりません|
|[CA1034](../code-quality/ca1034.md)|入れ子にされた型を参照可能にすることはできません|
|[CA1035](../code-quality/ca1035.md)|ICollection の実装は、厳密に型指定されたメンバーを含んでいます|
|[CA1036](../code-quality/ca1036.md)|比較可能な型でメソッドをオーバーライドします|
|[CA1038](../code-quality/ca1038.md)|列挙子は厳密に型指定されていなければなりません|
|[CA1039](../code-quality/ca1039.md)|リストは厳密に型指定されています|
|[CA1041](../code-quality/ca1041.md)|ObsoleteAttribute メッセージを指定します|
|[CA1043](../code-quality/ca1043.md)|インデクサーには整数または文字列引数を使用します|
|[CA1044](../code-quality/ca1044.md)|プロパティを書き込み専用にすることはできません|
|[CA1046](../code-quality/ca1046.md)|参照型で、演算子 equals をオーバーロードしないでください|
|[CA1047: SEALED](../code-quality/ca1047.md)|シールド型の保護されたメンバーを宣言しません|
|[CA1048: SEALED](../code-quality/ca1048.md)|シールド型の仮想メンバーを宣言しません|
|[CA1049](../code-quality/ca1049.md)|ネイティブ リソースを所有する型は、破棄可能でなければなりません|
|[CA1050](../code-quality/ca1050.md)|名前空間で型を宣言します|
|[CA1051](../code-quality/ca1051.md)|参照可能なインスタンス フィールドを宣言しません|
|[CA1052](../code-quality/ca1052.md)|スタティック ホルダー型はシールドされていなければなりません|
|[CA1053](../code-quality/ca1053.md)|スタティック ホルダー型はコンストラクターを含むことはできません|
|[CA1054](../code-quality/ca1054.md)|URI パラメーターを文字列にすることはできません|
|[CA1055](../code-quality/ca1055.md)|URI 戻り値を文字列にすることはできません|
|[CA1056](../code-quality/ca1056.md)|URI プロパティを文字列にすることはできません|
|[CA1057](../code-quality/ca1057.md)|文字列 URI オーバーロードが、System.Uri オーバーロードを呼び出します|
|[CA1058](../code-quality/ca1058.md)|型は、一定の基本型を拡張することはできません|
|[CA1059](../code-quality/ca1059.md)|メンバーは特定の具象型を公開できません|
|[CA1060](../code-quality/ca1060.md)|P/Invoke を NativeMethods クラスに移動します|
|[CA1061](../code-quality/ca1061.md)|基底クラス メソッドを非表示にしません|
|[CA1063](../code-quality/ca1063.md)|IDisposable を正しく実装します|
|[CA1064](../code-quality/ca1064.md)|例外は public として設定する必要があります|
|[CA1065](../code-quality/ca1065.md)|予期しない場所に例外を発生させません|
|[CA1301](../code-quality/ca1301.md)|重複するアクセラレータを使用しません|
|[CA1400](../code-quality/ca1400.md)|P/Invoke エントリ ポイントは存在しなければなりません|
|[CA1401](../code-quality/ca1401.md)|P/Invoke は参照可能であることはできません|
|[CA1403](../code-quality/ca1403.md)|Auto 配置の型を COM 参照可能にすることはできません|
|[CA1404](../code-quality/ca1404.md)|P/Invoke の直後に GetLastError を呼び出します|
|[CA1405](../code-quality/ca1405.md)|COM 参照可能な型の基本型は COM 参照可能でなければなりません|
|[CA1410](../code-quality/ca1410.md)|COM 登録メソッドは一致しなければなりません|
|[CA1415](../code-quality/ca1415.md)|P/Invoke を正しく宣言します|
|[CA1500](../code-quality/ca1500.md)|変数名はフィールド名と同一にすることはできません|
|[CA1502](../code-quality/ca1502.md)|メソッドの実装を複雑にしすぎないでください|
|[CA1708](../code-quality/ca1708.md)|識別子は、大文字と小文字の区別以外にも相違していなければなりません|
|[CA1716](../code-quality/ca1716.md)|識別子はキーワードと同一にすることはできません|
|[CA1801](../code-quality/ca1801.md)|使用されていないパラメーターの確認|
|[CA1804](../code-quality/ca1804.md)|使用されていないローカルを削除します|
|[CA1809](../code-quality/ca1809.md)|ローカルを使用しすぎないでください|
|[CA1810](../code-quality/ca1810.md)|参照型の静的フィールドをインラインで初期化します|
|[CA1811](../code-quality/ca1811.md)|呼び出されていないプライベート コードを使用しません|
|[CA1812](../code-quality/ca1812.md)|インスタンス化されていない内部クラスを使用しません|
|[CA1813](../code-quality/ca1813.md)|アンシールド属性を使用しません|
|[CA1814](../code-quality/ca1814.md)|複数次元の配列ではなくジャグ配列を使用します|
|[CA1815](../code-quality/ca1815.md)|equals および operator equals を値型でオーバーライドします|
|[CA1819](../code-quality/ca1819.md)|プロパティは、配列を返すことはできません|
|[CA1820](../code-quality/ca1820.md)|文字列の長さを使用して空の文字列をテストします|
|[CA1821](../code-quality/ca1821.md)|空のファイナライザーを削除します|
|[CA1822](../code-quality/ca1822.md)|メンバーを static に設定します|
|[CA1823](../code-quality/ca1823.md)|使用されていないプライベート フィールドを使用しません|
|[CA1900](../code-quality/ca1900.md)|値型フィールドはポータブルでなければなりません|
|[CA1901](../code-quality/ca1901.md)|P/Invoke 宣言はポータブルでなければなりません|
|[CA2002](../code-quality/ca2002.md)|弱い ID を伴うオブジェクト上でロックしません|
|[CA2100](../code-quality/ca2100.md)|SQL クエリのセキュリティ脆弱性を確認|
|[CA2101](../code-quality/ca2101.md)|P/Invoke 文字列引数に対してマーシャリングを指定します|
|[CA2108](../code-quality/ca2108.md)|値型での宣言セキュリティを確認します|
|[CA2111](../code-quality/ca2111.md)|ポインターは参照可能にすることはできません|
|[CA2112](../code-quality/ca2112.md)|セキュリティで保護された型はフィールドを公開してはなりません|
|[CA2114](../code-quality/ca2114.md)|メソッド セキュリティは型のスーパーセットでなければなりません|
|[CA2116](../code-quality/ca2116.md)|APTCA メソッドは APTCA メソッドのみを呼び出すことができます|
|[CA2117](../code-quality/ca2117.md)|APTCA 型は APTCA 基本型のみを拡張することができます|
|[CA2122](../code-quality/ca2122.md)|リンク要求を含むメソッドを間接的に公開しません|
|[CA2123](../code-quality/ca2123.md)|オーバーライドのリンク要求はベースと同一でなければなりません|
|[CA2124](../code-quality/ca2124.md)|脆弱性のある finally 句を外側の try でラップします|
|[CA2126](../code-quality/ca2126.md)|型のリンク要求には継承要求が必要です|
|[CA2131](../code-quality/ca2131.md)|セキュリティ上重要な型は型等価性に参加してはならない|
|[CA2132](../code-quality/ca2132.md)|既定のコンストラクターは、基本型の既定コンストラクターと同程度以上、重要であることが必要|
|[CA2133](../code-quality/ca2133.md)|デリゲートは透過性の整合がとれたメソッドにバインドする必要がある|
|[CA2134](../code-quality/ca2134.md)|メソッドは、基本メソッドをオーバーライドしている場合、透過性の整合性を保つ必要がある|
|[CA2137](../code-quality/ca2137.md)|透過的メソッドは、検証可能な IL のみを含まなければならない|
|[CA2138](../code-quality/ca2138.md)|透過的メソッドは、SuppressUnmanagedCodeSecurity 属性を持つメソッドを呼び出してはならない|
|[CA2140](../code-quality/ca2140.md)|透過的コードは、セキュリティ上重要な項目を参照してはならない|
|[CA2141](../code-quality/ca2141.md)|透過的メソッドは Linkdemand を満たしてはならない|
|[CA2146](../code-quality/ca2146.md)|型は、基本型およびインターフェイスと同程度以上、重要でなければならない|
|[CA2147](../code-quality/ca2147.md)|透過コードは、セキュリティ アサートを使用してはならない|
|[CA2149](../code-quality/ca2149.md)|透過的メソッドは、ネイティブ コード内に呼び出しを行ってはならない|
|[CA2200](../code-quality/ca2200.md)|スタック詳細を保持するために再度スローします|
|[CA2201](../code-quality/ca2201.md)|予約された例外の種類を発生させません|
|[CA2202](../code-quality/ca2202.md)|オブジェクトを複数回破棄しない|
|[CA2205](../code-quality/ca2205.md)|Win32 API に相当するマネージド API を使用します|
|[CA2207](../code-quality/ca2207.md)|値型のスタティック フィールドのインラインを初期化します|
|[CA2208](../code-quality/ca2208.md)|引数の例外を正しくインスタンス化します|
|[CA2211](../code-quality/ca2211.md)|非定数フィールドは表示されません|
|[CA2212](../code-quality/ca2212.md)|サービス コンポーネントを WebMethod に設定しません|
|[CA2213](../code-quality/ca2213.md)|破棄可能なフィールドは破棄されなければなりません|
|[CA2214](../code-quality/ca2214.md)|コンストラクターのオーバーライド可能なメソッドを呼び出しません|
|[CA2216](../code-quality/ca2216.md)|破棄可能な型はファイナライザーを宣言しなければなりません|
|[CA2217](../code-quality/ca2217.md)|列挙型を FlagsAttribute に設定しません|
|[CA2219](../code-quality/ca2219.md)|exception 句に例外を発生させないでください|
|[CA2220](../code-quality/ca2220.md)|ファイナライザーは基底クラスのファイナライザーを呼び出さなければなりません|
|[CA2221](../code-quality/ca2221.md)|ファイナライザーは保護されなければなりません|
|[CA2222](../code-quality/ca2222.md)|継承されたメンバーの参照範囲を縮小しません|
|[CA2223](../code-quality/ca2223.md)|メンバーは、戻り値の型以外にも異なる点がなければなりません|
|[CA2224](../code-quality/ca2224.md)|オーバーロードする演算子 equals で Equals をオーバーライドします|
|[CA2225](../code-quality/ca2225.md)|演算子オーバーロードには名前付けされた代替が存在します|
|[CA2226](../code-quality/ca2226.md)|演算子は対称型オーバーロードを含まなければなりません|
|[CA2227](../code-quality/ca2227.md)|Collection プロパティは読み取り専用でなければなりません|
|[CA2229](../code-quality/ca2229.md)|シリアル化コンストラクターを実装します|
|[CA2230](../code-quality/ca2230.md)|可変引数に対して param を使用します|
|[CA2231](../code-quality/ca2231.md)|ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします|
|[CA2232](../code-quality/ca2232.md)|Windows フォームのエントリ ポイントを STAThread に設定します|
|[CA2234](../code-quality/ca2234.md)|文字列の代わりに System.Uri オブジェクトを渡します|
|[CA2235](../code-quality/ca2235.md)|すべてのシリアル化不可能なフィールドを設定します|
|[CA2236](../code-quality/ca2236.md)|ISerializable 型で基底クラス メソッドを呼び出します|
|[CA2237](../code-quality/ca2237.md)|ISerializable 型を SerializableAttribute に設定します|
|[CA2238](../code-quality/ca2238.md)|シリアル化メソッドを正しく実装します|
|[CA2239](../code-quality/ca2239.md)|省略可能なフィールドに、逆シリアル化メソッドを指定します|
|[CA2240](../code-quality/ca2240.md)|ISerializable を正しく実装します|
|[CA2241](../code-quality/ca2241.md)|書式設定メソッドに正しい引数を提供|
|[CA2242](../code-quality/ca2242.md)|NaN に対して正しくテストします|
