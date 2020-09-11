---
title: 共有バージョンとバージョン付き Vspackage の選択 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SxS
- side-by-side installation
- installation [Visual Studio SDK], side-by-side
ms.assetid: e3128ac3-2e92-48e9-87ab-3b6c9d80e8c9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 96386c2d3b7d1e822fdd1dd6632d754740f86301
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90011932"
---
# <a name="choose-between-shared-and-versioned-vspackages"></a>共有バージョンとバージョン付き Vspackage を選択する
異なるバージョンの Visual Studio を同じコンピューターに共存させることができます。 Vspackage は、すべてのバージョンをサポートでき [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

 Vspackage のサイドバイサイドインストールは、共有戦略またはバージョン管理された戦略の2つの方法のいずれかを使用して有効にすることができます。 どちらも、.NET Framework の複数のバージョンの存在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] と、関連付けられているバージョンの両方に対応します。

 共有戦略では、1つの VSPackage がの複数のバージョンで使用できるように登録されてい [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 バージョン管理された戦略では、サポートするのバージョンごとに1つずつ、複数の VSPackage Dll がインストールされ [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

## <a name="shared-vspackages"></a>共有 Vspackage
 共有 VSPackage の使用は、の複数のバージョンで同じ VSPackage を使用する場合に適してい [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 共有 VSPackage を実装するには、次の手順を実行する必要があります。

- VSPackage との複数のバージョンとの互換性を確保 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] します。 これを行うには、次の2つの方法があります。

  - サポートするの最も古いバージョンの機能のみを使用するように、VSPackage を制限し [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

  - 実行中ののバージョンに合わせて VSPackage をプログラムし [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 その後、新しいサービスのクエリが失敗した場合、VSPackage は、以前のバージョンのでサポートされている他のサービスを提供でき [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

- VSPackage を適切に登録します。 詳細については、「 [VSPackage registration](../extensibility/internals/vspackage-registration.md) And [Managed VSPackage registration](/previous-versions/bb166783(v=vs.100))」を参照してください。

- ファイル拡張子を適切に登録します。 詳細については、「 [サイドバイサイド配置のファイル名拡張子の登録](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)」を参照してください。

- 適切なバージョンの用に VSPackage を展開するインストーラーを作成 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] します。 詳細については、「Windows インストーラーおよび[コンポーネント管理](../extensibility/internals/component-management.md)を[使用した vspackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。

- 登録の競合の問題に対処します。 詳細については、「 [VSPackage registration](../extensibility/internals/vspackage-registration.md)」を参照してください。

- 共有ファイルとバージョン付きファイルの両方で、複数のバージョンを安全にインストールおよび削除できるように、参照カウントが考慮されていることを確認します。 詳細については、「 [コンポーネント管理](../extensibility/internals/component-management.md)」を参照してください。

## <a name="versioned-vspackages"></a>バージョン管理された Vspackage
 バージョン管理された VSPackage 戦略では、サポートするのバージョンごとに1つの VSPackage を作成し [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 これは、以降のバージョンので提供されるサービスを利用することが予想される場合に適しています。これは、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 各 VSPackage が他のユーザーに影響を与えずに進化する可能性があるためです。 それにもかかわらず、1つのコードベースまたは複数の独立したコードベースから複数のバイナリを作成する方法は、共有戦略よりも初期開発が必要になる場合があります。 また、追加のセットアップ作業が必要になることがあります。これは、各バージョンに対して個別のセットアップを作成するか、インストールされているのバージョン [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] と VSPackage でサポートされているのバージョンを検出する1つのセットアップを作成する必要があるためです。

## <a name="binary-compatibility"></a>バイナリの互換性
 一般に、バイナリ互換性を使用すると、以前のバージョンの Visual Studio で開発されたネイティブコードの Vspackage を、より新しいバージョンの Visual Studio で実行できるようになります。 ただし、次の3つの重要な例外があります。

- VSPackage が共通言語ランタイムの特定のバージョンに依存している場合は、実行されているバージョンを判断する必要があり [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

- VSPackage は、別の VSPackage または別の製品の特定の機能に依存している場合があります。 その結果、VSPackage は依存関係が満たされている場所でのみ実行できます。

- VSPackage [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] またはそれ以降のバージョンののセキュリティ修正 Service Pack プログラムによって、が影響を受ける可能性があり [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 このような場合、以前のバージョンので開発された VSPackage は、 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] セキュリティ修正プログラムが適用された後で、のバージョンでは実行されない可能性があります。 ただし、新しいバージョンでパッケージを再構築し、以前のバージョンでも実行することができます。

  マネージ Vspackage は、のバージョン [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] と、 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] ターゲットバージョンのと一致するを使用してビルドする必要があり [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

  VSPackage バイナリのバイナリ互換性を計画するだけでなく、ソリューションとプロジェクトファイルの形式も考慮する必要があります。 VSPackage が新しいプロジェクトの種類を作成する場合、1つのバージョンだけでも複数のバージョンのでも実行できるかどうかを決定する必要があり [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 詳細については、「 [カスタムプロジェクトのアップグレード](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)」を参照してください。

## <a name="see-also"></a>関連項目
- [Windows インストーラーを使用した Vspackage のインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)
- [コンポーネント管理](../extensibility/internals/component-management.md)