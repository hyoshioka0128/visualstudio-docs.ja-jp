---
title: セキュリティの警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.securityrules
helpviewer_keywords:
- security [Visual Studio ALM], Enterprise Templates
- security warnings
- managed code analysis warnings, security warnings
- warnings, security
ms.assetid: 60d4e8ea-230a-494f-aa6a-b91db77540e4
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b5e30768ac6fa8c3c140156b94082bb2306efb51
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655201"
---
# <a name="security-warnings"></a>セキュリティの警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

セキュリティ警告は、より安全なライブラリとアプリケーションをサポートします。 この警告によって、プログラムにセキュリティ上の欠陥が含まれるのを防ぐことができます。 この警告のいずれかを無効にする場合、明確にコードに理由を記載し、開発プロジェクトの指定されたセキュリティ管理者にも報告します。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA2100:SQL クエリのセキュリティ脆弱性を確認](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md)|メソッドに渡された文字列引数から構築された文字列を使用して System.Data.IDbCommand.CommandText プロパティが設定されています。 この規則では、文字列引数にユーザー入力が含まれていることが想定されています。 ユーザー入力から構築された SQL コマンド文字列には、SQL 注入攻撃に対する脆弱性があります。|
|[CA2102:汎用ハンドラーの CLSCompliant でない例外をキャッチします](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md)|アセンブリ内の RuntimeCompatibilityAttribute でマークされていないメンバーまたは RuntimeCompatibility(WrapNonExceptionThrows = false) でマークされているメンバーには、System.Exception を処理する catch ブロックがあり、その直後に汎用 catch ブロックはありません。|
|[CA2103:命令型のセキュリティを確認します](../code-quality/ca2103-review-imperative-security.md)|メソッドが強制セキュリティを使用しています。また、そのメソッドで、確認要求がアクティブな場合でも変更できるステータス情報または戻り値を使用して、アクセス許可を構築している可能性があります。 できる限り、宣言セキュリティを使用します。|
|[CA2104:読み取り専用の変更可能な参照型を宣言しません](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md)|外部から参照できる型に、変更可能な参照型である、外部から参照可能な読み取り専用のフィールドがあります。 変更可能な型とは、インスタンス データを変更できる型です。|
|[CA2105:配列フィールドを読み取り専用にすることはできません](../code-quality/ca2105-array-fields-should-not-be-read-only.md)|配列を含むフィールドに読み取り専用 (Visual Basic では ReadOnly) 修飾子を適用すると、そのフィールドで参照先の配列を変更できません。 ただし、読み取り専用フィールドに格納された配列の要素は変更できます。|
|[CA2106:アサートをセキュリティで保護します](../code-quality/ca2106-secure-asserts.md)|メソッドによってアクセス許可がアサートされますが、呼び出し元に対してセキュリティ チェックが実行されていません。 セキュリティ チェックを実行せずにセキュリティ アクセス許可をアサートすると、悪用される可能性があるセキュリティの弱点がコード内に残る場合があります。|
|[CA2107:拒否および許可のみの使用を確認します](../code-quality/ca2107-review-deny-and-permit-only-usage.md)|PermitOnly メソッドと CodeAccessPermission.Deny セキュリティ アクションは、.NET Framework のセキュリティについて高度な知識を持っている場合にのみ使用してください。 コードにこのセキュリティ アクションを使用する場合、セキュリティを再確認する必要があります。|
|[CA2108:値型での宣言セキュリティを確認します](../code-quality/ca2108-review-declarative-security-on-value-types.md)|パブリックまたはプロテクトの値型が、データ アクセスまたはリンク確認要求で保護されています。|
|[CA2109:表示するイベント ハンドラーを確認します](../code-quality/ca2109-review-visible-event-handlers.md)|パブリックまたはプロテクトのイベント ハンドラー メソッドが検出されました。 イベント ハンドラー メソッドは、絶対に必要な場合を除き公開しないでください。|
|[CA2111:ポインターは参照可能にすることはできません](../code-quality/ca2111-pointers-should-not-be-visible.md)|ポインターがプライベート、内部、読み取り専用のいずれでもありません。 悪意のあるコードで、ポインターの値が変更される可能性があります。結果的に、メモリの任意の位置にアクセスされたり、アプリケーション エラーやシステム障害の原因になります。|
|[CA2112:セキュリティで保護された型はフィールドを公開してはなりません](../code-quality/ca2112-secured-types-should-not-expose-fields.md)|パブリック型またはプロテクト型に、パブリック フィールドが含まれ、リンク確認要求で保護されています。 リンク確認要求で保護されている型のインスタンスに対するアクセス権がコードにある場合、その型のフィールドにアクセスするためにリンク確認要求に適合する必要はありません。|
|[CA2114:メソッド セキュリティは型のスーパーセットでなければなりません](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md)|メソッドでは、同じアクションについて、メソッド レベルと型レベルの宣言セキュリティの両方を指定することはできません。|
|[CA2115:ネイティブ リソースを使用しているときには GC.KeepAlive を呼び出します](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)|この規則では、アンマネージ コードでまだ使用されているのに、アンマネージ リソースが終了されたときに発生する可能性のあるエラーを検出します。|
|[CA2116:APTCA メソッドは APTCA メソッドのみを呼び出すことができます](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)|APTCA (AllowPartiallyTrustedCallers) 属性が完全に信頼されたアセンブリにあり、部分的に信頼された呼び出し元を許可しない別のアセンブリのコードをアセンブリが実行する場合、セキュリティ上の弱点になります。|
|[CA2117:APTCA 型は APTCA 基本型のみを拡張することができます](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)|APTCA (AllowPartiallyTrustedCallers) 属性が完全に信頼されたアセンブリにあり、アセンブリの型が部分的に信頼された呼び出し元を許可しない型から継承する場合、セキュリティ上の弱点になります。|
|[CA2118:SuppressUnmanagedCodeSecurityAttribute の使用法を確認してください](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md)|COM 相互運用機能またはプラットフォーム呼び出し機能を使用するアンマネージ コードを実行するメンバーの場合、SuppressUnmanagedCodeSecurityAttribute によって、既定のセキュリティ システムの動作が変わります。 この属性は、主にパフォーマンスを向上するために使用されますが、パフォーマンスが向上するとセキュリティ上のリスクも高くなります。|
|[CA2119:プライベート インターフェイスを満たすメソッドをシールします](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md)|継承可能なパブリック型により、internal (Visual Basic では Friend) インターフェイスのオーバーライド可能なメソッド実装が提供されます。 この規則違反を修正するには、アセンブリの外側でメソッドがオーバーライドされないようにします。|
|[CA2120:シリアル化コンストラクターをセキュリティで保護します](../code-quality/ca2120-secure-serialization-constructors.md)|この型には、System.Runtime.Serialization.SerializationInfo オブジェクトおよび System.Runtime.Serialization.StreamingContext オブジェクトを使用するコンストラクター (シリアル化コンストラクターのシグネチャ) があります。 このコンストラクターはセキュリティ チェックで保護されていませんが、型に含まれる標準コンストラクターの 1 つ以上は保護されています。|
|[CA2121:静的コンストラクターはプライベートでなければなりません](../code-quality/ca2121-static-constructors-should-be-private.md)|システムで静的コンストラクターが呼び出されてから、型の最初のインスタンスが作成されるか、静的メンバーが参照されます。 静的コンストラクターがプライベートである場合、システム以外のコードから呼び出すことができます。 コンストラクターで実行される操作によっては、これによって予期しない動作が発生することがあります。|
|[CA2122:リンク要求を含むメソッドを間接的に公開しません](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)|パブリック メンバーまたはプロテクト メンバーはリンク確認要求を含み、セキュリティ チェックを実行しないメンバーから呼び出されています。 リンク確認要求では、直接の呼び出し元のアクセス許可しかチェックされません。|
|[CA2123:オーバーライドのリンク要求はベースと同一でなければなりません](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)|この規則は、メソッドをその基本メソッド (別の型のインターフェイスまたは仮想メソッド) とマッチングし、それぞれについてリンク確認要求を比較します。 この規則に違反すると、悪意のある呼び出し元が、保護されていないメソッドを呼び出すだけで、リンク確認要求を省略できます。|
|[CA2124:脆弱性のある finally 句を外側の try でラップします](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md)|パブリック メソッドまたはプロテクト メソッドに try/finally ブロックが含まれています。 この finally ブロックはセキュリティの状態をリセットすると思われますが、それ自体が finally ブロックで囲まれていません。|
|[CA2126:型のリンク要求には継承要求が必要です](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md)|シールされていないパブリックな型がリンク確認要求によって保護され、オーバーライド可能なメソッドを持っています。 その型またはメソッドが継承確認要求によって保護されていません。|
|[CA2136:メンバーには、透過性注釈の競合があってはならない](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|完全に透過的なアセンブリにクリティカルなコードを含めることはできません。 この規則では、完全に透過的なアセンブリを分析し、型、フィールド、およびメソッドのレベルで注釈の SecurityCritical を検出します。|
|[CA2147:透過コードは、セキュリティ アサートを使用してはならない](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|この規則では、完全に透過的なアセンブリまたは透過的/クリティカル混在のアセンブリ内のすべてのメソッドと型を分析し、宣言的または強制的に使用されている Assert にフラグを設定します。|
|[CA2140:透過的コードは、セキュリティ上重要な項目を参照してはならない](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|SecurityTransparentAttribute でマークされたメソッドが、SecurityCritical とマークされたパブリックでないメンバーを呼び出しています。 この規則では、透過的/クリティカル混在のアセンブリ内のすべてのメソッドと型を分析し、透過的なコードからパブリックでないセキュリティ クリティカルなコードへの呼び出しのうち SecurityTreatAsSafe が適用されていないものにフラグが設定されます。|

|[CA2130:セキュリティ上重要な定数は透過的である必要がある](../code-quality/ca2130-security-critical-constants-should-be-transparent.md)|実行時に検索の必要がない値がコンパイラのインライン定数に設定されているため、定数値に対して透過性は適用されません。 透過的なコードからは定数にアクセスできないとコード レビューアーが考えることがないよう、定数フィールドは透過的セキュリティなフィールドとして定義する必要があります。|
|-----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|[CA2131:セキュリティ上重要な型は型等価性に参加してはならない](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md)|データ型は型の等価性に関与し、型自身、または型のメンバーあるいはフィールドが、SecurityCriticalAttribute 属性でマークされます。 この規則は、すべての重要な型、または型の等価性に関与する重要なメソッドあるいはフィールドが定義されたすべての型に対して適用されます。 こうした型が CLR によって検出されると、CLR による型の読み込みが失敗し、実行時に TypeLoadException が発生します。 通常は、tlbimp やコンパイラによって型の等価性を実装するのではなく、ユーザーが手動で実装した場合に、この規則が適用されます。|
|[CA2132:既定のコンストラクターは、基本型の既定コンストラクターと同程度以上、重要であることが必要](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md)|SecurityCriticalAttribute でマークされている型およびメンバーを Silverlight アプリケーション コードで使用することはできません。 セキュリティが重要な型やメンバーは、.NET Framework for Silverlight クラス ライブラリの信頼されているコードからのみ使用できます。 派生クラスにおけるパブリックな構築または保護された構築の透過性は、基底クラスと同程度以上である必要があるため、アプリケーション内のクラスを、SecurityCritical としてマークされたクラスから派生させることはできません。|
|[CA2133:デリゲートは透過性の整合がとれたメソッドにバインドする必要がある](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md)|この警告は、SecurityCriticalAttribute でマークされているデリゲートを、透過的メソッドまたは SecuritySafeCriticalAttribute でマークされているメソッドにバインドするメソッドに対して適用されます。 この警告は、透過的なデリゲートまたはセーフ クリティカルなデリゲートを、クリティカル メソッドにバインドするメソッドに対しても適用されます。|
|[CA2134:メソッドは、基本メソッドをオーバーライドしている場合、透過性の整合性を保つ必要がある](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md)|この規則は、SecurityCriticalAttribute でマークされているメソッドが、透過的メソッドまたは SecuritySafeCriticalAttribute でマークされているメソッドをオーバーライドするときに適用されます。 また、透過的メソッドまたは SecuritySafeCriticalAttribute が適用されたメソッドが、SecurityCriticalAttribute が適用されたメソッドをオーバーライドした場合も、この規則が適用されます。 この規則は、仮想メソッドをオーバーライドする場合やインターフェイスを実装する場合に適用されます。|
|[CA2135:レベル 2 のアセンブリは LinkDemand を含んではならない](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md)|LinkDemands は、レベル 2 のセキュリティ規則セットでは使用が非推奨とされます。 LinkDemands を使用して Just-In-Time (JIT) コンパイル時にセキュリティを適用するのではなく、メソッド、型、およびフィールドに SecurityCriticalAttribute 属性を設定します。|
|[CA2136:メンバーには、透過性注釈の競合があってはならない](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|透過性属性は、大きいスコープのコード要素から小さいスコープの要素に適用されます。 大きいスコープのコード要素の透過性属性は、最初の要素に含まれているコード要素の透過性属性よりも優先されます。 たとえば、SecurityCriticalAttribute 属性でマークされたクラスに SecuritySafeCriticalAttribute 属性でマークされたメソッドを含めることはできません。|
|[CA2137:透過的メソッドは、検証可能な IL のみを含まなければならない](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md)|メソッドに検証できないコードが含まれているか、メソッドから参照渡しで型が返されます。 この規則は、透過的セキュリティ コードが、検証できない MSIL (Microsoft Intermediate Language) を実行しようとすると適用されます。 ただし、規則には完全な IL 検証ツールは含まれていないため、代わりにヒューリスティックを使用して、ほとんどの MSIL 検証違反が検出されます。|
|[CA2138:透過的メソッドは、SuppressUnmanagedCodeSecurity 属性を持つメソッドを呼び出してはならない](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md)|SuppressUnmanagedCodeSecurityAttribute 属性が適用されたメソッドを、透過的セキュリティ メソッドが呼び出します。|
|[CA2139:透過的メソッドは、HandleProcessCorruptingExceptions 属性を使用してはならない](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md)|この規則は、HandleProcessCorruptedStateExceptionsAttribute 属性を使用してプロセス破損状態例外を処理しようとする、すべての透過的メソッドに対して適用されます。 プロセス破損状態例外は、CLR バージョン 4.0 に分類される例外です (AccessViolationException など)。 HandleProcessCorruptedStateExceptionsAttribute 属性はセキュリティ クリティカルなメソッドでのみ使用できる属性で、透過的メソッドに適用された場合は無視されます。|
|[CA2140:透過的コードは、セキュリティ上重要な項目を参照してはならない](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|SecurityCriticalAttribute 属性が適用されたコード要素は、セキュリティ上重要になります。 透過的なメソッドでセキュリティ上重要な要素を使用することはできません。 透過データ型でセキュリティ上重要な型を使用しようとすると、TypeAccessException、MethodAccessException、FieldAccessException のいずれかの例外が発生します。|
|[CA2141: 透過的メソッドは、LinkDemand を満たしてはならない](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md)|透過的メソッドは、AllowPartiallyTrustedCallersAttribute (APTCA) 属性が適用されていないアセンブリ内のメソッドを呼び出します。また、透過的セキュリティ メソッドは、データ型またはメソッドに対する LinkDemand の要件を満たします。|
|[CA2142:透過的コードは、LinkDemand を使用して保護されてはならない](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)|この規則は、アクセスするために LinkDemands を要求する透過的メソッドに対して適用されます。 透過的セキュリティ コードでは、操作のセキュリティ検証を行うことができないため、アクセス許可を要求できません。|
|[CA2143:透過的メソッドは、セキュリティ確認要求を使用してはならない](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md)|透過的セキュリティ コードでは、操作のセキュリティ検証を行うことができないため、アクセス許可を要求できません。 透過的セキュリティ コードは、フル アクセス要求を使用して、セキュリティ上の決定を行う必要があります。セーフ クリティカルなコードでは、透過的なコードを使用してフル アクセス要求を行うことはできません。|
|[CA2144:透過的コードは、バイト配列からアセンブリを読み込んではならない](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md)|透過的なコードはセキュリティ上重要な操作を実行できないため、透過的なコードのセキュリティ レビューは、クリティカル コードのセキュリティ レビューほど完全ではありません。 バイト配列から読み込まれるアセンブリは透過的なコード内で認識されない場合がありますが、監査を必要とする、クリティカルなコード、またはさらに重要であるセーフ クリティカルなコードがそのバイト配列に含まれる可能性があります。|
|[CA2145:透過的メソッドを SuppressUnmanagedCodeSecurityAttribute で修飾してはならない](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md)|SuppressUnmanagedCodeSecurityAttribute 属性で修飾されたメソッドには、それを呼び出すメソッドに対して適用される暗黙的な LinkDemand があります。 この LinkDemand では、呼び出し元のコードがセキュリティ クリティカルなコードである必要があります。 SuppressUnmanagedCodeSecurity を使用するメソッドに SecurityCriticalAttribute 属性を設定すると、メソッドの呼び出し元に対してこの要件がより明確になります。|
|[CA2146:型は、基本型およびインターフェイスと同程度以上、重要でなければならない](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md)|派生型に透過的セキュリティ属性が設定されていて、この属性が基本型または実装されたインターフェイスほど重要ではない場合に、この規則が適用されます。 クリティカルな基本型から派生したり、クリティカルなインターフェイスを実装したりできるのは、クリティカルなデータ型だけです。また、セーフ クリティカルな基本型から派生したり、セーフ クリティカルなインターフェイスを実装したりできるのは、クリティカルまたはセーフ クリティカルなデータ型だけです。|
|[CA2147:透過コードは、セキュリティ アサートを使用してはならない](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|SecurityTransparentAttribute とマークされたコードには、アサートに必要なアクセス許可が付与されません。|
|[CA2149:透過的メソッドは、ネイティブ コード内に呼び出しを行ってはならない](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md)|この規則は、P/Invoke などを使用してネイティブ コードを直接呼び出すすべての透過的メソッドに対して適用されます。 この規則に違反すると、レベル 2 の透過性モデルで MethodAccessException が発生し、レベル 1 の透過性モデルで UnmanagedCode に対するフル アクセス要求が発生します。|
|[CA2151:クリティカル型のフィールドはセキュリティ クリティカルである必要があります](../code-quality/ca2151-fields-with-critical-types-should-be-security-critical.md)|セキュリティ クリティカルな型を使用するには、型を参照するコードがセキュリティ クリティカルであるか、セキュリティ セーフ クリティカルである必要があります。 これは、参照が間接的である場合にも当てはまります。 そのため、透過的セキュリティまたはセキュリティ セーフ クリティカルなフィールドが存在すると、透過的なコードはこのフィールドにアクセスできないので、紛らわしくなります。|
|[CA5122 P/Invoke 宣言を安全にクリティカルにすることはできません](../code-quality/ca5122-p-invoke-declarations-should-not-be-safe-critical.md)|メソッドは、セキュリティに対する配慮が必要な操作を行うときは SecuritySafeCritical としてマークされますが、透過的なコードによって使用される場合も安全です。 透過的なコードは、P/Invoke を通じてネイティブ コードを直接呼び出すことはありません。 そのため、P/Invoke をセキュリティ セーフ クリティカルとしてマークしても、透過的なコードはそれを呼び出すことができず、セキュリティ分析の際に紛らわしくなります。|
|[CA2153:破損状態例外の処理を回避する](../code-quality/ca2153-avoid-handling-corrupted-state-exceptions.md)|[破損状態例外 (CSE)](https://msdn.microsoft.com/magazine/dd419661.aspx) は、メモリの破損がプロセス内に存在していることを示します。 プロセスをクラッシュさせるのではなくこれらの例外をキャッチすることは、攻撃者が破損したメモリ領域にセキュリティ上の弱点を見出すことができた場合に、セキュリティ上の脆弱性となる可能性があります。|
|[CA3075:安全ではない DTD の処理](../code-quality/ca3075-insecure-dtd-processing.md)|安全ではない DTDProcessing インスタンスを使用する場合、または外部エンティティ ソースを参照する場合、パーサーは信頼されていない入力を受け入れ、攻撃者に機密情報を漏えいしてしまう可能性があります。|
|[CA3076:安全ではない XSLT スクリプトの実行](../code-quality/ca3076-insecure-xslt-script-execution.md)|.NET アプリケーションで XSLT (Extensible Stylesheet Language Transformation) を安全ではない方法で実行すると、攻撃者に機密情報を漏えいする可能性のある、信頼されていない URI 参照がプロセッサにより解決されるおそれがあります。そのことは、サービス拒否攻撃やクロスサイト攻撃につながります。|
|[CA3077:API のデザイン、XML ドキュメント、および XML テキスト リーダーでの安全ではない処理](../code-quality/ca3077-insecure-processing-in-api-design-xml-document-and-xml-text-reader.md)|XMLDocument と XMLTextReader から派生する API をデザインする場合、DtdProcessing にご注意ください。  外部エンティティ ソースを参照または解決したり、XML に安全ではない値を設定したりする場合に、安全ではない DTDProcessing インスタンスを使用すると、情報漏えいにつながる可能性があります。|
