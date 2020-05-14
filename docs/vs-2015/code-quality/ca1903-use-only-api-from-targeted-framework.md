---
title: 'CA1903: 対象となるフレームワークから API のみを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseOnlyAPIFromTargetedFramework
- CA1903
helpviewer_keywords:
- UseOnlyApiFromTargetedFramework
- CA1903
ms.assetid: efdb5cc7-bbd8-4fa7-9fff-02b91e59350e
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fa0d771d99ac8e7a4f4091db90a607cce970bc38
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75917830"
---
# <a name="ca1903-use-only-api-from-targeted-framework"></a>CA1903: 対象のフレームワークから API のみを使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [CA1903: ターゲットフレームワークから API のみを使用する](/visualstudio/code-quality/ca1903-use-only-api-from-targeted-framework)」を参照してください。

|||
|-|-|
|TypeName|UseOnlyApiFromTargetedFramework|
|CheckId|CA1903|
|[カテゴリ]|Microsoft. 移植性|
|互換性に影響する変更点|中断-外部から参照できるメンバーまたは型のシグネチャに対して発生した場合。<br /><br /> 非中断-メソッドの本体で発生した場合。|

## <a name="cause"></a>原因
 メンバーまたは型が、プロジェクトの対象となるフレームワークに含まれていなかった Service Pack で導入されたメンバーまたは型を使用しています。

## <a name="rule-description"></a>規則の説明
 新しいメンバーと型は .NET Framework 2.0 Service Pack 1 および2、.NET Framework 3.0 Service Pack 1 と2、および .NET Framework 3.5 Service Pack 1 に含まれていました。 .NET Framework のメジャーバージョンを対象とするプロジェクトでは、これらの新しい Api に対する依存関係を意図せずに取得できます。 この依存関係を防ぐため、この規則は、プロジェクトのターゲットフレームワークに既定で含まれていない新しいメンバーおよび型の使用時に適用されます。

 **ターゲットフレームワークと Service Pack の依存関係**

|||
|-|-|
|ターゲットフレームワークが|で導入されたメンバーの使用時に発生します|
|.NET Framework 2.0|.NET Framework 2.0 SP1、.NET Framework 2.0 SP2|
|.NET Framework 3.0|.NET Framework 2.0 SP1、.NET Framework 2.0 SP2、.NET Framework 3.0 SP1、.NET Framework 3.0 SP2|
|.NET Framework 3.5|.NET Framework 3.5 SP1|
|.NET Framework 4|N/A|

 プロジェクトのターゲットフレームワークを変更するには、「[特定の .NET Framework バージョンをターゲット](../ide/targeting-a-specific-dotnet-framework-version.md)にする」を参照してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 Service Pack の依存関係を削除するには、新しいメンバーまたは型のすべての使用を削除します。 これが意図的な依存関係である場合は、警告を抑制するか、この規則を無効にします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 指定された Service Pack に意図的に依存していない場合は、この規則による警告を抑制しないでください。 このような状況では、この Service Pack インストールされていないシステムでは、アプリケーションの実行が失敗する可能性があります。 意図的な依存関係である場合は、警告を抑制するか、この規則を無効にします。

## <a name="example"></a>使用例
 次の例は、.NET 2.0 Service Pack 1 でのみ使用できる DateTimeOffset 型を使用するクラスを示しています。 この例では、プロジェクトプロパティの [ターゲットフレームワーク] ボックスの一覧で .NET Framework 2.0 が選択されている必要があります。

 [!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Portability.UseOnlyApiFromTargetedFramework/CS/FxCop.Portability.UseOnlyApiFromTargetedFramework.cs#1)]

## <a name="example"></a>使用例
 次の例では、DateTimeOffset 型の使用法を DateTime 型に置き換えることによって、前述の違反を修正します。

 [!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Portability.UseOnlyApiFromTargetedFramework2/CS/FxCop.Portability.UseOnlyApiFromTargetedFramework2.cs#1)]

## <a name="see-also"></a>参照
 [特定の .NET Framework バージョンをターゲットとする](../ide/targeting-a-specific-dotnet-framework-version.md)[移植性の警告](../code-quality/portability-warnings.md)
