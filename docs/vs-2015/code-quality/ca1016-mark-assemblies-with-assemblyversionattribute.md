---
title: 'CA1016: AssemblyVersionAttribute | を使用してアセンブリをマークします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkAssembliesWithAssemblyVersion
- CA1016
helpviewer_keywords:
- CA1016
- MarkAssembliesWithAssemblyVersion
ms.assetid: 4340aed8-d92b-4cde-a398-cb6963c6da5a
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 97bd41e51c8d6b5415ffb91c5696c7055f46cf7c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545406"
---
# <a name="ca1016-mark-assemblies-with-assemblyversionattribute"></a>CA1016:アセンブリに AssemblyVersionAttribute を設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|MarkAssembliesWithAssemblyVersion|
|CheckId|CA1016|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 アセンブリにバージョン番号がありません。

## <a name="rule-description"></a>ルールの説明
 アセンブリの id は、次の情報で構成されます。

- [アセンブリ名]

- バージョン番号

- カルチャ

- 公開キー (厳密な名前を持つアセンブリの場合)。

  [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] では、バージョン番号を使用してアセンブリを一意に識別し、厳密な名前を持つアセンブリの型にバインドします。 バージョン番号は、バージョンと発行者のポリシーと共に使用されます。 既定で、アプリケーションは、ビルドされたアセンブリのバージョンでのみ実行されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、属性を使用してバージョン番号をアセンブリに追加し <xref:System.Reflection.AssemblyVersionAttribute?displayProperty=fullName> ます。 次の例を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 サードパーティまたは運用環境で使用されているアセンブリについては、この規則による警告を抑制しないでください。

## <a name="example"></a>例
 次の例は、属性が適用されているアセンブリを示してい <xref:System.Reflection.AssemblyVersionAttribute> ます。

 [!code-cpp[FxCop.Design.AssembliesVersion#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesVersion/cpp/FxCop.Design.AssembliesVersion.cpp#1)]
 [!code-csharp[FxCop.Design.AssembliesVersion#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesVersion/cs/FxCop.Design.AssembliesVersion.cs#1)]
 [!code-vb[FxCop.Design.AssembliesVersion#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesVersion/vb/FxCop.Design.AssembliesVersion.vb#1)]

## <a name="see-also"></a>関連項目
 [アセンブリのバージョン管理](https://msdn.microsoft.com/library/775ad4fb-914f-453c-98ef-ce1089b6f903)[方法: 発行者ポリシーを作成する](https://msdn.microsoft.com/library/8046bc5d-2fa9-4277-8a5e-6dcc96c281d9)
