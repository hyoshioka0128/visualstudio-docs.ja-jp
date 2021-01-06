---
title: プロジェクトの種類のアーキテクチャ |Microsoft Docs
description: この記事は、Visual Studio でのプロジェクトの種類のアーキテクチャに関する詳細な情報を含む記事にリンクしています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], architecture
ms.assetid: 9c1d940f-8a54-41f7-a8aa-c870e324371c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ecde348ce52bdd354df61855d9907acf85900be2
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877781"
---
# <a name="project-types-architecture"></a>プロジェクト タイプのアーキテクチャ
ここでは、でのプロジェクトの種類のアーキテクチャに関する詳細について説明 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)

 プロジェクトの種類が使用できるサービスと、そのサービスが実装する必要のあるインターフェイスが一覧表示されます。

- [プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)

 インターフェイスのプロジェクト型について説明します。また、必要に応じて、追加の機能を提供するために実装することもできます。

- [プロジェクト タイプを作成する状況](../../extensibility/internals/when-to-create-project-types.md)

 は、プロジェクトの種類を作成する必要があるタイミングと、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] vspackage やエディターなどの別の機能拡張機能を使用して同じ目的を達成できるタイミングを決定するのに役立ちます。

- [階層と選択](../../extensibility/internals/hierarchies-and-selection.md)

 が [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 階層と選択コンテキストを使用して一貫性のある簡略化されたユーザーエクスペリエンスを提供する方法について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)

 プロジェクトのサブタイプを使用して、およびのプロジェクトシステムの動作をカスタマイズする方法について説明し [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ます。

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 プロジェクトの概要を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE: integrated development environment) の基本的な構成要素として提供します。 プロジェクトがコードのビルドとコンパイルを制御する方法について説明する追加のトピックへのリンクが用意されています。
