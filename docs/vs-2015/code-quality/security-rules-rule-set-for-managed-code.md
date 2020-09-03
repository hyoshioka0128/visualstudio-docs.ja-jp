---
title: マネージコードの "セキュリティ規則" 規則セット |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 564aeac6-03fa-41b0-b655-88179f0ab01b
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 66d1c3feb33ae1a42478f7742fb0491bff3441e2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72605426"
---
# <a name="security-rules-rule-set-for-managed-code"></a>マネージド コードの "セキュリティ規則" 規則セット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

報告されるセキュリティの潜在的な問題の数を最大化するには、Microsoft セキュリティ規則の規則セットを含める必要があります。

|ルール|説明|
|----------|-----------------|
|[CA2100](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md)|SQL クエリのセキュリティ脆弱性を確認|
|[CA2102](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md)|汎用ハンドラーの CLSCompliant でない例外をキャッチします|
|[CA2103](../code-quality/ca2103-review-imperative-security.md)|命令型のセキュリティを確認します|
|[CA2104](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md)|読み取り専用の変更可能な参照型を宣言しません|
|[CA2105](../code-quality/ca2105-array-fields-should-not-be-read-only.md)|配列フィールドを読み取り専用にすることはできません|
|[CA2106](../code-quality/ca2106-secure-asserts.md)|アサートをセキュリティで保護します|
|[CA2107](../code-quality/ca2107-review-deny-and-permit-only-usage.md)|拒否および許可のみの使用を確認します|
|[CA2108](../code-quality/ca2108-review-declarative-security-on-value-types.md)|値型での宣言セキュリティを確認します|
|[CA2109](../code-quality/ca2109-review-visible-event-handlers.md)|表示するイベント ハンドラーを確認します|
|[CA2111](../code-quality/ca2111-pointers-should-not-be-visible.md)|ポインターは参照可能にすることはできません|
|[CA2112](../code-quality/ca2112-secured-types-should-not-expose-fields.md)|セキュリティで保護された型はフィールドを公開してはなりません|
|[CA2114](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md)|メソッド セキュリティは型のスーパーセットでなければなりません|
|[CA2115](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)|ネイティブ リソースを使用しているときには GC.KeepAlive を呼び出します|
|[CA2116](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)|APTCA メソッドは APTCA メソッドのみを呼び出すことができます|
|[CA2117](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)|APTCA 型は APTCA 基本型のみを拡張することができます|
|[CA2118](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md)|SuppressUnmanagedCodeSecurityAttribute の使用法を確認してください|
|[CA2119](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md)|プライベート インターフェイスを満たすメソッドをシールします|
|[CA2120](../code-quality/ca2120-secure-serialization-constructors.md)|シリアル化コンストラクターをセキュリティで保護します|
|[CA2121](../code-quality/ca2121-static-constructors-should-be-private.md)|静的コンストラクターはプライベートでなければなりません|
|[CA2122](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)|リンク要求を含むメソッドを間接的に公開しません|
|[CA2123](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)|オーバーライドのリンク要求はベースと同一でなければなりません|
|[CA2124](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md)|脆弱性のある finally 句を外側の try でラップします|
|[CA2126](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md)|型のリンク要求には継承要求が必要です|
|[CA2130](../code-quality/ca2130-security-critical-constants-should-be-transparent.md)|セキュリティ上重要な定数は透過的である必要がある|
|[CA2131](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md)|セキュリティ上重要な型は型等価性に参加してはならない|
|[CA2132](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md)|既定のコンストラクターは、基本型の既定コンストラクターと同程度以上、重要であることが必要|
|[CA2133](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md)|デリゲートは透過性の整合がとれたメソッドにバインドする必要がある|
|[CA2134](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md)|メソッドは、基本メソッドをオーバーライドしている場合、透過性の整合性を保つ必要がある|
|[CA2135](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md)|レベル 2 のアセンブリは LinkDemand を含んではならない|
|[CA2136](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|メンバーには、透過性注釈の競合があってはならない|
|[CA2137](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md)|透過的メソッドは、検証可能な IL のみを含まなければならない|
|[CA2138](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md)|透過的メソッドは、SuppressUnmanagedCodeSecurity 属性を持つメソッドを呼び出してはならない|
|[CA2139](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md)|透過的メソッドは、HandleProcessCorruptingExceptions 属性を使用してはならない|
|[CA2140](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|透過的コードは、セキュリティ上重要な項目を参照してはならない|
|[CA2141](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md)|透過的メソッドは Linkdemand を満たしてはならない|
|[CA2142](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)|透過的コードは、LinkDemand を使用して保護されてはならない|
|[CA2143](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md)|透過的メソッドは、セキュリティ確認要求を使用してはならない|
|[CA2144](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md)|透過的コードは、バイト配列からアセンブリを読み込んではならない|
|[CA2145](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md)|透過的メソッドを SuppressUnmanagedCodeSecurityAttribute で修飾してはならない|
|[CA2146](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md)|型は、基本型およびインターフェイスと同程度以上、重要でなければならない|
|[CA2147](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|透過コードは、セキュリティ アサートを使用してはならない|
|[CA2149](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md)|透過的メソッドは、ネイティブ コード内に呼び出しを行ってはならない|
|[CA2210](../code-quality/ca2210-assemblies-should-have-valid-strong-names.md)|アセンブリには有効な厳密な名前が必要です|
