---
title: 'CA2202: オブジェクトを複数回破棄することはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2202
- Do not dispose objects multiple times
- DoNotDisposeObjectsMultipleTimes
helpviewer_keywords:
- CA2202
ms.assetid: fa85349a-cf1e-42c8-a86b-eacae1f8bd96
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 31bf7fe33aa59c3a713d2da81ddbd11ed6899723
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546290"
---
# <a name="ca2202-do-not-dispose-objects-multiple-times"></a>CA2202:オブジェクトを複数回破棄しない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotDisposeObjectsMultipleTimes|
|CheckId|CA2202|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 メソッドの実装には、同じオブジェクトに対して、 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> または一部の型の Close () メソッドなどの Dispose と同等のの呼び出しを発生させる可能性があるコードパスが含まれています。

## <a name="rule-description"></a>ルールの説明
 正しく実装されたメソッドは、 <xref:System.IDisposable.Dispose%2A> 例外をスローせずに複数回呼び出すことができます。 ただし、これは保証されていないため、を生成しないようにするには、オブジェクトでを複数回 <xref:System.ObjectDisposedException?displayProperty=fullName> 呼び出す必要があり <xref:System.IDisposable.Dispose%2A> ます。

## <a name="related-rules"></a>関連規則
 [CA2000:スコープを失う前にオブジェクトを破棄](../code-quality/ca2000-dispose-objects-before-losing-scope.md)

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、コードパスに関係なく、オブジェクトに対して1回だけ呼び出されるように実装を変更し <xref:System.IDisposable.Dispose%2A> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 <xref:System.IDisposable.Dispose%2A>オブジェクトが安全に複数回呼び出し可能であることがわかっている場合でも、実装は将来変更される可能性があります。

## <a name="example"></a>例
 入れ子 `using` になっ `Using` たステートメント (Visual Basic) では、CA2202 警告の違反が発生する可能性があります。 入れ子になった内側のステートメントの IDisposable リソースに `using` 外側のステートメントのリソースが含まれている場合 `using` 、 `Dispose` 入れ子になったリソースのメソッドは、含まれているリソースを解放します。 このような状況が発生すると、 `Dispose` 外側のステートメントのメソッドは、 `using` そのリソースをもう一度破棄しようとします。

 次の例では、 <xref:System.IO.Stream> 外部の using ステートメントで作成されたオブジェクトが、オブジェクトを含むオブジェクトの Dispose メソッド内の inner using ステートメントの最後に解放され <xref:System.IO.StreamWriter> `stream` ます。 外側のステートメントの最後で `using` `stream` は、オブジェクトが2回解放されます。 2番目のリリースは、CA2202 の違反です。

```
using (Stream stream = new FileStream("file.txt", FileMode.OpenOrCreate))
{
    using (StreamWriter writer = new StreamWriter(stream))
    {
        // Use the writer object...
    }
}
```

## <a name="example"></a>例
 この問題を解決するには、 `try` / `finally` 外側のステートメントの代わりにブロックを使用し `using` ます。 ブロックで、 `finally` リソースが null でないことを確認し `stream` ます。

```
Stream stream = null;
try
{
    stream = new FileStream("file.txt", FileMode.OpenOrCreate);
    using (StreamWriter writer = new StreamWriter(stream))
    {
        stream = null;
        // Use the writer object...
    }
}
finally
{
    if(stream != null)
        stream.Dispose();
}
```

## <a name="see-also"></a>関連項目
 <xref:System.IDisposable?displayProperty=fullName> [Dispose パターン](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
