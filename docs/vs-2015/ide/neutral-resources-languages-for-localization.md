---
title: ローカリゼーションのニュートラル リソース言語 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- localization [Visual Studio], resources
- NeutralResourcesLanguageAttribute class
- globalization [Visual Studio], resources
- resources [Visual Studio], fallback system
- culture, locating resources
- neutral resources
ms.assetid: ef064995-3b84-4698-a708-9689b7723533
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 85e0be0172f27732f8efeb882cbcde5b9c6aef3d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670386"
---
# <a name="neutral-resources-languages-for-localization"></a>ローカリゼーションのニュートラル リソース言語
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:System.Resources.NeutralResourcesLanguageAttribute> クラスでは、メイン アセンブリに含まれるリソースのカルチャが指定されています。 この属性はパフォーマンス向上のために使われ、<xref:System.Resources.ResourceManager> オブジェクトがメイン アセンブリに含まれるリソースを検索しなくて済むようにします。

 次のコードでは、ニュートラル リソース言語を設定する方法を示します。 このコードは、ビルド スクリプト、AssemblyInfo.vb または AssemblyInfo.cs に挿入できます。

```vb
' Set neutral resources language for assembly.
<Assembly: NeutralResourcesLanguageAttribute("en")>

```

```csharp
// Set neutral resources language for assembly.
[assembly: NeutralResourcesLanguageAttribute("en")]
```

## <a name="see-also"></a>関連項目
 アプリケーション[のローカライズ](../ide/localizing-applications.md)[のためのリソースの階層構造](../ide/hierarchical-organization-of-resources-for-localization.md) [.NET Framework に基づく国際対応アプリケーションの概要](../ide/introduction-to-international-applications-based-on-the-dotnet-framework.md)<xref:System.Resources.ResourceManager> アプリケーションのローカライズ[とローカライズ](../ide/globalizing-and-localizing-applications.md)を行う
