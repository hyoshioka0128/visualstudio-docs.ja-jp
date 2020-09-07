---
title: マネージド コードの "セキュリティ規則" 規則セット
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 564aeac6-03fa-41b0-b655-88179f0ab01b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: c7ce330a8a2994f827234aae8b8db416da016b29
ms.sourcegitcommit: 5caad925ca0b5d136416144a279e984836d8f28c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "89509875"
---
# <a name="security-rules-rule-set-for-managed-code"></a>マネージド コードの "セキュリティ規則" 規則セット

レガシコード分析用の Microsoft セキュリティ規則セットを使用して、報告される潜在的なセキュリティ問題の数を最大化します。

|ルール|説明|
|----------|-----------------|
|[CA2100](../code-quality/ca2100.md)|SQL クエリのセキュリティ脆弱性を確認|
|[CA2102](../code-quality/ca2102.md)|汎用ハンドラーの CLSCompliant でない例外をキャッチします|
|[CA2103](../code-quality/ca2103.md)|命令型のセキュリティを確認します|
|[CA2104](../code-quality/ca2104.md)|読み取り専用の変更可能な参照型を宣言しません|
|[CA2105](../code-quality/ca2105.md)|配列フィールドを読み取り専用にすることはできません|
|[CA2106](../code-quality/ca2106.md)|アサートをセキュリティで保護します|
|[CA2107](../code-quality/ca2107.md)|拒否および許可のみの使用を確認します|
|[CA2108](../code-quality/ca2108.md)|値型での宣言セキュリティを確認します|
|[CA2109](../code-quality/ca2109.md)|表示するイベント ハンドラーを確認します|
|[CA2111](../code-quality/ca2111.md)|ポインターは参照可能にすることはできません|
|[CA2112](../code-quality/ca2112.md)|セキュリティで保護された型はフィールドを公開してはなりません|
|[CA2114](../code-quality/ca2114.md)|メソッド セキュリティは型のスーパーセットでなければなりません|
|[CA2115](../code-quality/ca2115.md)|ネイティブ リソースを使用しているときには GC.KeepAlive を呼び出します|
|[CA2116](../code-quality/ca2116.md)|APTCA メソッドは APTCA メソッドのみを呼び出すことができます|
|[CA2117](../code-quality/ca2117.md)|APTCA 型は APTCA 基本型のみを拡張することができます|
|[CA2118](../code-quality/ca2118.md)|SuppressUnmanagedCodeSecurityAttribute の使用法を確認してください|
|[CA2119](../code-quality/ca2119.md)|プライベート インターフェイスを満たすメソッドをシールします|
|[CA2120](../code-quality/ca2120.md)|シリアル化コンストラクターをセキュリティで保護します|
|[CA2121](../code-quality/ca2121.md)|静的コンストラクターはプライベートでなければなりません|
|[CA2122](../code-quality/ca2122.md)|リンク要求を含むメソッドを間接的に公開しません|
|[CA2123](../code-quality/ca2123.md)|オーバーライドのリンク要求はベースと同一でなければなりません|
|[CA2124](../code-quality/ca2124.md)|脆弱性のある finally 句を外側の try でラップします|
|[CA2126](../code-quality/ca2126.md)|型のリンク要求には継承要求が必要です|
|[CA2130](../code-quality/ca2130.md)|セキュリティ上重要な定数は透過的である必要がある|
|[CA2131](../code-quality/ca2131.md)|セキュリティ上重要な型は型等価性に参加してはならない|
|[CA2132](../code-quality/ca2132.md)|既定のコンストラクターは、基本型の既定コンストラクターと同程度以上、重要であることが必要|
|[CA2133](../code-quality/ca2133.md)|デリゲートは透過性の整合がとれたメソッドにバインドする必要がある|
|[CA2134](../code-quality/ca2134.md)|メソッドは、基本メソッドをオーバーライドしている場合、透過性の整合性を保つ必要がある|
|[CA2135](../code-quality/ca2135.md)|レベル 2 のアセンブリは LinkDemand を含んではならない|
|[CA2136](../code-quality/ca2136.md)|メンバーには、透過性注釈の競合があってはならない|
|[CA2137](../code-quality/ca2137.md)|透過的メソッドは、検証可能な IL のみを含まなければならない|
|[CA2138](../code-quality/ca2138.md)|透過的メソッドは、SuppressUnmanagedCodeSecurity 属性を持つメソッドを呼び出してはならない|
|[CA2139](../code-quality/ca2139.md)|透過的メソッドは、HandleProcessCorruptingExceptions 属性を使用してはならない|
|[CA2140](../code-quality/ca2140.md)|透過的コードは、セキュリティ上重要な項目を参照してはならない|
|[CA2141](../code-quality/ca2141.md)|透過的メソッドは Linkdemand を満たしてはならない|
|[CA2142](../code-quality/ca2142.md)|透過的コードは、LinkDemand を使用して保護されてはならない|
|[CA2143](../code-quality/ca2143.md)|透過的メソッドは、セキュリティ確認要求を使用してはならない|
|[CA2144](../code-quality/ca2144.md)|透過的コードは、バイト配列からアセンブリを読み込んではならない|
|[CA2145](../code-quality/ca2145.md)|透過的メソッドを SuppressUnmanagedCodeSecurityAttribute で修飾してはならない|
|[CA2146](../code-quality/ca2146.md)|型は、基本型およびインターフェイスと同程度以上、重要でなければならない|
|[CA2147](../code-quality/ca2147.md)|透過コードは、セキュリティ アサートを使用してはならない|
|[CA2149](../code-quality/ca2149.md)|透過的メソッドは、ネイティブ コード内に呼び出しを行ってはならない|
|[CA2210](../code-quality/ca2210.md)|アセンブリには有効な厳密な名前が必要です|
|[CA2300](ca2300.md)|安全ではないデシリアライザー BinaryFormatter を使用しないでください|
|[CA2301](ca2301.md)|最初に BinaryFormatter.Binder を設定しないで BinaryFormatter.Deserialize を呼び出さないでください|
|[CA2302](ca2302.md)|BinaryFormatter.Deserialize を呼び出す前に BinaryFormatter.Binder が設定されていることを確認します|
|[CA2305](ca2305.md)|安全ではないデシリアライザー LosFormatter を使用しないでください|
|[CA2310](ca2310.md)|安全ではないデシリアライザー NetDataContractSerializer を使用しないでください|
|[CA2311](ca2311.md)|最初に NetDataContractSerializer.Binder を設定しないで逆シリアル化しないでください|
|[CA2312](ca2312.md)|NetDataContractSerializer.Binder を設定してから逆シリアル化してください|
|[CA2315](ca2315.md)|安全ではないデシリアライザー ObjectStateFormatter を使用しないでください|
|[CA2321](ca2321.md)|SimpleTypeResolver を使って JavaScriptSerializer で逆シリアル化しないでください|
|[CA2322](ca2322.md)|逆シリアル化する前に JavaScriptSerializer が SimpleTypeResolver によって初期化されていないことを確認してください|
|[CA3001](../code-quality/ca3001.md)|SQL インジェクションの脆弱性のコード レビュー|
|[CA3002](../code-quality/ca3002.md)|XSS の脆弱性のコード レビュー|
|[CA3003](../code-quality/ca3003.md)|ファイル パス インジェクションの脆弱性のコード レビュー|
|[CA3004](../code-quality/ca3004.md)|情報漏えいの脆弱性のコード レビュー|
|[CA3005](../code-quality/ca3005.md)|LDAP インジェクションの脆弱性のコード レビュー|
|[CA3006](../code-quality/ca3006.md)|プロセス コマンド インジェクションの脆弱性のコード レビュー|
|[CA3007](../code-quality/ca3007.md)|オープン リダイレクトの脆弱性のコード レビュー|
|[CA3008](../code-quality/ca3008.md)|XPath インジェクションの脆弱性のコード レビュー|
|[CA3009](../code-quality/ca3009.md)|XML インジェクションの脆弱性のコード レビュー|
|[CA3010](../code-quality/ca3010.md)|XAML インジェクションの脆弱性のコード レビュー|
|[CA3011](../code-quality/ca3011.md)|DLL インジェクションの脆弱性のコード レビュー|
|[CA3012](../code-quality/ca3012.md)|RegEx インジェクションの脆弱性のコード レビュー|
|[CA5358](../code-quality/ca5358.md)|安全ではない暗号モードを使用しないでください|
|[CA5403](../code-quality/ca5403.md)|証明書をハードコーディングしない|