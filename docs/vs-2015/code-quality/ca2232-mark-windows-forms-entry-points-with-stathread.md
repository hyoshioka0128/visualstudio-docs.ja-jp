---
title: 'CA2232: Windows フォームのエントリポイントを、すべてのスレッドでマークします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkWindowsFormsEntryPointsWithStaThread
- CA2232
helpviewer_keywords:
- CA2232
- MarkWindowsFormsEntryPointsWithStaThread
ms.assetid: a3c95130-8e7f-4419-9fcd-b67d077e8efb
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 42bb554f8e57c036d41a89fdc2657a25ecc74e20
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540284"
---
# <a name="ca2232-mark-windows-forms-entry-points-with-stathread"></a>CA2232:Windows フォームのエントリ ポイントを STAThread に設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|MarkWindowsFormsEntryPointsWithStaThread|
|CheckId|CA2232|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 アセンブリが <xref:System.Windows.Forms> 名前空間を参照し、そのエントリポイントが属性でマークされていません <xref:System.STAThreadAttribute?displayProperty=fullName> 。

## <a name="rule-description"></a>ルールの説明
 <xref:System.STAThreadAttribute>アプリケーションの COM スレッドモデルがシングルスレッドアパートメントであることを示します。 この属性は、Windows フォームを使用するすべてのアプリケーションのエントリ ポイントに指定する必要があります。省略すると、Windows コンポーネントが正常に機能しないことがあります。 属性が存在しない場合、アプリケーションは、Windows フォームでサポートされていないマルチスレッドアパートメントモデルを使用します。

> [!NOTE]
> [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]アプリケーションフレームワークを使用するプロジェクトでは、 **Main**メソッドをスレッドでマークする必要はありません。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]コンパイラは自動的にこれを行います。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.STAThreadAttribute> エントリポイントに属性を追加します。 <xref:System.MTAThreadAttribute?displayProperty=fullName>属性が存在する場合は、削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 <xref:System.STAThreadAttribute>属性が不要でサポートされていない .NET Compact Framework を開発している場合は、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、の正しい使用方法を示して <xref:System.STAThreadAttribute> います。

 [!code-csharp[FxCop.Usage.StaThread#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.StaThread/cs/FxCop.Usage.StaThread.cs#1)]
 [!code-vb[FxCop.Usage.StaThread#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.StaThread/vb/FxCop.Usage.StaThread.vb#1)]
