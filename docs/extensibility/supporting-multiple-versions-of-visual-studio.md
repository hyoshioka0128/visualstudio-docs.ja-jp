---
title: 複数バージョンの Visual Studio をサポートする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d571f1be4da45ff5ed6b2538cfb515930bde1de
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699476"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>複数バージョンの Visual Studio をサポートする
「*サイド バイサイド*」という用語は、同じコンピューターに複数のバージョンの製品をインストールして保守できることを意味します。 VSPackages の場合、ユーザーは複数の Visual Studio バージョンを同じコンピューターにインストールできます。 ただし、VSPackages のバージョンを 1 つのバージョンの Visual Studio に読み込むことはできません。

 VSPackage を Visual Studio のサイド バイ サイド バージョンに読み込める前に、次の点を考慮してください。

- どのサイド バイ サイド実装戦略に従う必要があるかを決定する必要があります。

   詳細については、「 [VSPackages の共有とバージョン管理の選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md)」を参照してください。

- ソリューションとプロジェクトのファイル形式は、実装戦略に適合している必要があります。

   詳細については、「[カスタム プロジェクトのアップグレード](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)」および[「side-by-Side 展開のファイル名拡張子の登録](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)」を参照してください。

- インストーラーは、バージョン管理されたコンポーネントと、すべてのバージョンで共有されるコンポーネントが正しくインストールおよび登録されるように、実装戦略を処理する必要があります。

   詳細については、「 [Windows インストーラーを使用した VSPackage](../extensibility/internals/installing-vspackages-with-windows-installer.md)のインストール」および[「コンポーネント管理](../extensibility/internals/component-management.md)」を参照してください。

  > [!NOTE]
  > Visual Studio のバージョンをインストールすると、対応するバージョンの .NET Framework もインストールされます。 たとえば、同じコンピューターに Visual Studio 2010 と Visual Studio 2012 をインストールすると、それぞれ .NET Framework のバージョン 4.0 と 4.5 もインストールされます。

## <a name="in-this-section"></a>このセクションの内容
- [共有 VS パッケージとバージョン管理された VS パッケージの選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md)VSPackage でのサイド バイ サイドの問題を解決する方法について説明します。

- [サイド バイ サイド展開のファイル名拡張子の登録](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)VSPackage が並べて表示されるシナリオでファイルの関連付けを登録する方法について説明します。

## <a name="related-sections"></a>関連項目
- [Windows インストーラーによる VSPackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)
