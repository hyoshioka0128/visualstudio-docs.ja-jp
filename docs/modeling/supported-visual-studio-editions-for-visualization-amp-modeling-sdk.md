---
title: 視覚化およびモデリング SDK でサポートされている Visual Studio のエディション
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
ms.openlocfilehash: 908a224feb9f6ad463ae14812b3a8550bf932e35
ms.sourcegitcommit: c31815e140f2ec79e00a9a9a19900778ec11e860
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "92298551"
---
# <a name="supported-visual-studio-editions-for-visualization--modeling-sdk"></a>Visualization and Modeling SDK に対してサポートされている Visual Studio のエディション

次に、の作成環境と配置環境ででサポートされている Visual Studio のエディションの一覧を示し [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] ます。 これらのエディションの詳細については、Microsoft Visual Studio [デベロッパーセンター](https://visualstudio.microsoft.com/)を参照してください。

## <a name="authoring-edition"></a>作成エディション

DSL を定義するには、以下のコンポーネントをインストールしておく必要があります。

|製品|ダウンロード リンク|
|-|-|
|Visual Studio|[http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com/)|
|Visual Studio SDK|[http://go.microsoft.com/fwlink/?LinkId=185580](/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts&preserve-view=true)|
|Visual Studio Visualization and Modeling SDK|[http://go.microsoft.com/fwlink/?LinkID=186128](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)|

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="deployment-editions"></a>配置エディション

[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] では、ビルドするドメイン固有言語を展開するための次の構成がサポートされています。

- Visual Studio Enterprise

- Visual Studio Professional

- Visual Studio Shell (統合モード) 再頒布可能パッケージ

- Visual Studio Shell (分離モード) 再頒布可能パッケージ

> [!NOTE]
> DSL をシェル製品で実行できるようにするには、拡張機能マニフェストで [ **サポートされている VS Edition** ] フィールドを設定する必要があります。 詳細については、「[ドメイン固有言語ソリューションの配置](msi-and-vsix-deployment-of-a-dsl.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))