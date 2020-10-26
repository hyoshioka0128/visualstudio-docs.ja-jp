---
title: マネージコードの "拡張デザインガイドライン規則" 規則セット |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: a338caf2-b75d-4f23-a0f9-3024fa0bceac
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0951d337375a7396d1158dc933b77fda13fa91a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667620"
---
# <a name="extended-design-guidelines-rules-rule-set-for-managed-code"></a>マネージド コードの "拡張デザイン ガイドライン規則" 規則セット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft 拡張デザインガイドライン規則セットは、基本デザインガイドライン規則を拡張して、報告されるユーザビリティと保守容易性の問題を最大化します。 特に、命名に関するガイドラインに重点が置かれています。 プロジェクトにライブラリコードが含まれている場合、または保守しやすいコードを記述するために最高の基準を適用する場合は、この規則セットを含めることを検討してください。

 拡張デザインガイドライン規則には、Microsoft の基本デザインガイドライン規則がすべて含まれています。 基本的な設計ガイドライン規則には、Microsoft の最小限の推奨規則がすべて含まれています。 詳細については、「マネージコードの[基本デザインガイドライン規則の規則セット](../code-quality/basic-design-guideline-rules-rule-set-for-managed-code.md)」と「マネージド[コードに対するマネージ推奨規則](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md)の規則セット」を参照してください。

 次の表では、"Microsoft 拡張デザインガイドライン規則" 規則セット内のすべての規則について説明します。

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
|[CA1000](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)|ジェネリック型の静的メンバーを宣言しません|
|[CA1002](../code-quality/ca1002-do-not-expose-generic-lists.md)|ジェネリック リストを公開しません|
|[CA1003](../code-quality/ca1003-use-generic-event-handler-instances.md)|汎用イベント ハンドラーのインスタンスを使用します|
|[CA1004](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)|ジェネリック メソッドは型パラメーターを指定しなければなりません|
|[CA1005](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)|ジェネリック型でパラメーターを使用しすぎないでください|
|[CA1006](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)|ジェネリック型をメンバー シグネチャ内で入れ子にしません|
|[CA1007](../code-quality/ca1007-use-generics-where-appropriate.md)|適切な場所にジェネリックを使用します|
|[CA1008](../code-quality/ca1008-enums-should-have-zero-value.md)|Enums は 0 値を含んでいなければなりません|
|[CA1010](../code-quality/ca1010-collections-should-implement-generic-interface.md)|コレクションは、ジェネリック インターフェイスを実装しなければなりません|
|[CA1011](../code-quality/ca1011-consider-passing-base-types-as-parameters.md)|基本型をパラメーターとして渡すことを考慮します|
|[CA1012](../code-quality/ca1012-abstract-types-should-not-have-constructors.md)|抽象型にはコンストラクターを含めません|
|[CA1013](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)|オーバーロードする加算および減算で、演算子 equals をオーバーロードします|
|[CA1014](../code-quality/ca1014-mark-assemblies-with-clscompliantattribute.md)|アセンブリに CLSCompliantAttribute を設定します|
|[CA1017](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)|アセンブリに ComVisibleAttribute を設定します|
|[CA1018](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md)|属性を AttributeUsageAttribute に設定します|
|[CA1019](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)|属性引数にアクセサーを定義します|
|[CA1023](../code-quality/ca1023-indexers-should-not-be-multidimensional.md)|インデクサーを多次元にすることはできません|
|[CA1024](../code-quality/ca1024-use-properties-where-appropriate.md)|適切な場所にプロパティを使用します|
|[CA1025](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)|反復する引数を params 配列で置き換えます|
|[CA1026](../code-quality/ca1026-default-parameters-should-not-be-used.md)|既定パラメーターを使用することはできません|
|[CA1027](../code-quality/ca1027-mark-enums-with-flagsattribute.md)|列挙型を FlagsAttribute に設定します|
|[CA1028](../code-quality/ca1028-enum-storage-should-be-int32.md)|列挙ストレージは Int32 でなければなりません|
|[CA1030](../code-quality/ca1030-use-events-where-appropriate.md)|適切な場所にイベントを使用します|
|[CA1031](../code-quality/ca1031-do-not-catch-general-exception-types.md)|一般的な例外の種類はキャッチしません|
|[CA1032](../code-quality/ca1032-implement-standard-exception-constructors.md)|標準例外コンストラクターを実装します|
|[CA1034](../code-quality/ca1034-nested-types-should-not-be-visible.md)|入れ子にされた型を参照可能にすることはできません|
|[CA1035](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)|ICollection の実装は、厳密に型指定されたメンバーを含んでいます|
|[CA1036](../code-quality/ca1036-override-methods-on-comparable-types.md)|比較可能な型でメソッドをオーバーライドします|
|[CA1038](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)|列挙子は厳密に型指定されていなければなりません|
|[CA1039](../code-quality/ca1039-lists-are-strongly-typed.md)|リストは厳密に型指定されています|
|[CA1041](../code-quality/ca1041-provide-obsoleteattribute-message.md)|ObsoleteAttribute メッセージを指定します|
|[CA1043](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)|インデクサーには整数または文字列引数を使用します|
|[CA1044](../code-quality/ca1044-properties-should-not-be-write-only.md)|プロパティを書き込み専用にすることはできません|
|[CA1046](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)|参照型で、演算子 equals をオーバーロードしないでください|
|[CA1047: SEALED](../code-quality/ca1047-do-not-declare-protected-members-in-sealed-types.md)|シールド型の保護されたメンバーを宣言しません|
|[CA1048: SEALED](../code-quality/ca1048-do-not-declare-virtual-members-in-sealed-types.md)|シールド型の仮想メンバーを宣言しません|
|[CA1050](../code-quality/ca1050-declare-types-in-namespaces.md)|名前空間で型を宣言します|
|[CA1051](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)|参照可能なインスタンス フィールドを宣言しません|
|[CA1052](../code-quality/ca1052-static-holder-types-should-be-sealed.md)|スタティック ホルダー型はシールドされていなければなりません|
|[CA1053](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md)|スタティック ホルダー型はコンストラクターを含むことはできません|
|[CA1054](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)|URI パラメーターを文字列にすることはできません|
|[CA1055](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)|URI 戻り値を文字列にすることはできません|
|[CA1056](../code-quality/ca1056-uri-properties-should-not-be-strings.md)|URI プロパティを文字列にすることはできません|
|[CA1057](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)|文字列 URI オーバーロードが、System.Uri オーバーロードを呼び出します|
|[CA1058](../code-quality/ca1058-types-should-not-extend-certain-base-types.md)|型は、一定の基本型を拡張することはできません|
|[CA1059](../code-quality/ca1059-members-should-not-expose-certain-concrete-types.md)|メンバーは特定の具象型を公開できません|
|[CA1064](../code-quality/ca1064-exceptions-should-be-public.md)|例外は public として設定する必要があります|
|[CA1500](../code-quality/ca1500-variable-names-should-not-match-field-names.md)|変数名はフィールド名と同一にすることはできません|
|[CA1502](../code-quality/ca1502-avoid-excessive-complexity.md)|メソッドの実装を複雑にしすぎないでください|
|[CA1708](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)|識別子は、大文字と小文字の区別以外にも相違していなければなりません|
|[CA1716](../code-quality/ca1716-identifiers-should-not-match-keywords.md)|識別子はキーワードと同一にすることはできません|
|[CA1801](../code-quality/ca1801-review-unused-parameters.md)|使用されていないパラメーターの確認|
|[CA1804](../code-quality/ca1804-remove-unused-locals.md)|使用されていないローカルを削除します|
|[CA1809](../code-quality/ca1809-avoid-excessive-locals.md)|ローカルを使用しすぎないでください|
|[CA1810](../code-quality/ca1810-initialize-reference-type-static-fields-inline.md)|参照型の静的フィールドをインラインで初期化します|
|[CA1811](../code-quality/ca1811-avoid-uncalled-private-code.md)|呼び出されていないプライベート コードを使用しません|
|[CA1812](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)|インスタンス化されていない内部クラスを使用しません|
|[CA1813](../code-quality/ca1813-avoid-unsealed-attributes.md)|アンシールド属性を使用しません|
|[CA1814](../code-quality/ca1814-prefer-jagged-arrays-over-multidimensional.md)|複数次元の配列ではなくジャグ配列を使用します|
|[CA1815](../code-quality/ca1815-override-equals-and-operator-equals-on-value-types.md)|equals および operator equals を値型でオーバーライドします|
|[CA1819](../code-quality/ca1819-properties-should-not-return-arrays.md)|プロパティは、配列を返すことはできません|
|[CA1820](../code-quality/ca1820-test-for-empty-strings-using-string-length.md)|文字列の長さを使用して空の文字列をテストします|
|[CA1822](../code-quality/ca1822-mark-members-as-static.md)|メンバーを static に設定します|
|[CA1823](../code-quality/ca1823-avoid-unused-private-fields.md)|使用されていないプライベート フィールドを使用しません|
|[CA2201](../code-quality/ca2201-do-not-raise-reserved-exception-types.md)|予約された例外の種類を発生させません|
|[CA2205](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)|Win32 API に相当するマネージド API を使用します|
|[CA2208](../code-quality/ca2208-instantiate-argument-exceptions-correctly.md)|引数の例外を正しくインスタンス化します|
|[CA2211](../code-quality/ca2211-non-constant-fields-should-not-be-visible.md)|非定数フィールドは表示されません|
|[CA2217](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)|列挙型を FlagsAttribute に設定しません|
|[CA2219](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)|exception 句に例外を発生させないでください|
|[CA2221](../code-quality/ca2221-finalizers-should-be-protected.md)|ファイナライザーは保護されなければなりません|
|[CA2222](../code-quality/ca2222-do-not-decrease-inherited-member-visibility.md)|継承されたメンバーの参照範囲を縮小しません|
|[CA2223](../code-quality/ca2223-members-should-differ-by-more-than-return-type.md)|メンバーは、戻り値の型以外にも異なる点がなければなりません|
|[CA2224](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)|オーバーロードする演算子 equals で Equals をオーバーライドします|
|[CA2225](../code-quality/ca2225-operator-overloads-have-named-alternates.md)|演算子オーバーロードには名前付けされた代替が存在します|
|[CA2226](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)|演算子は対称型オーバーロードを含まなければなりません|
|[CA2227](../code-quality/ca2227-collection-properties-should-be-read-only.md)|Collection プロパティは読み取り専用でなければなりません|
|[CA2230](../code-quality/ca2230-use-params-for-variable-arguments.md)|可変引数に対して param を使用します|
|[CA2234](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)|文字列の代わりに System.Uri オブジェクトを渡します|
|[CA2239](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)|省略可能なフィールドに、逆シリアル化メソッドを指定します|
|[CA1020](../code-quality/ca1020-avoid-namespaces-with-few-types.md)|型をほとんど含まない名前空間を使用しません|
|[CA1021](../code-quality/ca1021-avoid-out-parameters.md)|out パラメーターを使用しません|
|[CA1040](../code-quality/ca1040-avoid-empty-interfaces.md)|空のインターフェイスは使用しません|
|[CA1045](../code-quality/ca1045-do-not-pass-types-by-reference.md)|型を参照によって渡しません|
|[CA1062](../code-quality/ca1062-validate-arguments-of-public-methods.md)|パブリック メソッドの引数の検証|
|[CA1501](../code-quality/ca1501-avoid-excessive-inheritance.md)|継承を使用しすぎないでください|
|[CA1504](../code-quality/ca1504-review-misleading-field-names.md)|紛らわしいフィールド名を確認します|
|[CA1505](../code-quality/ca1505-avoid-unmaintainable-code.md)|メンテナンスできないコードを使用しないでください|
|[CA1506](../code-quality/ca1506-avoid-excessive-class-coupling.md)|クラス結合度を大きくしすぎないでください|
|[CA1700](../code-quality/ca1700-do-not-name-enum-values-reserved.md)|列挙型値に 'Reserved' という名前を指定しません|
|[CA1701](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)|リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません|
|[CA1702](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)|複合語では、大文字と小文字が正しく区別されなければなりません|
|[CA1703](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)|リソース文字列は正しく入力されなければなりません|
|[CA1704](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)|識別子は正しく入力されなければなりません|
|[CA1707](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)|識別子はアンダースコアを含むことはできません|
|[CA1709](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)|識別子では、大文字と小文字が正しく区別されなければなりません|
|[CA1710](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)|識別子は、正しいサフィックスを含んでいなければなりません|
|[CA1711](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)|識別子は、不適切なサフィックスを含むことはできません|
|[CA1712](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)|列挙型値を型名のプレフィックスにしません|
|[CA1713](../code-quality/ca1713-events-should-not-have-before-or-after-prefix.md)|イベントは、before または after プレフィックスを含むことはできません|
|[CA1714](../code-quality/ca1714-flags-enums-should-have-plural-names.md)|フラグ列挙型は、複数形の名前を含んでいなければなりません|
|[CA1715](../code-quality/ca1715-identifiers-should-have-correct-prefix.md)|識別子は正しいプレフィックスを含んでいなければなりません|
|[CA1717](../code-quality/ca1717-only-flagsattribute-enums-should-have-plural-names.md)|FlagsAttribute 列挙型のみが複数形の名前を含んでいなければなりません|
|[CA1719](../code-quality/ca1719-parameter-names-should-not-match-member-names.md)|パラメーター名はメンバー名と同一にすることはできません|
|[CA1720](../code-quality/ca1720-identifiers-should-not-contain-type-names.md)|識別子には型名を含めないでください|
|[CA1721](../code-quality/ca1721-property-names-should-not-match-get-methods.md)|プロパティ名は get メソッドと同一にすることはできません|
|[CA1722](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md)|識別子は不適切なプレフィックスを含むことはできません|
|[CA1724](../code-quality/ca1724-type-names-should-not-match-namespaces.md)|型名は名前空間と同一にすることはできません|
|[CA1725](../code-quality/ca1725-parameter-names-should-match-base-declaration.md)|パラメーター名は基本宣言と同一でなければなりません|
|[CA1726](../code-quality/ca1726-use-preferred-terms.md)|適切な用語を使用します|
|[CA2204](../code-quality/ca2204-literals-should-be-spelled-correctly.md)|リテラルに正しいスペルを要求|
