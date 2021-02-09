---
title: 複数バージョンの Visual Studio のサポート |Microsoft Docs
description: 複数のバージョンの Visual Studio をサポートする方法について説明します。 Vspackage はさまざまなバージョンに読み込むことができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 52b8bf1be57e10790d91d4712e56d707621cc7df
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889942"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>複数バージョンの Visual Studio をサポートする
この用語は、同じコンピューターに複数のバージョンの製品をインストール *して維持* することを意味します。 Vspackage では、ユーザーは複数の Visual Studio バージョンを同じコンピューターにインストールできます。 ただし、Vspackage のサイドバイサイドバージョンを1つのバージョンの Visual Studio に読み込むことはできません。

 VSPackage を Visual Studio のサイドバイサイドバージョンに読み込む前に、次のことを考慮してください。

- 実行する並列実装方法を決定する必要があります。

   詳細については、「 [共有バージョンとバージョン付き Vspackage の選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md)」を参照してください。

- ソリューションとプロジェクトファイルの形式は、実装戦略に適合している必要があります。

   詳細については、「 [カスタムプロジェクトのアップグレード](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects) 」および「 [サイドバイサイド配置用のファイル名拡張子の登録](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)」を参照してください。

- インストーラーは、バージョン管理されたコンポーネントと、すべてのバージョン間で共有されるコンポーネントが正しくインストールおよび登録されるように、実装戦略を処理する必要があります。

   詳細については、「Windows インストーラーと[コンポーネント管理](../extensibility/internals/component-management.md)を[使用した vspackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。

  > [!NOTE]
  > Visual Studio のバージョンをインストールすると、対応するバージョンの .NET Framework もインストールされます。 たとえば、同じコンピューターに Visual Studio 2010 と Visual Studio 2012 をインストールすると、.NET Framework のバージョン4.0 と4.5 もそれぞれインストールされます。

## <a name="in-this-section"></a>このセクションの内容
- [共有バージョンとバージョン付き Vspackage の選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md) VSPackage のサイドバイサイドの問題を解決する方法について説明します。

- [サイドバイサイド配置のためにファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md) VSPackage がサイドバイサイドのシナリオでファイルの関連付けを登録する方法について説明します。

## <a name="related-sections"></a>関連項目
- [Windows インストーラーによる VSPackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)
