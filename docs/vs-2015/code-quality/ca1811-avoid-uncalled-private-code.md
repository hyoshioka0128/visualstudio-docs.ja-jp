---
title: 'CA1811: 呼び出されるプライベートコードを回避する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUncalledPrivateCode
- CA1811
helpviewer_keywords:
- CA1811
- AvoidUncalledPrivateCode
ms.assetid: aadbba74-7821-475f-8980-34d17c0a0a8b
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 223b2ff9aa25ddd94a3c62eb9e641127a1cace4e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543820"
---
# <a name="ca1811-avoid-uncalled-private-code"></a>CA1811:呼び出されていないプライベート コードを使用しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AvoidUncalledPrivateCode|
|CheckId|CA1811|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 プライベートまたは内部 (アセンブリレベル) のメンバーは、アセンブリ内の呼び出し元を持っていません。共通言語ランタイムによって呼び出されず、デリゲートによって呼び出されません。 次のメンバーは、この規則によってチェックされません。

- 明示的なインターフェイスメンバー。

- 静的コンストラクター。

- シリアル化コンストラクター。

- またはでマークされたメソッド <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> 。

- オーバーライドされるメンバー。

## <a name="rule-description"></a>ルールの説明
 このルールは、ルールロジックで現在識別されていないエントリポイントが発生した場合に、偽陽性を報告できます。 また、コンパイラが呼び出し不可能なコードをアセンブリに出力する場合もあります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、呼び出し不可能なコードを削除するか、それを呼び出すコードを追加します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制するのは安全です。

## <a name="related-rules"></a>関連規則
 [CA1812:インスタンス化されていない内部クラスを使用しません](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1801:使用されていないパラメーターの確認](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804:使用されていないローカルを削除します](../code-quality/ca1804-remove-unused-locals.md)
