---
title: 'CA1300: MessageBoxOptions | を指定します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyMessageBoxOptions
- CA1300
helpviewer_keywords:
- SpecifyMessageBoxOptions
- CA1300
ms.assetid: 9357a724-026e-4a3d-a03a-f14635064ec6
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: af0017a7ee6918a80a93ca90c7cf3de78885d61f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85539192"
---
# <a name="ca1300-specify-messageboxoptions"></a>CA1300:MessageBoxOption を指定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|SpecifyMessageBoxOptions|
|CheckId|CA1300|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドは、 <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> 引数を受け取らないメソッドのオーバーロードを呼び出し <xref:System.Windows.Forms.MessageBoxOptions?displayProperty=fullName> ます。

## <a name="rule-description"></a>ルールの説明
 右から左への読み取り順序を使用するカルチャに対してメッセージボックスを正しく表示するには、 <xref:System.Windows.Forms.MessageBoxOptions> <xref:System.Windows.Forms.MessageBoxOptions> 列挙体のおよびメンバーを <xref:System.Windows.Forms.MessageBoxOptions> メソッドに渡す必要があり <xref:System.Windows.Forms.MessageBox.Show%2A> ます。 <xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=fullName>格納しているコントロールのプロパティを調べて、右から左への読み取り順序を使用するかどうかを判断します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.Windows.Forms.MessageBox.Show%2A> 引数を受け取るメソッドのオーバーロードを呼び出し <xref:System.Windows.Forms.MessageBoxOptions> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 右から左への読み取り順序を使用するカルチャに対してコードライブラリがローカライズされない場合は、この規則による警告を抑制しても安全です。

## <a name="example"></a>例
 次の例は、カルチャの読み取り順序に適したオプションを持つメッセージボックスを表示するメソッドを示しています。 例をビルドするには、表示されていないリソースファイルが必要です。 例のコメントに従って、リソースファイルを使用せずに例をビルドし、右から左へ記述する機能をテストします。

 [!code-csharp[FxCop.Globalization.SpecifyMBOptions#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/cs/FxCop.Globalization.SpecifyMBOptions.cs#1)]
 [!code-vb[FxCop.Globalization.SpecifyMBOptions#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/vb/FxCop.Globalization.SpecifyMBOptions.vb#1)]

## <a name="see-also"></a>参照
 <xref:System.Resources.ResourceManager?displayProperty=fullName> [デスクトップ アプリケーションのリソース](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
