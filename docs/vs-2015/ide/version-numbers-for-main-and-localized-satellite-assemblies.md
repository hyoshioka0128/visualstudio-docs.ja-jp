---
title: メイン アセンブリおよびローカライズされたサテライト アセンブリのバージョン番号 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- satellite assemblies, version numbers
- SatelliteContractVersionAttribute
- version numbers, assemblies
- assemblies [Visual Studio], version numbers
- versioning, assemblies
ms.assetid: 5489aea1-57b4-4561-9bb4-24d490269602
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aa064d875d5354ac4ae1fc5fdd8493c5efbbee01
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663057"
---
# <a name="version-numbers-for-main-and-localized-satellite-assemblies"></a>メイン アセンブリおよびローカライズされたサテライト アセンブリのバージョン番号
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:System.Resources.SatelliteContractVersionAttribute> クラスは、リソース マネージャーでローカライズされたリソースを使用するメイン アセンブリのバージョン管理をサポートしています。 <xref:System.Resources.SatelliteContractVersionAttribute> をアプリケーションのメイン アセンブリに適用すると、サテライト アセンブリを更新することなくメイン アセンブリを更新および再展開することができます。 たとえば、新しいリソースを導入していない Service Pack でも、サテライト アセンブリをリビルドして再展開することなく <xref:System.Resources.SatelliteContractVersionAttribute> クラスを使用できます。 ローカライズされたリソースを使用できるようにするには、メイン アセンブリのサテライト コントラクト バージョンがサテライト アセンブリの <xref:System.Reflection.AssemblyVersionAttribute> クラスと一致する必要があります。 <xref:System.Resources.SatelliteContractVersionAttribute>に正確なバージョン番号を指定する必要があります。"*" などのワイルドカード文字は使用できません。 詳細については、「[デスクトップ アプリケーションのリソースの取得](https://msdn.microsoft.com/library/eca16922-1c46-4f68-aefe-e7a12283641f)」を参照してください。

## <a name="updating-assemblies"></a>アセンブリを更新する
 <xref:System.Resources.SatelliteContractVersionAttribute> クラスを使用すると、サテライト アセンブリを更新することなくメイン アセンブリを更新し、メイン アセンブリを更新することなくサテライト アセンブリを更新できます。 メイン アセンブリを更新すると、メイン アセンブリのバージョン番号は変更されます。 既存のサテライト アセンブリを引き続き使用する場合は、メイン アセンブリのバージョン番号を変更し、サテライト コントラクト バージョン番号は同じままにします。 たとえば、最初のリリースで、メイン アセンブリのバージョンが 1.0.0.0 だとします。 サテライト アセンブリのサテライト コントラクト バージョンとアセンブリ バージョンはいずれも 1.0.0.0 です。 Service Pack に合わせてメイン アセンブリを更新する必要がある場合は、アセンブリのバージョンを 1.0.0.1 に変更し、サテライト コントラクト バージョンとサテライトのアセンブリ バージョンは 1.0.0.0 のままにすることができます。

 サテライト アセンブリを更新する必要があり、メイン アセンブリの更新は不要な場合は、サテライト アセンブリの <xref:System.Reflection.AssemblyVersionAttribute> を変更します。 サテライト アセンブリと共に、新しいサテライト アセンブリが古いサテライト アセンブリと互換性があることを示すポリシー アセンブリを含めて出荷する必要があります。 ポリシーの詳細については、「[ランタイムがアセンブリを検索する方法](https://msdn.microsoft.com/library/772ac6f4-64d2-4cfb-92fd-58096dcd6c34)」を参照してください。

 次のコードは、サテライト コントラクト バージョンを設定する方法を示しています。 このコードは、ビルド スクリプト、AssemblyInfo.vb または AssemblyInfo.cs に挿入できます。

```vb
<Assembly: SatelliteContractVersionAttribute("4.3.2.1")>

```

```csharp
[assembly: SatelliteContractVersionAttribute("4.3.2.1")]
```

## <a name="see-also"></a>関連項目
 [ランタイムがアセンブリを検索する方法](https://msdn.microsoft.com/library/772ac6f4-64d2-4cfb-92fd-58096dcd6c34)[アセンブリ属性](https://msdn.microsoft.com/library/36a98a81-b5b5-4c19-912a-11f91eff7f4e)[セキュリティおよびローカライズされたサテライトアセンブリ](../ide/security-and-localized-satellite-assemblies.md)[アプリケーションのローカライズアプリケーション](../ide/localizing-applications.md)[のグローバライズとローカライズ](../ide/globalizing-and-localizing-applications.md)
