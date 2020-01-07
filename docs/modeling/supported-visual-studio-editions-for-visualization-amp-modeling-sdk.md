---
title: Visualization and Modeling SDK for Visual Studio のエディションがサポートされています
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, supported Visual Studio editions
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 127b45ae6a0ab28d7f83ee41449d7846858ee4a9
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591906"
---
# <a name="supported-visual-studio-editions-for-visualization--modeling-sdk"></a>Visualization and Modeling SDK に対してサポートされている Visual Studio のエディション

サポートされている Visual Studio のエディションの一覧を以下に[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]オーサリングとデプロイ環境にします。 これらのエディションの詳細については、Microsoft Visual Studio を参照してください。[デベロッパー センター](https://visualstudio.microsoft.com/)します。

## <a name="authoring-edition"></a>作成エディション

DSL を定義するには、以下のコンポーネントをインストールしておく必要があります。

|||
|-|-|
|Visual Studio|[http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com/)|
|Visual Studio SDK|[http://go.microsoft.com/fwlink/?LinkId=185580](/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts)|
|Visual Studio Visualization and Modeling SDK|[http://go.microsoft.com/fwlink/?LinkID=186128](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)|

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="deployment-editions"></a>配置エディション

[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] では、作成したドメイン固有言語を配置するために、以下の構成がサポートされています。

- Visual Studio Enterprise

- Visual Studio Professional

- Visual Studio Shell (統合モード) 再頒布可能パッケージの再頒布可能パッケージ

- Visual Studio Shell (分離モード) 再頒布可能パッケージ

> [!NOTE]
> DSL を Shell 製品上で実行可能にするには、設定する必要があります、**サポートされている VS エディション**フィールドに、拡張機能マニフェストします。 詳細については、「[ドメイン固有言語ソリューションの配置](msi-and-vsix-deployment-of-a-dsl.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
