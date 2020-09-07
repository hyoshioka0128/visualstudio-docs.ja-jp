---
title: FxCop 規則のポートの状態
ms.date: 05/21/2019
ms.topic: reference
helpviewer_keywords:
- fxcop rules
- fxcop analyzers, ported rules
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 28429b43295956d29bb9fc04f80ccf7ba1b1e720
ms.sourcegitcommit: 5caad925ca0b5d136416144a279e984836d8f28c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "89508367"
---
# <a name="fxcop-rule-port-status"></a>Fxcop 規則のポートの状態

以前に Visual Studio で静的コード分析を使用したことがある場合は、現在の実装で [FxCop アナライザー](install-fxcop-analyzers.md)として使用できる規則を考えているかもしれません。 このページには、移植されたルールの一覧が表示されます。 移植されていないルール、およびそれらに移植する計画があるかどうかについては、「 [unported 規則](fxcop-unported-rules.md) 」を参照してください。

## <a name="ported-rules"></a>移植された規則

Roslyn-アナライザーリポジトリの自動生成された [ドキュメントページ](https://github.com/dotnet/roslyn-analyzers/blob/master/src/Microsoft.CodeAnalysis.FxCopAnalyzers/Microsoft.CodeAnalysis.FxCopAnalyzers.md) には、FxCop アナライザーに移植されたルールの最新の一覧が含まれています。 このページには、規則が既定で有効になっているかどうかや、関連付けられている *コード修正プログラム*があるかどうかなどの追加情報も含まれています。 ([コード修正](../ide/quick-actions.md) は、Visual Studio の電球アイコンメニューで使用できるワンクリック修正です)。

このページの日付のとき、 [fxcop アナライザー](install-fxcop-analyzers.md) に移植された fxcop 規則の一覧には次のものが含まれます。

ルールの ID | タイトル
--------|---------
[CA1000](ca1000.md) | ジェネリック型の静的メンバーを宣言しません
[CA1001](ca1001.md) | 破棄可能なフィールドを所有する型は、破棄可能でなければなりません
[CA1002](ca1002.md) | ジェネリック リストを公開しません
[CA1003](ca1003.md) | 汎用イベント ハンドラーのインスタンスを使用します
[CA1005](ca1005.md) | ジェネリック型でパラメーターを使用しすぎないでください
[CA1008](ca1008.md) | Enums は 0 値を含んでいなければなりません
[CA1010](ca1010.md) | コレクションは、ジェネリック インターフェイスを実装しなければなりません
[CA1012](ca1012.md) | 抽象型にはコンストラクターを含めません
[CA1014](ca1014.md) | アセンブリを CLSCompliant にマークします
[CA1016](ca1016.md) | アセンブリのバージョンをアセンブリにマークする
[CA1017](ca1017.md) | アセンブリに ComVisible を設定します
[CA1018](ca1018.md) | 属性を AttributeUsageAttribute に設定します
[CA1019](ca1019.md) | 属性引数にアクセサーを定義します
[CA1021](ca1021.md) | out パラメーターを使用しません
[CA1024](ca1024.md) | 適切な場所にプロパティを使用します
[CA1027](ca1027.md) | 列挙型を FlagsAttribute に設定します
[CA1028](ca1028.md) | 列挙ストレージは Int32 でなければなりません
[CA1030](ca1030.md) | 適切な場所にイベントを使用します
[CA1031](ca1031.md) | 一般的な例外の種類はキャッチしません
[CA1032](ca1032.md) | 標準例外コンストラクターを実装します
[CA1033](ca1033.md) | インターフェイス メソッドは、子型によって呼び出し可能でなければなりません
[CA1034](ca1034.md) | 入れ子にされた型を参照可能にすることはできません
[CA1036](ca1036.md) | 比較可能な型でメソッドをオーバーライドします
[CA1040](ca1040.md) | 空のインターフェイスは使用しません
[CA1041](ca1041.md) | ObsoleteAttribute メッセージを指定します
[CA1043](ca1043.md) | インデクサーに整数または文字列引数を使用する
[CA1044](ca1044.md) | プロパティを書き込み専用にすることはできません
[CA1045](ca1045.md) | 型を参照によって渡しません
[CA1046](ca1046.md) | 参照型で、演算子 equals をオーバーロードしないでください
[CA1047: SEALED](ca1047.md) | シールド型の保護されたメンバーを宣言しません
[CA1050](ca1050.md) | 名前空間で型を宣言します
[CA1051](ca1051.md) | 参照可能なインスタンス フィールドを宣言しません
[CA1052](ca1052.md) | 静的ホルダー型は static または NotInheritable である必要があります
[CA1053](ca1053.md) | 静的ホルダー型にコンストラクターを含めることはできません (CA1053 は FxCop アナライザーの [CA1052](ca1052.md) に含まれています)
[CA1054](ca1054.md) | Uri パラメーターを文字列にすることはできません
[CA1055](ca1055.md) | Uri 戻り値を文字列にすることはできません
[CA1056](ca1056.md) | Uri プロパティを文字列にすることはできません
[CA1058](ca1058.md) | 型は、一定の基本型を拡張することはできません
[CA1060](ca1060.md) | Pinvokes をネイティブメソッドクラスに移動する
[CA1061](ca1061.md) | 基底クラス メソッドを非表示にしません
[CA1062](ca1062.md) | パブリック メソッドの引数の検証
[CA1063](ca1063.md) | IDisposable を正しく実装する
[CA1064](ca1064.md) | 例外は public として設定する必要があります
[CA1065](ca1065.md) | 予期しない場所に例外を発生させません
[CA1066](ca1066.md) | Type {0} は Equals をオーバーライドするため、IEquatable を実装しなければなりませ \<T> ん
[CA1067](ca1067.md) | IEquatable を実装するときに、Object.equals (object) をオーバーライドします。\<T>
[CA1303](ca1303.md) | ローカライズされるパラメーターとしてリテラルを渡さない
[CA1304](ca1304.md) | CultureInfo を指定します
[CA1305](ca1305.md) | IFormatProvider を指定します
[CA1307](ca1307.md) | 意味を明確にするための StringComparison の指定
[CA1308](ca1308.md) | 文字列を大文字に標準化します
[CA1309](ca1309.md) | 序数の文字列比較を使用する
[CA1401](ca1401.md) | P/Invoke は参照可能であることはできません
[CA1501](ca1501.md) | 継承を使用しすぎないでください
[CA1502](ca1502.md) | メソッドの実装を複雑にしすぎないでください
[CA1505](ca1505.md) | メンテナンスできないコードを使用しないでください
[CA1506](ca1506.md) | クラス結合度を大きくしすぎないでください
[CA1700](ca1700.md) | 列挙型値に 'Reserved' という名前を指定しません
[CA1707](ca1707.md) | 識別子はアンダースコアを含むことはできません
[CA1708](ca1708.md) | 識別子は、大文字と小文字の区別以外にも相違していなければなりません
[CA1710](ca1710.md) | 識別子は、正しいサフィックスを含んでいなければなりません
[CA1711](ca1711.md) | 識別子は、不適切なサフィックスを含むことはできません
[CA1712](ca1712.md) | 列挙型値を型名のプレフィックスにしません
[CA1713](ca1713.md) | イベントは、before または after プレフィックスを含むことはできません
[CA1714](ca1714.md) | フラグ列挙型は、複数形の名前を含んでいなければなりません
[CA1715](ca1715.md) | 識別子は正しいプレフィックスを含んでいなければなりません
[CA1716](ca1716.md) | 識別子はキーワードと同一にすることはできません
[CA1717](ca1717.md) | FlagsAttribute 列挙型のみが複数形の名前を含んでいなければなりません
[CA1720](ca1720.md) | 識別子に型名が含まれています
[CA1721](ca1721.md) | プロパティ名は get メソッドと同一にすることはできません
[CA1724](ca1724.md) | 型名を名前空間と一致させることはできません
[CA1725](ca1725.md) | パラメーター名は基本宣言と同一でなければなりません
[CA1801](ca1801.md) | 使用されていないパラメーターの確認
[CA1802](ca1802.md) | 適切な場所にリテラルを使用する
[CA1805](ca1805.md) | 不必要に初期化しない
[CA1806](ca1806.md) | メソッドの結果を無視しない
[CA1810](ca1810.md) | 参照型の静的フィールドをインラインで初期化します
[CA1812](ca1812.md) | インスタンス化されていない内部クラスを使用しません
[CA1813](ca1813.md) | アンシールド属性を使用しません
[CA1814](ca1814.md) | 複数次元の配列ではなくジャグ配列を使用します
[CA1815](ca1815.md) | equals および operator equals を値型でオーバーライドします
[CA1816](ca1816.md) | Dispose メソッドは Gc.suppressfinalize を呼び出す必要があります
[CA1819](ca1819.md) | プロパティは、配列を返すことはできません
[CA1820](ca1820.md) | 文字列の長さを使用して空の文字列をテストします
[CA1821](ca1821.md) | 空のファイナライザーの削除
[CA1822](ca1822.md) | メンバーを static に設定します
[CA1823](ca1823.md) | 使用されていないプライベート フィールドを使用しません
[CA1824](ca1824.md) | アセンブリを NeutralResourcesLanguageAttribute に設定します
[CA1825](ca1825.md) | 長さ0の配列を割り当てないようにします。
[CA2000](ca2000.md) | スコープを失う前にオブジェクトを破棄
[CA2002](ca2002.md) | 弱い ID を伴うオブジェクト上でロックしません
[CA2100](ca2100.md) | SQL クエリのセキュリティ脆弱性を確認
[CA2101](ca2101.md) | P/Invoke 文字列引数に対してマーシャリングを指定します
[CA2109](ca2109.md) | 表示するイベント ハンドラーを確認します
[CA2119](ca2119.md) | プライベート インターフェイスを満たすメソッドをシールします
[CA2153](ca2153.md) | 破損状態の例外をキャッチしない
[CA2200](ca2200.md) | スタックの詳細を保持するために再スローします。
[CA2201](ca2201.md) | 予約された例外の種類を発生させません
[CA2207](ca2207.md) | 値型のスタティック フィールドのインラインを初期化します
[CA2208](ca2208.md) | 引数の例外を正しくインスタンス化します
[CA2211](ca2211.md) | 非定数フィールドは表示されません
[CA2213](ca2213.md) | 破棄可能なフィールドは破棄されなければなりません
[CA2214](ca2214.md) | コンストラクターのオーバーライド可能なメソッドを呼び出しません
[CA2215](ca2215.md) | Dispose メソッドが基底クラスの Dispose を呼び出す必要があります
[CA2216](ca2216.md) | 破棄可能な型はファイナライザーを宣言しなければなりません
[CA2217](ca2217.md) | 列挙型を FlagsAttribute に設定しません
[CA2219](ca2219.md) | Finally 句で例外を発生させない
[CA2225](ca2225.md) | 演算子オーバーロードには名前付けされた代替が存在します
[CA2226](ca2226.md) | 演算子は対称型オーバーロードを含まなければなりません
[CA2227](ca2227.md) | Collection プロパティは読み取り専用でなければなりません
[CA2229](ca2229.md) | シリアル化コンストラクターを実装します
[CA2231](ca2231.md) | 値型 Equals のオーバーライドで、演算子 equals をオーバーロードします
[CA2234](ca2234.md) | 文字列ではなくシステム uri オブジェクトを渡す
[CA2235](ca2235.md) | すべてのシリアル化不可能なフィールドを設定します
[CA2237](ca2237.md) | ISerializable 型を Serializable に設定します
[CA2241](ca2241.md) | 書式設定メソッドに正しい引数を提供
[CA2242](ca2242.md) | NaN に対して正しくテストします
[CA2243](ca2243.md) | 属性文字列リテラルは、正しく解析する必要があります
[CA2300](ca2300.md) | 安全ではないデシリアライザー BinaryFormatter を使用しないでください
[CA2301](ca2301.md) | 最初に BinaryFormatter.Binder を設定しないで BinaryFormatter.Deserialize を呼び出さないでください
[CA2302](ca2302.md) | BinaryFormatter.Deserialize を呼び出す前に BinaryFormatter.Binder が設定されていることを確認します
[CA2305](ca2305.md) | 安全ではないデシリアライザー LosFormatter を使用しないでください
[CA2310](ca2310.md) | 安全ではないデシリアライザー NetDataContractSerializer を使用しないでください
[CA2311](ca2311.md) | 最初に NetDataContractSerializer.Binder を設定しないで逆シリアル化しないでください
[CA2312](ca2312.md) | NetDataContractSerializer.Binder を設定してから逆シリアル化してください
[CA2315](ca2315.md) | 安全ではないデシリアライザー ObjectStateFormatter を使用しないでください
[CA2321](ca2321.md) | SimpleTypeResolver を使って JavaScriptSerializer で逆シリアル化しないでください
[CA2322](ca2322.md) | 逆シリアル化する前に JavaScriptSerializer が SimpleTypeResolver によって初期化されていないことを確認してください
[CA3001](ca3001.md) | SQL インジェクションの脆弱性のコード レビュー
[CA3002](ca3002.md) | XSS の脆弱性のコード レビュー
[CA3003](ca3003.md) | ファイル パス インジェクションの脆弱性のコード レビュー
[CA3004](ca3004.md) | 情報漏えいの脆弱性のコード レビュー
[CA3005](ca3005.md) | LDAP インジェクションの脆弱性のコード レビュー
[CA3006](ca3006.md) | プロセス コマンド インジェクションの脆弱性のコード レビュー
[CA3007](ca3007.md) | オープン リダイレクトの脆弱性のコード レビュー
[CA3008](ca3008.md) | XPath インジェクションの脆弱性のコード レビュー
[CA3009](ca3009.md) | XML インジェクションの脆弱性のコード レビュー
[CA3010](ca3010.md) | XAML インジェクションの脆弱性のコード レビュー
[CA3011](ca3011.md) | DLL インジェクションの脆弱性のコード レビュー
[CA3012](ca3012.md) | RegEx インジェクションの脆弱性のコード レビュー
[CA3061](ca3061.md) | URL でスキーマを追加しない
[CA3075](ca3075.md) | XML での DTD 処理が安全ではありません
[CA3076](ca3076.md) | 安全ではない XSLT スクリプトの処理。
[CA3077](ca3077.md) | API 設計、XmlDocument、XmlTextReader で安全ではない処理
[CA3147](ca3147.md) | アンチ偽造トークンを検証する動詞ハンドラーをマークします
[CA5350](ca5350.md) | 脆弱な暗号アルゴリズムを使用しないでください
[CA5351](ca5351.md) | 破損した暗号アルゴリズムを使用しない
[CA5358](ca5358.md) | 安全ではない暗号モードを使用しないでください
CA5359 | 証明書の検証を無効にしない
CA5360 | 逆シリアル化で危険なメソッドを呼び出さないでください
[CA5361](ca5361.md) | 強力な暗号の SChannel 使用を無効にしない
CA5362 | Serializable クラスの Self を参照しない
[CA5363](ca5363.md) | 要求の検証を無効にしない
[CA5364](ca5364.md) | 非推奨のセキュリティプロトコルを使用しない
CA5365 | HTTP ヘッダーチェックを無効にしない
CA5366 | DataSet に XmlReader を使用する Xml の読み取り
CA5367 | ポインターフィールドを持つ型をシリアル化しない
CA5368 | ページから派生したクラスの ViewStateUserKey を設定する
[CA5369](ca5369.md) | 逆シリアル化に XmlReader を使用する
[CA5370](ca5370.md) | 読み取りの検証に XmlReader を使用する
[CA5371](ca5371.md) | スキーマ読み取りに XmlReader を使用する
[CA5372](ca5372.md) | Xpath ドキュメントに XmlReader を使用する
[CA5373](ca5373.md) | 廃止されたキー派生関数を使用しません
CA5374 | XslTransform を使用しない
CA5375 | アカウントを使用しない Shared Access Signature
CA5376 | SharedAccessProtocol HttpsOnly を使用する
CA5377 | コンテナーレベルのアクセスポリシーを使用する
[CA5378](ca5378.md) | ServicePointManagerSecurityProtocols を無効にしません
CA5379 | 弱いキー派生関数アルゴリズムを使用しない
CA9999 | アナライザーのバージョンが一致しません

## <a name="see-also"></a>関連項目

- [FxCopAnalyzers の規則](https://github.com/dotnet/roslyn-analyzers/blob/master/src/Microsoft.CodeAnalysis.FxCopAnalyzers/Microsoft.CodeAnalysis.FxCopAnalyzers.md)
