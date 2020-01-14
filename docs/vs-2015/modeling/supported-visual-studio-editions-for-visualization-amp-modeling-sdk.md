---
title: 視覚化およびモデリング SDK のサポートされている Visual Studio のエディション |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, supported Visual Studio editions
ms.assetid: 7c313ba0-031d-45b8-8220-eead61754747
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 227c2871f68545c9f9fe5fa1ea3ceee827ccdc6a
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75917306"
---
# <a name="supported-visual-studio-editions-for-visualization-amp-modeling-sdk"></a>視覚化 &amp; モデリング SDK のサポートされている Visual Studio のエディション
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

サポートされている Visual Studio のエディションの一覧を以下に[!INCLUDE[dsl](../includes/dsl-md.md)]オーサリングとデプロイ環境にします。 これらのエディションの詳細については、Microsoft [!INCLUDE[vsprvs](../includes/vsprvs-md.md)][デベロッパーセンター](https://msdn.microsoft.com/vstudio/products/)を参照してください。

## <a name="authoring-edition"></a>作成エディション
 DSL を定義するには、以下のコンポーネントをインストールしておく必要があります。

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[https://www.visualstudio.com/](https://www.visualstudio.com/)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[Visual Studio SDK](../extensibility/visual-studio-sdk.md)|
|Visual Studio Visualization and Modeling SDK|[SDK のダウンロードのモデリング](https://www.microsoft.com/download/details.aspx?id=48148)|
## <a name="deployment-editions"></a>配置エディション
 [!INCLUDE[dsl](../includes/dsl-md.md)] では、作成したドメイン固有言語を配置するために、以下の構成がサポートされています。

- Visual Studio Enterprise

- Visual Studio Professional

- Visual Studio Shell (統合モード) 再頒布可能パッケージの再頒布可能パッケージ

- Visual Studio Shell (分離モード) 再頒布可能パッケージ

> [!NOTE]
> DSL を Shell 製品上で実行可能にするには、設定する必要があります、**サポートされている VS エディション**フィールドに、拡張機能マニフェストします。 詳細については、「[ドメイン固有言語ソリューションの配置](../modeling/deploying-domain-specific-language-solutions.md)」を参照してください。

## <a name="see-also"></a>参照
 [ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
