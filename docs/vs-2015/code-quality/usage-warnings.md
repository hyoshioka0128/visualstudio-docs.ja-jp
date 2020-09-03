---
title: 使用状況に関する警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.usagerules
helpviewer_keywords:
- warnings, usage
- managed code analysis warnings, usage warnings
- usage warnings
ms.assetid: fe7dc2a3-289d-4bf7-a1e4-0947a81287c4
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bd1e993723d3ef1779eb3a23e19fedd081b6a6d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72603516"
---
# <a name="usage-warnings"></a>使用法に関する警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用状況の警告は、.NET Framework の適切な使用をサポートします。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA1801:使用されていないパラメーターの確認](../code-quality/ca1801-review-unused-parameters.md)|メソッドのシグネチャに、メソッドの本体で使用されていないパラメーターがあります。|
|[CA1806:メソッドの結果を無視しない](../code-quality/ca1806-do-not-ignore-method-results.md)|新しく作成されたオブジェクトが現在まで使用されていないか、新しい文字列を作成して返すメソッドが呼び出されて作成された新しい文字列が現在まで使用されていません。あるいは、COM または P/Invoke メソッドから返された HRESULT またはエラー コードが現在まで使用されていません。|
|[CA1816:GC.SuppressFinalize を正しく呼び出します](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)|Dispose を実装するメソッドが GC.SuppressFinalize を呼び出していないか、Dispose を実装しないメソッドが GC.SuppressFinalize を呼び出しています。または、あるメソッドが GC.SuppressFinalize を呼び出し、this (Visual Basic では Me) 以外のオブジェクトを渡しています。|
|[CA2200:スタック詳細を保持するために再度スローします](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)|例外が再スローされ、例外は throw ステートメントで明示的に指定されます。 Throw ステートメントで例外を指定することによって例外が再スローされた場合、例外をスローした元のメソッドと現在のメソッド間のメソッド呼び出しの一覧は失われます。|
|[CA2201:予約された例外の種類を発生させません](../code-quality/ca2201-do-not-raise-reserved-exception-types.md)|これにより、元のエラーの検出とデバッグが困難になります。|
|[CA2202:オブジェクトを複数回破棄しない](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md)|メソッドの実装に、同じオブジェクトに対して System.IDisposable.Dispose または Dispose と同等の操作 (たとえば、一部の型に対する Close() メソッドなど) を複数回呼び出すコード パスが含まれています。|
|[CA2204:リテラルに正しいスペルを要求](../code-quality/ca2204-literals-should-be-spelled-correctly.md)|メソッド本体に含まれるリテラル文字列内に Microsoft スペル チェック ライブラリで認識されない語が 1 つ以上あります。|
|[CA2205:Win32 API に相当するマネージド API を使用します](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)|プラットフォーム呼び出しメソッドが定義されていますが、それと同等の機能を持つメソッドが .NET Framework クラスライブラリに存在します。|
|[CA2207:値型のスタティック フィールドのインラインを初期化します](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)|値型で明示的な静的コンストラクターを宣言しています。 この規則違反を修正するには、静的データが宣言されたとき、および静的コンストラクターを削除するときに、静的データをすべて初期化します。|
|[CA2208:引数の例外を正しくインスタンス化します](../code-quality/ca2208-instantiate-argument-exceptions-correctly.md)|ArgumentException またはそのクラスから派生した例外の種類の既定 (パラメーターなし) のコンストラクターに対して呼び出しが行われたか、ArgumentException またはそのクラスから派生した例外の種類のパラメーター付きのコンストラクターに不適切な文字列型の引数が渡されました。|
|[CA2211:非定数フィールドは表示されません](../code-quality/ca2211-non-constant-fields-should-not-be-visible.md)|定数でも読み取り専用でもない静的フィールドは、スレッド セーフではありません。 このようなフィールドへのアクセスは慎重に制御する必要があり、クラスオブジェクトへのアクセスを同期するための高度なプログラミング手法が必要です。|
|[CA2212:サービス コンポーネントを WebMethod に設定しません](../code-quality/ca2212-do-not-mark-serviced-components-with-webmethod.md)|System.enterpriseservices を継承する型のメソッドは、WebMethodAttribute でマークされています。 ServicedComponent WebMethodAttribute と ServicedComponent メソッドは、コンテキストおよびトランザクション フローの動作および要件が衝突するため、状況によっては正常に動作しません。|
|[CA2213:破棄可能なフィールドは破棄されなければなりません](../code-quality/ca2213-disposable-fields-should-be-disposed.md)|System.IDisposable を実装する型が、IDisposable も実装する型を持つフィールドを宣言しています。 このフィールドの Dispose メソッドは、宣言している型の Dispose メソッドから呼び出されていません。|
|[CA2214:コンストラクターのオーバーライド可能なメソッドを呼び出しません](../code-quality/ca2214-do-not-call-overridable-methods-in-constructors.md)|コンストラクターが仮想メソッドを呼び出すと、そのメソッドを呼び出すインスタンスのコンストラクターが実行されていない可能性があります。|
|[CA2215:Dispose メソッドが基底クラスの Dispose を呼び出す必要があります](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)|型が、破棄できる型から継承している場合、使用している Dispose メソッド内から基本型の Dispose メソッドを呼び出す必要があります。|
|[CA2216:破棄可能な型はファイナライザーを宣言しなければなりません](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)|System.object を実装し、アンマネージリソースの使用を提案するフィールドを持つ型は、「オブジェクトの最終処理」で説明されているように、ファイナライザーを実装しません。|
|[CA2217:列挙型を FlagsAttribute に設定しません](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)|外部から参照できる列挙体は、FlagsAttribute でマークされ、列挙体の2つまたは複数の定義済みの値の組み合わせではない1つ以上の値を持ちます。|
|[CA2218:オーバーライドする Equals で GetHashCode をオーバーライドします](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)|GetHashCode は、現在のインスタンスに基づいて、ハッシュ アルゴリズムとデータ構造 (ハッシュ テーブルなど) に適した値を返します。 同じ型で等値の 2 つのオブジェクトによって同じハッシュ コードが返される必要があります。|
|[CA2219:exception 句に例外を発生させないでください](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)|finally 句または fault 句で例外が発生すると、アクティブな例外が新しい例外によって隠されます。 filter 句で例外が発生すると、ランタイムがその例外を暗黙的にキャッチします。 これにより、元のエラーの検出とデバッグが困難になります。|
|[CA2220:ファイナライザーは基底クラスのファイナライザーを呼び出さなければなりません](../code-quality/ca2220-finalizers-should-call-base-class-finalizer.md)|終了処理は、継承の階層構造を使用して反映する必要があります。 これを確実に行うには、型が型の Finalize メソッドで基本クラスの Finalize メソッドを呼び出す必要があります。|
|[CA2221:ファイナライザーは保護されなければなりません](../code-quality/ca2221-finalizers-should-be-protected.md)|ファイナライザーは、ファミリ アクセス修飾子を使用する必要があります。|
|[CA2222:継承されたメンバーの参照範囲を縮小しません](../code-quality/ca2222-do-not-decrease-inherited-member-visibility.md)|継承メンバーのアクセス修飾子は変更しないでください。 継承メンバーをプライベートに変更しても、呼び出し元はメソッドの基本クラスの実装にアクセスできます。|
|[CA2223:メンバーは、戻り値の型以外にも異なる点がなければなりません](../code-quality/ca2223-members-should-differ-by-more-than-return-type.md)|共通言語ランタイムでは、戻り値の型以外は同じであるメンバーの区別に戻り値の型を使用することが許可されていますが、この機能は共通言語仕様ではなく、.NET プログラミング言語の共通機能でもありません。|
|[CA2224:オーバーロードする演算子 equals で Equals をオーバーライドします](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)|パブリック型は等値演算子を実装しますが、Object.equals をオーバーライドしません。|
|[CA2225:演算子オーバーロードには名前付けされた代替が存在します](../code-quality/ca2225-operator-overloads-have-named-alternates.md)|演算子のオーバーロードが検出され、予想される名前の代替メソッドが検出されませんでした。 名前付き代替メンバーは、演算子と同じ機能へのアクセスを提供し、オーバーロードされた演算子をサポートしない言語でプログラミングする開発者向けに用意されています。|
|[CA2226:演算子は対称型オーバーロードを含まなければなりません](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)|型は等値演算子または非等値演算子を実装し、逆の演算子は実装しません。|
|[CA2227:Collection プロパティは読み取り専用でなければなりません](../code-quality/ca2227-collection-properties-should-be-read-only.md)|書き込み可能なコレクション プロパティにより、ユーザーはコレクションを異なるコレクションで置換できます。 読み取り専用プロパティは、コレクションを置換できないようにしますが、個別のメンバーが設定されることは回避できません。|
|[CA2228:未公開のリソース形式を出荷しません](../code-quality/ca2228-do-not-ship-unreleased-resource-formats.md)|プレリリースバージョンの .NET Framework を使用してビルドされたリソースファイルは、サポートされているバージョンの .NET Framework では使用できない可能性があります。|
|[CA2229:シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)|この規則違反を修正するには、シリアル化コンストラクターを実装します。 シールされたクラスの場合、コンストラクターをプライベートにするか、プロテクトにします。|
|[CA2230:可変引数に対して param を使用します](../code-quality/ca2230-use-params-for-variable-arguments.md)|パブリック型またはプロテクト型に、params キーワードではなく VarArgs 呼び出し規則を使用するパブリック メソッドまたはプロテクト メソッドが含まれています。|
|[CA2231:ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)|値型は、Object.Equals をオーバーライドしていますが、等値演算子を実装していません。|
|[CA2232:Windows フォームのエントリ ポイントを STAThread に設定します](../code-quality/ca2232-mark-windows-forms-entry-points-with-stathread.md)|STAThreadAttribute は、アプリケーションの COM スレッド処理モデルがシングルスレッド アパートメントであることを示します。 この属性は、Windows フォームを使用するすべてのアプリケーションのエントリ ポイントに指定する必要があります。省略すると、Windows コンポーネントが正常に機能しないことがあります。|
|[CA2233:操作はオーバーフローできません](../code-quality/ca2233-operations-should-not-overflow.md)|最初にオペランドを検証せずに算術演算を実行しないでください。演算の結果が、関連するデータ型の有効な値の範囲を超えていないことを確認してください。|
|[CA2234:文字列の代わりに System.Uri オブジェクトを渡します](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)|"uri"、"URI"、"urn"、"URN"、"url"、または "URL" という名前を持つ文字列パラメーターが指定されているメソッドに対して、呼び出しが行われました。  そのメソッドの型宣言に対応するメソッドのオーバーロードが存在し、それに対して System.Uri パラメーターが指定されています。|
|[CA2235:すべてのシリアル化不可能なフィールドを設定します](../code-quality/ca2235-mark-all-non-serializable-fields.md)|シリアル化できない型のインスタンス フィールドが、シリアル化できる型で宣言されています。|
|[CA2236:ISerializable 型で基底クラス メソッドを呼び出します](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)|この規則違反を修正するには、基本型の GetObjectData メソッドまたはシリアル化コンストラクターを、対応する派生型のメソッドまたはコンストラクターから呼び出します。|
|[CA2237:ISerializable 型を SerializableAttribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)|共通言語ランタイムによってシリアル化可能として認識されるようにするには、型が ISerializable インターフェイスの実装によってカスタムシリアル化ルーチンを使用する場合でも、型は SerializableAttribute 属性でマークする必要があります。|
|[CA2238:シリアル化メソッドを正しく実装します](../code-quality/ca2238-implement-serialization-methods-correctly.md)|シリアル化イベントを処理するメソッドに、適切なシグネチャ、戻り値の型、または参照範囲がありません。|
|[CA2239:省略可能なフィールドに、逆シリアル化メソッドを指定します](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)|型には OptionalFieldAttribute 属性でマークされたフィールドがありますが、この型ではシリアル化解除のイベント処理メソッドが提供されていません。|
|[CA2240:ISerializable を正しく実装します](../code-quality/ca2240-implement-iserializable-correctly.md)|この規則違反を修正するには、GetObjectData メソッドを表示およびオーバーライド可能にし、すべてのインスタンスフィールドがシリアル化プロセスに含まれるか、または NonSerializedAttribute 属性で明示的にマークされていることを確認します。|
|[CA2241:書式設定メソッドに正しい引数を提供](../code-quality/ca2241-provide-correct-arguments-to-formatting-methods.md)|System.string に渡される format 引数に、各オブジェクト引数に対応する書式指定項目が含まれていません。また、その逆も同様です。|
|[CA2242:NaN に対して正しくテストします](../code-quality/ca2242-test-for-nan-correctly.md)|この式が Single.Nan または Double.Nan に対して値をテストしています。 値をテストするには、Single.IsNan(Single) または Double.IsNan(Double) を使用します。|
|[CA2243:属性文字列リテラルは、正しく解析する必要があります](../code-quality/ca2243-attribute-string-literals-should-parse-correctly.md)|属性の文字列リテラルパラメーターは、URL、GUID、またはバージョンに対して正しく解析されません。|
