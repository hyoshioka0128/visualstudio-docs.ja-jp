---
title: 'CA1063: IDisposable を正しく実装します |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ImplementIDisposableCorrectly
- CA1063
helpviewer_keywords:
- CA1063
- ImplementIDisposableCorrectly
ms.assetid: 12afb1ea-3a17-4a3f-a1f0-fcdb853e2359
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 04691d2344b232906676180122ad67fff5405891
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539361"
---
# <a name="ca1063-implement-idisposable-correctly"></a>CA1063:IDisposable を正しく実装します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|ImplementIDisposableCorrectly|
|CheckId|CA1063|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 `IDisposable`が正しく実装されていません。 この問題の原因をいくつか次に示します。

- IDisposable はクラスで再実装されます。

- Finalize は再オーバーライドされます。

- Dispose はオーバーライドされます。

- Dispose () は、public、sealed、または named Dispose ではありません。

- Dispose (bool) は、protected、virtual、または封印されていません。

- シールされていない型では、Dispose () は Dispose (true) を呼び出す必要があります。

- シールされていない型の場合、Finalize 実装は Dispose (bool) または case クラスのファイナライザーのいずれかまたは両方を呼び出しません。

  これらのパターンのいずれかに違反すると、この警告がトリガーされます。

  すべての封印されていないルート IDisposable 型は、独自の protected virtual void Dispose (bool) メソッドを提供する必要があります。 Dispose () は dispose (true) を呼び出し、Finalize は Dispose (false) を呼び出す必要があります。 封印されていないルート IDisposable 型を作成する場合は、Dispose (bool) を定義して呼び出す必要があります。 詳細については、.NET Framework のドキュメントの「[フレームワークのデザインガイドライン](https://msdn.microsoft.com/library/5fbcaf4f-ea2a-4d20-b0d6-e61dee202b4b)」の「[アンマネージリソースのクリーンアップ](https://msdn.microsoft.com/library/a17b0066-71c2-4ba4-9822-8e19332fc213)」を参照してください。

## <a name="rule-description"></a>ルールの説明
 すべての IDisposable 型は、Dispose パターンを適切に実装する必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 コードを調べて、この違反を修正する次の解決策を特定します。

- によって実装されたインターフェイスの一覧から IDisposable を削除 {0} し、代わりに基底クラスの Dispose の実装をオーバーライドします。

- 型からファイナライザーを削除し {0} 、Dispose (bool disposing) をオーバーライドし、' disposing ' が false であるコードパスに終了ロジックを配置します。

- を削除し {0} 、dispose (bool disposing) をオーバーライドし、' disposing ' が true であるコードパスに dispose ロジックを配置します。

- {0}が public および sealed として宣言されていることを確認します。

- 名前 {0} を ' Dispose ' に変更し、public および sealed として宣言されていることを確認します。

- {0}が protected、virtual、および未封印として宣言されていることを確認します。

- {0}Dispose (true) を呼び出すようにを変更し、GC を呼び出します。現在のオブジェクトインスタンス (では ' this ' または ' Me ') に Gc.suppressfinalize し [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] てから、を返します。

- を変更して、 {0} Dispose (false) を呼び出し、を返します。

- 封印されていないルート IDisposable クラスを作成する場合は、IDisposable の実装が、このセクションで既に説明したパターンに従っていることを確認してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="pseudo-code-example"></a>擬似コードの例
 次の擬似コードは、マネージリソースとネイティブリソースを使用するクラスに Dispose (bool) を実装する方法の一般的な例を示しています。

```
public class Resource : IDisposable
{
    private IntPtr nativeResource = Marshal.AllocHGlobal(100);
    private AnotherResource managedResource = new AnotherResource();

// Dispose() calls Dispose(true)
    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }
    // NOTE: Leave out the finalizer altogether if this class doesn't
    // own unmanaged resources itself, but leave the other methods
    // exactly as they are.
    ~Resource()
    {
        // Finalizer calls Dispose(false)
        Dispose(false);
    }
    // The bulk of the clean-up code is implemented in Dispose(bool)
    protected virtual void Dispose(bool disposing)
    {
        if (disposing)
        {
            // free managed resources
            if (managedResource != null)
            {
                managedResource.Dispose();
                managedResource = null;
            }
        }
        // free native resources if there are any.
        if (nativeResource != IntPtr.Zero)
        {
            Marshal.FreeHGlobal(nativeResource);
            nativeResource = IntPtr.Zero;
        }
    }
}
```
