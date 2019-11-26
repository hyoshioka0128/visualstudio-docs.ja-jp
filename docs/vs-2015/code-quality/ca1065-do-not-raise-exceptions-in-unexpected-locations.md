---
title: 'CA1065: 予期しない場所で例外を発生させない |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1065
- DoNotRaiseExceptionsInUnexpectedLocations
helpviewer_keywords:
- DoNotRaiseExceptionsInUnexpectedLocations
- CA1065
ms.assetid: 4e1bade4-4ca2-4219-abc3-c7b2d741e157
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 439c6b5fc30be2e76eb6c0b6a44b1ec5226633b1
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295949"
---
# <a name="ca1065-do-not-raise-exceptions-in-unexpected-locations"></a>CA1065: 予期しない場所に例外を発生させません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotRaiseExceptionsInUnexpectedLocations|
|CheckId|CA1065|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 例外をスローしないはずのメソッドが例外をスローします。

## <a name="rule-description"></a>規則の説明
 例外をスローすることが想定されていないメソッドは、次のように分類できます。

- Property Get メソッド

- イベントのアクセサー メソッド

- Equals メソッド

- GetHashCode メソッド

- ToString メソッド

- 静的コンストラクター

- ファイナライザー

- Dispose メソッド

- 等値演算子

- 暗黙的なキャスト演算子

  以下のセクションでは、これらのメソッドの種類について説明します。

### <a name="property-get-methods"></a>Property Get メソッド
 プロパティは、基本的にはスマートフィールドです。 そのため、これらはできるだけフィールドのように動作する必要があります。 フィールドは例外をスローせず、どちらのプロパティでもありません。 例外をスローするプロパティがある場合は、それをメソッドにすることを検討してください。

 次の例外は、プロパティの get メソッドからスローすることができます。

- <xref:System.InvalidOperationException?displayProperty=fullName> とすべての派生 (<xref:System.ObjectDisposedException?displayProperty=fullName>を含む)

- <xref:System.NotSupportedException?displayProperty=fullName> とすべての派生物

- <xref:System.ArgumentException?displayProperty=fullName> (インデックス付きの get からのみ)

- <xref:System.Collections.Generic.KeyNotFoundException> (インデックス付きの get からのみ)

### <a name="event-accessor-methods"></a>イベントのアクセサー メソッド
 イベントアクセサーは、例外をスローしない単純な操作である必要があります。 イベントハンドラーを追加または削除しようとすると、例外をスローしないようにする必要があります。

 イベントには、次の例外がスローされます。

- <xref:System.InvalidOperationException?displayProperty=fullName> とすべての派生 (<xref:System.ObjectDisposedException?displayProperty=fullName>を含む)

- <xref:System.NotSupportedException?displayProperty=fullName> とすべての派生物

- <xref:System.ArgumentException> と派生

### <a name="equals-methods"></a>Equals メソッド
 次の**Equals**メソッドは例外をスローしません。

- <xref:System.Object.Equals%2A?displayProperty=fullName>

- [M:IEquatable.Equals](https://go.microsoft.com/fwlink/?LinkId=113472)

  **Equals**メソッドは、例外をスローするのではなく、`true` または `false` を返す必要があります。 たとえば、Equals に2つの一致しない型が渡された場合、<xref:System.ArgumentException>をスローするのではなく、`false` を返すだけです。

### <a name="gethashcode-methods"></a>GetHashCode メソッド
 次の**GetHashCode**メソッドは、通常、例外をスローしません。

- <xref:System.Object.GetHashCode%2A>

- [M:IEqualityComparer.GetHashCode (T)](https://go.microsoft.com/fwlink/?LinkId=113477)

  **GetHashCode**は常に値を返す必要があります。 それ以外の場合、ハッシュテーブル内の項目が失われる可能性があります。

  引数を受け取る**GetHashCode**のバージョンは、<xref:System.ArgumentException>をスローすることがあります。 ただし、**オブジェクト GetHashCode**は例外をスローすることはできません。

### <a name="tostring-methods"></a>ToString メソッド
 デバッガーでは、オブジェクトに関する情報を文字列形式で表示するために <xref:System.Object.ToString%2A?displayProperty=fullName> を使用します。 したがって、 **ToString**はオブジェクトの状態を変更する必要がなく、例外をスローしないようにする必要があります。

### <a name="static-constructors"></a>静的コンストラクター
 静的コンストラクターから例外をスローすると、現在のアプリケーションドメインでその型を使用できなくなります。 静的コンストラクターから例外をスローするための十分な理由 (セキュリティの問題など) が必要です。

### <a name="finalizers"></a>ファイナライザー
 ファイナライザーから例外をスローすると、CLR が高速に処理され、プロセスが破棄されます。 したがって、ファイナライザーで例外をスローすることは常に避ける必要があります。

### <a name="dispose-methods"></a>Dispose メソッド
 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> メソッドでは、例外をスローすることはできません。 Dispose は、`finally` 句でクリーンアップロジックの一部として呼び出されることがよくあります。 したがって、Dispose から明示的に例外をスローすると、ユーザーは `finally` 句内に例外処理を追加するように強制されます。

 **Dispose (false)** コードパスは、ほとんどの場合、ファイナライザーから呼び出されるため、例外をスローすることはできません。

### <a name="equality-operators--"></a>等値演算子 (= =、! =)
 Equals メソッドと同様に、等値演算子は `true` または `false` のいずれかを返す必要があり、例外をスローしません。

### <a name="implicit-cast-operators"></a>暗黙的なキャスト演算子
 ユーザーは、暗黙的なキャスト演算子が呼び出されたことを認識しないことがよくあるため、暗黙的なキャスト演算子によってスローされる例外は完全に予期しないものになります。 したがって、暗黙的なキャスト演算子からは例外をスローしません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 プロパティの getter の場合は、例外をスローする必要がなくなったロジックを変更するか、プロパティをメソッドに変更します。

 上記の他のすべてのメソッド型については、例外をスローする必要がなくなったロジックを変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 スローされた例外ではなく例外宣言によって違反が発生した場合は、この規則からの警告を抑制することが安全です。

## <a name="related-rules"></a>関連規則
 [CA2219: exception 句に例外を発生させないでください](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)

## <a name="see-also"></a>関連項目
 [デザインの警告](../code-quality/design-warnings.md)
