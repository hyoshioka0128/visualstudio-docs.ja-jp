---
title: 共有 VS パッケージとバージョン管理 VS パッケージのどちらを選択する |マイクロソフトドキュメント
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
ms.openlocfilehash: 21fefb776fceeeef4db6997a5bd12a8b987af7d2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739876"
---
# <a name="choose-between-shared-and-versioned-vspackages"></a>共有 VS パッケージとバージョン対応 VS パッケージの間で選択
異なるバージョンの Visual Studio を同じコンピューターに共存させることができます。 VSPackage は、任意の[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]バージョンの組み合わせをサポートできます。

 VSPackages のサイド バイ サイド インストールは、共有戦略またはバージョン管理戦略の 2 つの戦略のいずれかを使用して有効にすることができます。 どちらも、.NET Framework の[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]複数のバージョンと関連するバージョンの存在に対応します。

 共有戦略では、VSPackage が複数の[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]バージョンで使用するために登録されています。 バージョン管理された戦略では、サポートするバージョンごとに 1 つずつ、複数の[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]VSPackage DLL がインストールされます。

## <a name="shared-vspackages"></a>共有 VS パッケージ
 共有 VSPackage を使用すると、複数の[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]バージョンの VSPackage を使用する場合に適しています。 共有 VSPackage を実装するには、次の手順を実行する必要があります。

- VSPackage を 複数のバージョンの[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]と互換性を持つようになります。 これを行う 2 つの方法があります。

  - VSPackage を、サポートする最も古いバージョンの[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]機能のみを使用するように制限します。

  - VSPackage を実行しているバージョン[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]に適応するようにプログラムします。 その後、新しいサービスのクエリが失敗した場合、VSPackage は、以前のバージョンでサポートされている[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]他のサービスを提供できます。

- 適切に VSPackage を登録します。 詳細については、「 [VSPackage 登録](../extensibility/internals/vspackage-registration.md)と[管理 VSPackage 登録](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)」を参照してください。

- ファイル拡張子を適切に登録します。 詳細については、「 [side-by-side デプロイメントのファイル名拡張子の登録](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)」を参照してください。

- の適切なバージョン用に VSPackage を展開するインストーラー[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]を作成します。 詳細については、「 Windows インストーラーと[コンポーネント管理](../extensibility/internals/component-management.md)[を使用した VSPackage](../extensibility/internals/installing-vspackages-with-windows-installer.md)のインストール 」を参照してください。

- 登録の競合の問題に対処します。 詳細については、「 [VSPackage の登録](../extensibility/internals/vspackage-registration.md)」を参照してください。

- 共有ファイルとバージョン管理されたファイルの両方が参照カウントを尊重して、複数のバージョンの安全なインストールと削除を可能にするようにしてください。 詳細については、[コンポーネント管理を](../extensibility/internals/component-management.md)参照してください。

## <a name="versioned-vspackages"></a>バージョン管理された VS パッケージ
 バージョン管理された VSPackage 戦略では、サポートするバージョン[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]ごとに VSPackage を 1 つ作成します。 これは、VSPackage の各バージョンが提供[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]するサービスを利用する場合に適しています。 ただし、単一のコード ベースまたは複数の独立したコード ベースから複数のバイナリを作成するというバージョン管理の戦略では、共有戦略よりも初期開発が必要になる可能性があります。 また、各バージョンに対して別のセットアップを作成するか、インストールされているバージョンと VSPackage がサポートしているバージョンを検出する[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]1 つのセットアップを作成する必要があるため、追加のセットアップ作業が必要になる場合があります。

## <a name="binary-compatibility"></a>バイナリの互換性
 一般に、バイナリ互換性により、以前のバージョンの Visual Studio で開発されたネイティブ コードの VSPackage を、より新しいバージョンの Visual Studio で実行できます。 ただし、次の 3 つの重要な例外があります。

- VSPackage が共通言語ランタイムの特定のバージョンに依存している場合は、そのバージョンが実行されているバージョン[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]を決定する必要があります。

- VSPackage は、別の VSPackage または別の製品の特定の機能に依存している可能性があります。 したがって、VSPackage は依存関係が満たされた場合にのみ実行できます。

- VSPackage は[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]、サービス パックまたはそれ以降のバージョンの セキュリティ修正プログラムの[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]影響を受ける可能性があります。 このような場合、以前のバージョンの VSPackage を使用して[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]開発された VSPackage[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]は、セキュリティ修正プログラムの適用後のバージョンでは実行されない可能性があります。 ただし、新しいバージョンでパッケージを再構築し、以前のバージョンでも実行できます。

  管理 VSPackages は、 の[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]バージョンと、[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]のターゲット バージョンと[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]一致する バージョンを使用してビルドする必要があります。

  VSPackage バイナリバイナリのバイナリ互換性の計画に加えて、ソリューションとプロジェクトのファイル形式も考慮する必要があります。 VSPackage で新しいプロジェクトの種類を作成する場合は、1 つのバージョンで実行できるか、複数のバージョン[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]で実行できるかを決定する必要があります。 詳細については、「[カスタム プロジェクトのアップグレード](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)」を参照してください。

## <a name="see-also"></a>関連項目
- [Windows インストーラーを使用した VS パッケージのインストール](../extensibility/internals/installing-vspackages-with-windows-installer.md)
- [コンポーネント管理](../extensibility/internals/component-management.md)
