---
title: 複数バージョンの Visual Studio 2015 のサポート |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8f4393a88a689e2a923291ada37a9b6d85718db5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841349"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>複数バージョンの Visual Studio をサポートする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この用語は、同じコンピューターに複数のバージョンの製品をインストール *して維持* することを意味します。 Vspackage では、ユーザーは複数の Visual Studio バージョンを同じコンピューターにインストールできます。 ただし、Vspackage のサイドバイサイドバージョンを1つのバージョンの Visual Studio に読み込むことはできません。

 VSPackage を Visual Studio のサイドバイサイドバージョンに読み込む前に、次のことを考慮してください。

- 実行する並列実装方法を決定する必要があります。

     詳細については、「 [共有バージョンとバージョン付き Vspackage の選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md)」を参照してください。

- ソリューションとプロジェクトファイルの形式は、実装戦略に適合している必要があります。

     詳細については、「 [カスタムプロジェクトのアップグレード](../misc/upgrading-custom-projects.md) 」および「 [サイドバイサイド配置用のファイル名拡張子の登録](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)」を参照してください。

- インストーラーは、バージョン管理されたコンポーネントと、すべてのバージョン間で共有されるコンポーネントが正しくインストールおよび登録されるように、実装戦略を処理する必要があります。

     詳細については、「Windows インストーラーと[コンポーネント管理](../extensibility/internals/component-management.md)を[使用した vspackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。

    > [!NOTE]
    > Visual Studio のバージョンをインストールすると、対応するバージョンのもインストールさ [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] れます。 たとえば、同じコンピューターに Visual Studio 2010 と Visual Studio 2012 をインストールすると、それぞれのバージョン4.0 と4.5 もインストールさ [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] れます。

## <a name="in-this-section"></a>このセクションの内容
 [共有バージョンとバージョン付き Vspackage の選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md) VSPackage のサイドバイサイドの問題を解決する方法について説明します。

 [サイドバイサイド配置のためにファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md) VSPackage がサイドバイサイドのシナリオでファイルの関連付けを登録する方法について説明します。

## <a name="related-sections"></a>関連項目
 [Vspackage のインストール](../misc/installing-vspackages.md) Vspackage をビルドしてインストールする方法と、複数のバージョンの Visual Studio を同時に実行しているユーザーをサポートする方法について説明します。
