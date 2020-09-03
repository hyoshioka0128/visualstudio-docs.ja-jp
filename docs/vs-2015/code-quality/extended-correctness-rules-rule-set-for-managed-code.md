---
title: マネージコードの "拡張正確性規則" 規則セット |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 5b181f5b-6c7a-4e46-a783-360e1da427a0
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bef208dbcb4c1017840602d198b5099267b25a99
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667640"
---
# <a name="extended-correctness-rules-rule-set-for-managed-code"></a>マネージド コードの "拡張正確性規則" 規則セット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft 拡張正確性規則の規則セットは、コード分析によって報告されるロジックおよびフレームワークの使用エラーを最大化します。 COM 相互運用性やモバイルアプリケーションなど、特定のシナリオに重点が置かれています。 これらのシナリオのいずれかがプロジェクトに適用される場合、またはプロジェクトの追加の問題を検出する場合は、この規則セットを含めることを検討してください。

 Microsoft 拡張正確性規則の規則セットには、Microsoft の "基本正確性規則" 規則セットに含まれる規則が含まれています。 基本的な正確性規則には、"Microsoft の最小推奨規則" 規則セットに含まれる規則が含まれます。 詳細については、「マネージコードとマネージド[コードの "マネージ推奨規則" 規則セット](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md)[の "基本的な正確性規則規則セット](../code-quality/basic-correctness-rules-rule-set-for-managed-code.md)" を参照してください。

 次の表では、Microsoft 拡張正確性規則の規則セットに含まれるすべての規則について説明します。

|ルール|説明|
|----------|-----------------|
|[CA1001](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)|破棄可能なフィールドを所有する型は、破棄可能でなければなりません|
|[CA1009](../code-quality/ca1009-declare-event-handlers-correctly.md)|イベント ハンドラーを正しく宣言します|
|[CA1016](../code-quality/ca1016-mark-assemblies-with-assemblyversionattribute.md)|アセンブリに AssemblyVersionAttribute を設定します|
|[CA1033](../code-quality/ca1033-interface-methods-should-be-callable-by-child-types.md)|インターフェイス メソッドは、子型によって呼び出し可能でなければなりません|
|[CA1049](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)|ネイティブ リソースを所有する型は、破棄可能でなければなりません|
|[CA1060](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)|P/Invoke を NativeMethods クラスに移動します|
|[CA1061](../code-quality/ca1061-do-not-hide-base-class-methods.md)|基底クラス メソッドを非表示にしません|
|[CA1063](../code-quality/ca1063-implement-idisposable-correctly.md)|IDisposable を正しく実装します|
|[CA1065](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)|予期しない場所に例外を発生させません|
|[CA1301](../code-quality/ca1301-avoid-duplicate-accelerators.md)|重複するアクセラレータを使用しません|
|[CA1400](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)|P/Invoke エントリ ポイントは存在しなければなりません|
|[CA1401](../code-quality/ca1401-p-invokes-should-not-be-visible.md)|P/Invoke は参照可能であることはできません|
|[CA1403](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)|Auto 配置の型を COM 参照可能にすることはできません|
|[CA1404](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md)|P/Invoke の直後に GetLastError を呼び出します|
|[CA1405](../code-quality/ca1405-com-visible-type-base-types-should-be-com-visible.md)|COM 参照可能な型の基本型は COM 参照可能でなければなりません|
|[CA1410](../code-quality/ca1410-com-registration-methods-should-be-matched.md)|COM 登録メソッドは一致しなければなりません|
|[CA1415](../code-quality/ca1415-declare-p-invokes-correctly.md)|P/Invoke を正しく宣言します|
|[CA1821](../code-quality/ca1821-remove-empty-finalizers.md)|空のファイナライザーを削除します|
|[CA1900](../code-quality/ca1900-value-type-fields-should-be-portable.md)|値型フィールドはポータブルでなければなりません|
|[CA1901](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)|P/Invoke 宣言はポータブルでなければなりません|
|[CA2002](../code-quality/ca2002-do-not-lock-on-objects-with-weak-identity.md)|弱い ID を伴うオブジェクト上でロックしません|
|[CA2100](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md)|SQL クエリのセキュリティ脆弱性を確認|
|[CA2101](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)|P/Invoke 文字列引数に対してマーシャリングを指定します|
|[CA2108](../code-quality/ca2108-review-declarative-security-on-value-types.md)|値型での宣言セキュリティを確認します|
|[CA2111](../code-quality/ca2111-pointers-should-not-be-visible.md)|ポインターは参照可能にすることはできません|
|[CA2112](../code-quality/ca2112-secured-types-should-not-expose-fields.md)|セキュリティで保護された型はフィールドを公開してはなりません|
|[CA2114](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md)|メソッド セキュリティは型のスーパーセットでなければなりません|
|[CA2116](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)|APTCA メソッドは APTCA メソッドのみを呼び出すことができます|
|[CA2117](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)|APTCA 型は APTCA 基本型のみを拡張することができます|
|[CA2122](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)|リンク要求を含むメソッドを間接的に公開しません|
|[CA2123](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)|オーバーライドのリンク要求はベースと同一でなければなりません|
|[CA2124](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md)|脆弱性のある finally 句を外側の try でラップします|
|[CA2126](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md)|型のリンク要求には継承要求が必要です|
|[CA2131](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md)|セキュリティ上重要な型は型等価性に参加してはならない|
|[CA2132](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md)|既定のコンストラクターは、基本型の既定コンストラクターと同程度以上、重要であることが必要|
|[CA2133](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md)|デリゲートは透過性の整合がとれたメソッドにバインドする必要がある|
|[CA2134](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md)|メソッドは、基本メソッドをオーバーライドしている場合、透過性の整合性を保つ必要がある|
|[CA2137](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md)|透過的メソッドは、検証可能な IL のみを含まなければならない|
|[CA2138](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md)|透過的メソッドは、SuppressUnmanagedCodeSecurity 属性を持つメソッドを呼び出してはならない|
|[CA2140](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|透過的コードは、セキュリティ上重要な項目を参照してはならない|
|[CA2141](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md)|透過的メソッドは Linkdemand を満たしてはならない|
|[CA2146](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md)|型は、基本型およびインターフェイスと同程度以上、重要でなければならない|
|[CA2147](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|透過コードは、セキュリティ アサートを使用してはならない|
|[CA2149](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md)|透過的メソッドは、ネイティブ コード内に呼び出しを行ってはならない|
|[CA2200](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)|スタック詳細を保持するために再度スローします|
|[CA2202](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md)|オブジェクトを複数回破棄しない|
|[CA2207](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)|値型のスタティック フィールドのインラインを初期化します|
|[CA2212](../code-quality/ca2212-do-not-mark-serviced-components-with-webmethod.md)|サービス コンポーネントを WebMethod に設定しません|
|[CA2213](../code-quality/ca2213-disposable-fields-should-be-disposed.md)|破棄可能なフィールドは破棄されなければなりません|
|[CA2214](../code-quality/ca2214-do-not-call-overridable-methods-in-constructors.md)|コンストラクターのオーバーライド可能なメソッドを呼び出しません|
|[CA2216](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)|破棄可能な型はファイナライザーを宣言しなければなりません|
|[CA2220](../code-quality/ca2220-finalizers-should-call-base-class-finalizer.md)|ファイナライザーは基底クラスのファイナライザーを呼び出さなければなりません|
|[CA2229](../code-quality/ca2229-implement-serialization-constructors.md)|シリアル化コンストラクターを実装します|
|[CA2231](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)|ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします|
|[CA2232](../code-quality/ca2232-mark-windows-forms-entry-points-with-stathread.md)|Windows フォームのエントリ ポイントを STAThread に設定します|
|[CA2235](../code-quality/ca2235-mark-all-non-serializable-fields.md)|すべてのシリアル化不可能なフィールドを設定します|
|[CA2236](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)|ISerializable 型で基底クラス メソッドを呼び出します|
|[CA2237](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)|ISerializable 型を SerializableAttribute に設定します|
|[CA2238](../code-quality/ca2238-implement-serialization-methods-correctly.md)|シリアル化メソッドを正しく実装します|
|[CA2240](../code-quality/ca2240-implement-iserializable-correctly.md)|ISerializable を正しく実装します|
|[CA2241](../code-quality/ca2241-provide-correct-arguments-to-formatting-methods.md)|書式設定メソッドに正しい引数を提供|
|[CA2242](../code-quality/ca2242-test-for-nan-correctly.md)|NaN に対して正しくテストします|
|[CA1008](../code-quality/ca1008-enums-should-have-zero-value.md)|Enums は 0 値を含んでいなければなりません|
|[CA1013](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)|オーバーロードする加算および減算で、演算子 equals をオーバーロードします|
|[CA1303](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)|ローカライズされるパラメーターとしてリテラルを渡さない|
|[CA1308](../code-quality/ca1308-normalize-strings-to-uppercase.md)|文字列を大文字に標準化します|
|[CA1806](../code-quality/ca1806-do-not-ignore-method-results.md)|メソッドの結果を無視しない|
|[CA1816](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)|GC.SuppressFinalize を正しく呼び出します|
|[CA1819](../code-quality/ca1819-properties-should-not-return-arrays.md)|プロパティは、配列を返すことはできません|
|[CA1820](../code-quality/ca1820-test-for-empty-strings-using-string-length.md)|文字列の長さを使用して空の文字列をテストします|
|[CA1903](../code-quality/ca1903-use-only-api-from-targeted-framework.md)|対象のフレームワークから API のみを使用します|
|[CA2004](../code-quality/ca2004-remove-calls-to-gc-keepalive.md)|GC.KeepAlive への呼び出しを削除します|
|[CA2006](../code-quality/ca2006-use-safehandle-to-encapsulate-native-resources.md)|SafeHandle を使用して、ネイティブ リソースを要約します|
|[CA2102](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md)|汎用ハンドラーの CLSCompliant でない例外をキャッチします|
|[CA2104](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md)|読み取り専用の変更可能な参照型を宣言しません|
|[CA2105](../code-quality/ca2105-array-fields-should-not-be-read-only.md)|配列フィールドを読み取り専用にすることはできません|
|[CA2106](../code-quality/ca2106-secure-asserts.md)|アサートをセキュリティで保護します|
|[CA2115](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)|ネイティブ リソースを使用しているときには GC.KeepAlive を呼び出します|
|[CA2119](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md)|プライベート インターフェイスを満たすメソッドをシールします|
|[CA2120](../code-quality/ca2120-secure-serialization-constructors.md)|シリアル化コンストラクターをセキュリティで保護します|
|[CA2121](../code-quality/ca2121-static-constructors-should-be-private.md)|静的コンストラクターはプライベートでなければなりません|
|[CA2130](../code-quality/ca2130-security-critical-constants-should-be-transparent.md)|セキュリティ上重要な定数は透過的である必要がある|
|[CA2205](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)|Win32 API に相当するマネージド API を使用します|
|[CA2215](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)|Dispose メソッドが基底クラスの Dispose を呼び出す必要があります|
|[CA2221](../code-quality/ca2221-finalizers-should-be-protected.md)|ファイナライザーは保護されなければなりません|
|[CA2222](../code-quality/ca2222-do-not-decrease-inherited-member-visibility.md)|継承されたメンバーの参照範囲を縮小しません|
|[CA2223](../code-quality/ca2223-members-should-differ-by-more-than-return-type.md)|メンバーは、戻り値の型以外にも異なる点がなければなりません|
|[CA2224](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)|オーバーロードする演算子 equals で Equals をオーバーライドします|
|[CA2226](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)|演算子は対称型オーバーロードを含まなければなりません|
|[CA2227](../code-quality/ca2227-collection-properties-should-be-read-only.md)|Collection プロパティは読み取り専用でなければなりません|
|[CA2239](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)|省略可能なフィールドに、逆シリアル化メソッドを指定します|
|[CA1032](../code-quality/ca1032-implement-standard-exception-constructors.md)|標準例外コンストラクターを実装します|
|[CA1054](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)|URI パラメーターを文字列にすることはできません|
|[CA1055](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)|URI 戻り値を文字列にすることはできません|
|[CA1056](../code-quality/ca1056-uri-properties-should-not-be-strings.md)|URI プロパティを文字列にすることはできません|
|[CA1057](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)|文字列 URI オーバーロードが、System.Uri オーバーロードを呼び出します|
|[CA1402](../code-quality/ca1402-avoid-overloads-in-com-visible-interfaces.md)|COM 参照可能インターフェイスでのオーバーロードを避けてください|
|[CA1406](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md)|Visual Basic 6 クライアントに対しては Int64 引数を使用しません|
|[CA1407](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)|Com 参照可能な型で静的メンバーを使用しません|
|[CA1408](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)|AutoDual ClassInterfaceType を使用しないでください|
|[CA1409](../code-quality/ca1409-com-visible-types-should-be-creatable.md)|COM 参照可能な型は作成可能でなければなりません|
|[CA1411](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)|COM 登録メソッドは参照可能であることはできません|
|[CA1412](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)|ComSource インターフェイスを IDispatch として設定します|
|[CA1413](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)|Com 参照可能な値型ではパブリックでないフィールドを使用しません|
|[CA1414](../code-quality/ca1414-mark-boolean-p-invoke-arguments-with-marshalas.md)|ブール型の P/Invoke 引数を MarshalAs に設定します|
|[CA1600](../code-quality/ca1600-do-not-use-idle-process-priority.md)|アイドル状態のプロセス優先度を使用しません|
|[CA1601](../code-quality/ca1601-do-not-use-timers-that-prevent-power-state-changes.md)|電源の状態の変更を妨げるタイマーを使用しません|
|[CA1824](../code-quality/ca1824-mark-assemblies-with-neutralresourceslanguageattribute.md)|アセンブリを NeutralResourcesLanguageAttribute に設定します|
|[CA2001](../code-quality/ca2001-avoid-calling-problematic-methods.md)|問題が発生する可能性のあるメソッドは呼び出しません|
|[CA2003](../code-quality/ca2003-do-not-treat-fibers-as-threads.md)|ファイバーをスレッドとして扱いません|
|[CA2135](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md)|レベル 2 のアセンブリは LinkDemand を含んではならない|
|[CA2136](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|メンバーには、透過性注釈の競合があってはならない|
|[CA2139](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md)|透過的メソッドは、HandleProcessCorruptingExceptions 属性を使用してはならない|
|[CA2142](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)|透過的コードは、LinkDemand を使用して保護されてはならない|
|[CA2143](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md)|透過的メソッドは、セキュリティ確認要求を使用してはならない|
|[CA2144](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md)|透過的コードは、バイト配列からアセンブリを読み込んではならない|
|[CA2145](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md)|透過的メソッドを SuppressUnmanagedCodeSecurityAttribute で修飾してはならない|
|[CA2204](../code-quality/ca2204-literals-should-be-spelled-correctly.md)|リテラルに正しいスペルを要求|
|[CA2211](../code-quality/ca2211-non-constant-fields-should-not-be-visible.md)|非定数フィールドは表示されません|
|[CA2217](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)|列挙型を FlagsAttribute に設定しません|
|[CA2218](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)|オーバーライドする Equals で GetHashCode をオーバーライドします|
|[CA2219](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)|exception 句に例外を発生させないでください|
|[CA2225](../code-quality/ca2225-operator-overloads-have-named-alternates.md)|演算子オーバーロードには名前付けされた代替が存在します|
|[CA2228](../code-quality/ca2228-do-not-ship-unreleased-resource-formats.md)|未公開のリソース形式を出荷しません|
|[CA2230](../code-quality/ca2230-use-params-for-variable-arguments.md)|可変引数に対して param を使用します|
|[CA2233](../code-quality/ca2233-operations-should-not-overflow.md)|操作はオーバーフローできません|
|[CA2234](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)|文字列の代わりに System.Uri オブジェクトを渡します|
|[CA2243](../code-quality/ca2243-attribute-string-literals-should-parse-correctly.md)|属性文字列リテラルは、正しく解析する必要があります|
