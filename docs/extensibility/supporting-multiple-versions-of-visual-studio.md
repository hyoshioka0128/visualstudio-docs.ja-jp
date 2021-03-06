---
title: Visual Studio の複数のバージョンのサポート |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3837116a33dc5608f75e48e3397273f65e5ea260
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49817991"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>複数バージョンの Visual Studio をサポートする
用語*サイド バイ サイドで*をインストールして同じコンピューター上の製品の複数のバージョンを維持することを意味します。 つまり、Vspackage の場合、ユーザーが同じコンピューターにインストールされているいくつかの Visual Studio のバージョンを持つことができます。 ただし、1 つのバージョンの Visual Studio に読み込まれる Vspackage のサイド バイ サイドのバージョンを含めることはできません。  
  
 VSPackage でサイド バイ サイドのバージョンの Visual Studio に読み込まれることを行う前に、次を検討してください。  
  
- サイド バイ サイドでの実装戦略に従うを決定する必要があります。  
  
   詳細については、次を参照してください。[共有間で選択するとバージョン管理 Vspackage](../extensibility/choosing-between-shared-and-versioned-vspackages.md)します。  
  
- ソリューションとプロジェクトのファイル形式は、実装戦略に収める必要があります。  
  
   詳細については、次を参照してください。[カスタム プロジェクトのアップグレード](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)と[サイド バイ サイドで配置のファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)します。  
  
- バージョン管理されたコンポーネントは、またすべてのバージョン間で共有されるコンポーネントを正しくインストールおよび登録できるように、インストーラーは、実装戦略を処理する必要があります。  
  
   詳細については、次を参照してください。 [Windows インストーラーで Vspackage をインストールする](../extensibility/internals/installing-vspackages-with-windows-installer.md)また[コンポーネント管理](../extensibility/internals/component-management.md)します。  
  
  > [!NOTE]
  >  Visual Studio のバージョンをインストールするの対応するバージョンをインストールしても、[!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)]します。 たとえば、バージョン 4.0 と 4.5 の Visual Studio 2010 および Visual Studio 2012 を同じコンピューターにインストールするインストールも、 [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)]、それぞれします。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [共有 VSPackage と バージョン管理 VSPackage の選択](../extensibility/choosing-between-shared-and-versioned-vspackages.md)  
 VSPackage でのサイド バイ サイドで問題を解決する方法について説明します。  
  
 [side-by-side 配置に対してファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)  
 サイド バイ サイドのシナリオでは、VSPackage がファイルの関連付けを登録する方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [Windows インストーラーによる VSPackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)  
