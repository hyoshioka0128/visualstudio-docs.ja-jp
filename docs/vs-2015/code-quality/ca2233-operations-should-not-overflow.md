---
title: 'CA2233: 操作をオーバーフローさせることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperationsShouldNotOverflow
- CA2233
helpviewer_keywords:
- OperationsShouldNotOverflow
- CA2233
ms.assetid: 3a2b06ba-6d1b-4666-9eaf-e053ef47ffaa
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: eff09fb8f4423560c4681c94507d909f5864c69e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545237"
---
# <a name="ca2233-operations-should-not-overflow"></a>CA2233:操作はオーバーフローできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|OperationsShouldNotOverflow|
|CheckId|CA2233|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 メソッドは算術演算を実行し、オーバーフローを防ぐために、オペランドを事前に検証しません。

## <a name="rule-description"></a>ルールの説明
 演算の結果が関連するデータ型の有効な値の範囲外であることを確認するために、最初にオペランドを検証せずに算術演算を実行することはできません。 算術オーバーフローでは、実行コンテキストおよび関連するデータ型に応じて、 <xref:System.OverflowException?displayProperty=fullName> または結果の最上位ビットが破棄される可能性があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、操作を実行する前にオペランドを検証します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 オペランドの値によって算術演算のオーバーフローが発生しない場合は、この規則による警告を抑制しても安全です。

## <a name="example-of-a-violation"></a>違反の例

### <a name="description"></a>説明
 次の例のメソッドは、この規則に違反する整数を操作します。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] このを起動するには、[整数オーバーフローを **削除** する] オプションを無効にする必要があります。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Usage.OperationOverflow#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/cs/FxCop.Usage.OperationOverflow.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflow#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/vb/FxCop.Usage.OperationOverflow.vb#1)]

### <a name="comments"></a>コメント
 この例のメソッドが渡された場合 <xref:System.Int32.MinValue?displayProperty=fullName> 、操作はアンダーフローします。 これにより、結果の最上位ビットが破棄されます。 この状況を次のコードに示します。

 [C#]

```
public static void Main()
{
    int value = int.MinValue;    // int.MinValue is -2147483648
    value = Calculator.Decrement(value);
    Console.WriteLine(value);
}
```

 VISUAL

```
Public Shared Sub Main()
    Dim value = Integer.MinValue    ' Integer.MinValue is -2147483648
    value = Calculator.Decrement(value)
    Console.WriteLine(value)
End Sub
```

### <a name="output"></a>出力

```
2147483647
```

## <a name="fix-with-input-parameter-validation"></a>入力パラメーターの検証を使用した修正

### <a name="description"></a>説明
 次の例では、入力の値を検証することによって、以前の違反を修正します。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Usage.OperationOverflowFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/cs/FxCop.Usage.OperationOverflowFixed.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflowFixed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/vb/FxCop.Usage.OperationOverflowFixed.vb#1)]

## <a name="fix-with-a-checked-block"></a>チェックされたブロックで修正

### <a name="description"></a>説明
 次の例では、チェックされたブロックで操作をラップすることによって、前の違反を修正します。 操作によってオーバーフローが発生した場合は、が <xref:System.OverflowException?displayProperty=fullName> スローされます。

 では、チェックされたブロックはサポートされていないことに注意 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] してください。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Usage.OperationOverflowChecked#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowChecked/cs/FxCop.Usage.OperationOverflowChecked.cs#1)]

## <a name="turn-on-checked-arithmetic-overflowunderflow"></a>チェックされた算術オーバーフロー/アンダーフローをオンにする
 C# でチェックされた算術オーバーフローまたはアンダーフローをオンにすると、すべての整数演算を checked ブロックにラップすることと同じ結果になります。

 **C でチェックされた算術オーバーフローまたはアンダーフローをオンにするには#**

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[**プロパティ**] を選択します。

2. **[ビルド]** タブを選択してから **[詳細設定]** をクリックします。

3. [ **算術オーバーフローまたはアンダーフローのチェック** ] を選択し、[ **OK**] をクリックします。

## <a name="see-also"></a>参照
 <xref:System.OverflowException?displayProperty=fullName>[C# 演算子](https://msdn.microsoft.com/library/0301e31f-22ad-49af-ac3c-d5eae7f0ac43)[のチェックとオフ](https://msdn.microsoft.com/library/a84bc877-2c7f-4396-8735-1ce97c42f35e)
