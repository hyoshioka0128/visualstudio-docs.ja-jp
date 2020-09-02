---
title: VSPackage セットアップシナリオ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, deployment considerations
ms.assetid: d2928498-f27c-46b4-a9cd-cba41fd85a10
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a09b794a6cd81966df45a1b30182040d7ab9335e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696757"
---
# <a name="vspackage-setup-scenarios"></a>VSPackage のセットアップ シナリオ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

柔軟性を高めるために VSPackage インストーラーを設計することが重要です。 たとえば、今後、セキュリティパッチをリリースする必要がある場合や、完全なサイドバイサイドバージョン管理のサポートを必要とするビジネス戦略を変更する場合があります。  
  
 [複数のバージョンの Visual Studio をサポート](../../extensibility/supporting-multiple-versions-of-visual-studio.md)する場合は、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSPackage の共有インストールまたはサイドバイサイドインストールを使用して、のサイドバイサイドインストールをサポートする利点と問題について確認できます。 つまり、サイドバイサイドの Vspackage では、の新機能を最大限にサポートする柔軟性が提供されて [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] います。  
  
 このトピックで説明するシナリオは、唯一の選択肢ではありませんが、推奨されるベストプラクティスとして提示されます。  
  
## <a name="components-privacy-and-sharing"></a>コンポーネント、プライバシー、および共有  
  
##### <a name="make-your-components-independent"></a>コンポーネントを独立にする  
 コンポーネントを特定して設定し、を割り当てて、コンポーネントを展開した後は、その構成を `GUID` 変更することはできません。 コンポーネントのコンポジションを変更する場合、結果として得られるコンポーネントは新しいコンポーネントである必要があり `GUID` ます。 これらの事実を考慮すると、各コンポーネントを独立した独立した単位にすることによって、バージョン管理の柔軟性を最大限に高めることができます。 コンポーネントを制御するルールの詳細については、「 [コンポーネントコードの変更](https://msdn.microsoft.com/library/aa367849\(VS.85\).aspx) 」および「コンポーネント [ルールが壊れた場合](https://msdn.microsoft.com/library/aa372795\(VS.85\).aspx)の動作」を参照してください。  
  
##### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>コンポーネントに共有とプライベートのリソースを混在させない  
 参照カウントはコンポーネントレベルで発生します。 その結果、共有リソースとプライベートリソースを1つのコンポーネントに混在させることで、共有リソースを上書きすることなく、実行可能ファイルなどのプライベートリソースを更新できなくなります。 このシナリオでは、下位互換性の問題が生じ、サイドバイサイド機能の作成が制限されます。  
  
 たとえば、VSPackage をに登録するために使用するレジストリ値は、 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] VSPackage をに登録するために使用されているものとは別のコンポーネントに保持する必要があり [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 共有ファイルまたはレジストリ値は、他のコンポーネントにも存在します。  
  
## <a name="scenario-1-shared-vspackage"></a>シナリオ 1: 共有 VSPackage  
 このシナリオでは、共有 VSPackage (複数のバージョンのをサポートする1つのバイナリ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ) が Windows インストーラーパッケージに同梱されています。 の各バージョンへの登録 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、ユーザーが選択できる機能によって制御されます。 また、個別の機能に割り当てられている場合は、各コンポーネントを個別に選択してインストールまたはアンインストールすることができます。これにより、ユーザーは VSPackage を異なるバージョンに統合することができ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 Windows インストーラーパッケージでの機能の使用方法の詳細については、「 [Windows インストーラーの機能](https://msdn.microsoft.com/library/aa372840\(VS.85\).aspx) 」を参照してください。  
  
 ![VS 共有 VS パッケージ グラフィック](../../extensibility/internals/media/vs-sharedpackage.gif "VS_SharedPackage")  
共有 VSPackage インストーラー  
  
 図に示すように、共有コンポーネントは、常にインストールされている Feat_Common 機能の一部として作成されます。 Feat_VS2002 と Feat_VS2003 の機能を表示することで、VSPackage が統合するバージョンをインストール時に選択でき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 また、Windows インストーラーメンテナンスモードを使用して機能を追加または削除することもできます。この場合、のさまざまなバージョンの VSPackage 登録情報を追加または削除し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
> [!NOTE]
> 機能の表示列を0に設定すると、非表示になります。 1などの低レベルの列の値は、常にインストールされます。 詳細については、「 [Installlevel プロパティ](https://msdn.microsoft.com/library/aa369536\(VS.85\).aspx) 」と「 [Feature Table](https://msdn.microsoft.com/library/aa368585.aspx)」を参照してください。  
  
## <a name="scenario-2-shared-vspackage-update"></a>シナリオ 2: Shared VSPackage Update  
 このシナリオでは、シナリオ1で更新されたバージョンの VSPackage インストーラーが出荷されます。 説明のために、この更新プログラムにはのサポートが追加されてい [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ますが、セキュリティパッチやバグ修正の Service Pack がより単純な場合もあります。 新しいコンポーネントをインストールするための Windows インストーラーの規則では、システム上の変更されていないコンポーネントを再コピーしないようにする必要があります。 この場合、バージョン1.0 が既に存在するシステムによって、更新されたコンポーネント Comp_MyVSPackage.dll が上書きされ、ユーザーはそのコンポーネント Comp_VS2005_Reg に Feat_VS2005 新しい機能を追加することを選択できます。  
  
> [!CAUTION]
> VSPackage がの複数のバージョンで共有されて [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] いる場合、VSPackage の今後のリリースでは、以前のバージョンのとの下位互換性が維持されることが不可欠です [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 旧バージョンとの互換性を維持するには、サイドバイサイドのプライベート Vspackage を使用する必要があります。 詳細については、「 [Visual Studio の複数のバージョンのサポート](../../extensibility/supporting-multiple-versions-of-visual-studio.md)」を参照してください。  
  
 ![VS 共有 VS パッケージ更新イメージ](../../extensibility/internals/media/vs-sharedpackageupdate.gif "VS_SharedPackageUpdate")  
Shared VSPackage update インストーラー  
  
 このシナリオでは、Windows インストーラーのマイナーアップグレードのサポートを利用して、新しい VSPackage インストーラーを紹介します。 ユーザーは、バージョン1.1 をインストールするだけで、バージョン1.0 をアップグレードします。 ただし、システムにバージョン1.0 が必要ではありません。 バージョン1.0 のないシステムには、同じインストーラーによってバージョン1.1 がインストールされます。 このように小規模なアップグレードを行う利点は、アップグレードのインストーラーと製品版のインストーラーを開発する作業を実行する必要がないことです。 1つのインストーラーで両方のジョブを行います。 セキュリティの修正や Service Pack では、Windows インストーラーパッチを利用することがあります。 詳細については、「 [修正プログラムとアップグレード](https://msdn.microsoft.com/library/aa370579\(VS.85\).aspx)」を参照してください。  
  
## <a name="scenario-3-side-by-side-vspackage"></a>シナリオ 3: サイドバイサイドの VSPackage  
 このシナリオでは、Visual Studio .NET 2003 との各バージョン用に1つずつ、2つの VSPackage インストーラーを示し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 各インストーラーでは、サイドバイサイド (プライベート) VSPackage がインストールされます (特定のバージョンの用に特別にビルドおよびインストールされてい [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます)。 各 VSPackage は、独自のコンポーネントに含まれています。 その結果、それぞれの修正プログラムまたはメンテナンスリリースで個別にサービスを提供できます。 VSPackage DLL はバージョン固有であるため、DLL と同じコンポーネントに登録情報を含めるのが安全です。  
  
 ![Vs サイド&#45;&#45;サイド VS パッケージグラフィック](../../extensibility/internals/media/vs-sbys-package.gif "VS_SbyS_Package")  
サイドバイサイド VSPackage インストーラー  
  
 各インストーラーには、2つのインストーラー間で共有されるコードも含まれています。 共通の場所に共有コードがインストールされている場合、両方の .msi ファイルをインストールすると、共有コードが1回だけインストールされます。 2番目のインストーラーでは、コンポーネントの参照カウントをインクリメントします。 参照カウントによって、Vspackage のいずれかがアンインストールされた場合、共有コードは他の VSPackage のために残ります。 2番目の VSPackage もアンインストールされると、共有コードが削除されます。  
  
## <a name="scenario-4-side-by-side-vspackage-update"></a>シナリオ 4: サイドバイサイドの VSPackage 更新  
 このシナリオでは、の VSPackage にセキュリティの脆弱性があるため、 [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)] 更新を発行する必要があります。 シナリオ2と同様に、既存のインストールを更新してセキュリティ修正プログラムを適用し、セキュリティ修正プログラムが既に配置されている新しいインストールを展開する新しい .msi ファイルを作成できます。  
  
 この場合、VSPackage は、グローバルアセンブリキャッシュ (GAC) にインストールされているマネージ VSPackage です。 セキュリティ修正プログラムを含めるように再構築する場合は、アセンブリのバージョン番号のリビジョン番号部分を変更する必要があります。 新しいアセンブリバージョン番号の登録情報により、以前のバージョンが上書きされ、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] が固定アセンブリを読み込みます。  
  
 ![Vs サイド&#45;&#45;サイド VS パッケージ更新グラフィック](../../extensibility/internals/media/vs-sbys-packageupdate.gif "VS_SbyS_PackageUpdate")  
サイドバイサイドの VSPackage 更新インストーラー  
  
 **メモ** Side-by-side アセンブリの配置の詳細については、「展開の [簡略化と、.NET Framework による DLL の使用の解決](https://msdn.microsoft.com/library/ms973843.aspx)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Windows インストーラー](https://msdn.microsoft.com/library/cc185688\(VS.85\).aspx)   
 [複数バージョンの Visual Studio をサポートする](../../extensibility/supporting-multiple-versions-of-visual-studio.md)
