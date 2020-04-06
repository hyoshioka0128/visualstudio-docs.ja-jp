---
title: VSPackage セットアップ シナリオ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, deployment considerations
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 01279666642adb729d4350b8a497c42d78159120
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703973"
---
# <a name="vspackage-setup-scenarios"></a>VSPackage のセットアップ シナリオ

柔軟性を持つ VSPackage インストーラーを設計することが重要です。 たとえば、将来セキュリティ更新プログラムをリリースする必要がある場合や、サイド バイ サイドのバージョン管理サポートを必要とするビジネス戦略を変更する必要がある場合があります。

[複数バージョンの Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)のサポート では、VSPackage の共有インストールまたはサイド バイ サイド インストール[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のいずれかでサイド バイ サイド インストールをサポートする利点と問題について説明します。 つまり、サイド バイ サイド VSPackages を使用すると、 の新機能をサポート[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]する柔軟性が最も高くなります。

このトピックで説明するシナリオは、ユーザーの選択ではなく、推奨されるベスト プラクティスとして提示されます。

## <a name="components-privacy-and-sharing"></a>コンポーネント、プライバシー、共有

### <a name="make-your-components-independent"></a>コンポーネントを独立させる

コンポーネントを識別して設定し、 を割`GUID`り当てて、コンポーネントを配置すると、その構成を変更することはできません。 コンポーネントのコンポジションを変更する場合、生成されるコンポーネントは新しい コンポーネントで、新`GUID`しい コンポーネントである必要があります。 これらの事実を考えると、最大のバージョン管理の柔軟性は、各コンポーネントを独立した自立したユニットにすることによって可能になります。 コンポーネントを管理するルールの詳細については、「[コンポーネント コードの変更](/windows/desktop/Msi/changing-the-component-code)」および「[コンポーネント ルールが壊れた場合の動作」](/windows/desktop/Msi/what-happens-if-the-component-rules-are-broken)を参照してください。

### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>コンポーネント内の共有リソースとプライベートリソースを混在させないでください。

参照カウントは、コンポーネント レベルで発生します。 そのため、共有リソースとプライベート リソースを 1 つのコンポーネントに混在させると、共有リソースを上書きすることなく、実行可能ファイルなどのプライベート リソースを更新できなくなります。 このシナリオでは、下位互換性の問題が発生し、サイド バイ サイド機能の作成を制限します。

たとえば、VSPackage を 使用して VSPackage[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]を登録するために使用するレジストリ値は、Visual Studio で VSPackage を登録するために使用するコンポーネントとは別のコンポーネントに保持する必要があります。 共有ファイルまたはレジストリ値は、さらに別のコンポーネントに入ります。

## <a name="scenario-1-shared-vspackage"></a>シナリオ 1: 共有 VS パッケージ

このシナリオでは、共有 VSPackage (Visual Studio の複数のバージョンをサポートする単一のバイナリは、Windows インストーラー パッケージに付属しています。 Visual Studio の各バージョンへの登録は、ユーザーが選択可能な機能によって制御されます。 また、個別の機能に割り当てられている場合、各コンポーネントをインストールまたはアンインストール用に個別に選択して、VSPackage を異なるバージョンの に統合する[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]制御をユーザーに与えることを意味します。 (Windows インストーラー パッケージの機能の使用の詳細については、「Windows インストーラの[機能](/windows/desktop/Msi/windows-installer-features)」を参照してください。

![VS 共有 VS パッケージ インストーラー](../../extensibility/internals/media/vs_sharedpackage.gif "VS_SharedPackage")

図に示すように、共有コンポーネントは常にインストールされるFeat_Common機能の一部として作成されます。 Feat_VS2002とFeat_VS2003機能を表示することで、VSPackage を統合する Visual Studio のバージョンをインストール時に選択できます。 ユーザーは、Windows インストーラーのメンテナンス モードを使用して、機能を追加または削除することもできます。

> [!NOTE]
> フィーチャの [表示] 列を 0 に設定すると、非表示になります。 1 などの低レベルの列の値は、常にインストールされます。 詳細については、「 [INSTALLLEVEL プロパティ](/windows/desktop/Msi/installlevel)」および[「機能テーブル 」](/windows/desktop/Msi/feature-table)を参照してください。

## <a name="scenario-2-shared-vspackage-update"></a>シナリオ 2: 共有 VSPackage の更新

このシナリオでは、VSPackage のインストーラーの更新されたバージョンのシナリオ 1 が出荷されます。 説明のために、この更新プログラムは Visual Studio のサポートを追加しますが、セキュリティ更新プログラムやバグ修正サービス パックも簡単です。 新しいコンポーネントをインストールするための Windows インストーラの規則では、既にシステム上にある変更されていないコンポーネントを再コピーしないようにする必要があります。 この場合、バージョン 1.0 が既に存在するシステムは、更新されたコンポーネント Comp_MyVSPackage.dll を上書きし、ユーザーがコンポーネント Comp_VS2005_Regを使用して新しい機能Feat_VS2005を追加することを選択できるようにします。

> [!CAUTION]
> VSPackage が 複数のバージョンで[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]共有される場合は、VSPackage の以降のリリースで、以前のバージョンの Visual Studio との下位互換性が維持される必要があります。 下位互換性を維持できない場合は、サイド バイ サイドのプライベート VSPackages を使用する必要があります。 詳細については、「 [Visual Studio の複数バージョンのサポート](../../extensibility/supporting-multiple-versions-of-visual-studio.md)」を参照してください。

![VS 共有 VS パッケージ更新のインストーラー](../../extensibility/internals/media/vs_sharedpackageupdate.gif "VS_SharedPackageUpdate")

このシナリオでは、マイナー アップグレードの Windows インストーラーのサポートを利用して、新しい VSPackage インストーラーを提示します。 ユーザーは単純にバージョン 1.1 をインストールし、バージョン 1.0 をアップグレードします。 ただし、システムにバージョン 1.0 をインストールする必要はありません。 同じインストーラがバージョン 1.0 を使用しないシステムにバージョン 1.1 をインストールします。 この方法でマイナー アップグレードを提供する利点は、アップグレード インストーラとフル製品インストーラーの開発作業を行う必要がなされないことです。 1 つのインストーラーは両方のジョブを実行します。 セキュリティ修正プログラムまたはサービス パックは、Windows インストーラの修正プログラムを利用する場合があります。 詳細については、「[修正プログラムとアップグレード](/windows/desktop/Msi/patching-and-upgrades)」を参照してください。

## <a name="scenario-3-side-by-side-vspackage"></a>シナリオ 3: サイド バイ サイド VS パッケージ

このシナリオでは、2 つの VSPackage インストーラーを示します 。 各インストーラーは、サイド バイ サイド 、つまりプライベートの VSPackage (特定のバージョンの Visual Studio 用に特別にビルドされ、インストールされたもの) をインストールします。 各 VSPackage は、独自のコンポーネントに含まれています。 したがって、各パッチは、パッチまたはメンテナンス リリースで個別にサービスを提供できます。 VSPackage DLL はバージョン固有であるため、DLL と同じコンポーネントに登録情報を含めることができます。

![VS サイド バイ サイド VS パッケージ インストーラー](../../extensibility/internals/media/vs_sbys_package.gif "VS_SbyS_Package")

各インストーラーには、2 つのインストーラー間で共有されるコードも含まれています。 共有コードが共通の場所にインストールされている場合、両方の .msi ファイルをインストールすると、共有コードは 1 回だけインストールされます。 2 番目のインストーラーは、コンポーネントの参照カウントをインクリメントするだけです。 参照カウントは、VSPackages の 1 つがアンインストールされた場合、共有コードは、他の VSPackage の残ることを保証します。 2 番目の VSPackage もアンインストールすると、共有コードは削除されます。

## <a name="scenario-4-side-by-side-vspackage-update"></a>シナリオ 4: サイド バイ サイド VSPackage の更新

このシナリオでは、VsPackage の Visual Studio は、セキュリティの脆弱性に苦しんで、更新プログラムを発行する必要があります。 シナリオ 2 と同様に、セキュリティ修正プログラムを含むように既存のインストールを更新する新しい .msi ファイルを作成したり、セキュリティ修正プログラムを既に適用して新しいインストールを展開したりできます。

この場合、VSPackage は、グローバル アセンブリ キャッシュ (GAC) にインストールされているマネージ VSPackage です。 セキュリティ修正を含むように再構築する場合は、アセンブリ バージョン番号のリビジョン番号の部分を変更する必要があります。 新しいアセンブリ バージョン番号の登録情報によって、以前のバージョンが上[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]書きされ、固定アセンブリが読み込まれます。

![VS サイド バイ サイド VS パッケージ更新プログラムのインストーラー](../../extensibility/internals/media/vs_sbys_packageupdate.gif "VS_SbyS_PackageUpdate")

サイド バイ サイド アセンブリの展開の詳細については、「 [.NET Framework を使用した DLL 地獄の展開の簡略化と解決](https://msdn.microsoft.com/library/ms973843.aspx)」を参照してください。

## <a name="see-also"></a>関連項目

- [インストーラ](/windows/desktop/Msi/windows-installer-portal)
- [複数バージョンの Visual Studio をサポートする](../../extensibility/supporting-multiple-versions-of-visual-studio.md)
