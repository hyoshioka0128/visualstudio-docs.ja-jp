---
title: '方法: 機能拡張プロジェクトを Visual Studio 2015 に移行するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, upgrading
ms.assetid: 22491cdc-8f04-4e1c-8eb4-ff33798ec792
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e2f4926a503304491164635b983353ba7f3bb0f6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75915984"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2015"></a>方法: 機能拡張プロジェクトを Visual Studio 2015 に移行する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

拡張機能をアップグレードする方法を次に示します。  
  
> [!IMPORTANT]
> 以前のバージョンの Visual Studio 用に拡張機能ソリューションのバージョンを維持する場合は、アップグレードする前にコピーを作成してください。 アップグレードされたバージョンを以前の状態に戻すことが困難な場合があります。  
  
#### <a name="to-upgrade-an-extensibility-solution"></a>拡張ソリューションをアップグレードするには  
  
1. アップグレードするコピーを使用して、新しいバージョンでそれを開きます。 アップグレードを元に戻すことはできません。  
  
2. アップグレードが完了したら、外部プログラムのパスを新しいバージョンの devenv.exe に変更します。 **ソリューションエクスプローラー**でプロジェクトノードを右クリックし、[**プロパティ**] を選択します。 [ **デバッグ** ] タブで、[ **外部プログラムを開始** ] を選択し、[devenv.exe のパスを Visual Studio 2015 のパスに変更します。これは次のようになります。  
  
     **%ProgramFiles%\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe**  
  
3. Microsoft.VisualStudio.Shell.14.0.dll への参照を追加します。 ( **ソリューションエクスプローラー** でプロジェクトノードを右クリックし、[ **追加/参照**] をクリックします。 [ **拡張** ] タブを選択し、 **14.0**を確認します。)  
  
4. ソリューションをビルドします。 ビルドされたファイルは次のように配置されます。  
  
     **%LOCALAPPDATA%\Microsoft\VisualStudio.14.0Exp\Extensions \\<作成者名 \> \\<プロジェクト名 \> \\<プロジェクト \> \\ のバージョン**です。  
  
#### <a name="to-update-an-extensibility-project-to-nuget-vs-sdk-reference-assemblies"></a>機能拡張プロジェクトを NuGet VS SDK 参照アセンブリに更新するには  
  
1. プロジェクトに必要な VS SDK 参照アセンブリを特定します。  **ソリューションエクスプローラー**で、プロジェクトの [**参照設定**] ノードを展開し、プロジェクト参照の一覧を確認します。  VS SDK 参照アセンブリには、名前に **VisualStudio** というプレフィックスが付けられます (例: VisualStudio)。  
  
2. プロジェクトから VS SDK 参照アセンブリを選択し、右クリックして **削除**します。  
  
3. VS SDK 参照アセンブリの NuGet バージョンを追加します。  **ソリューションエクスプローラー参照**] ノードで、[ **NuGet パッケージの管理**] を開きます。 ] ダイアログで、ユーザー アカウントを追加します。  このダイアログの詳細については、「 [ダイアログを使用した NuGet パッケージの管理](/nuget/consume-packages/install-use-packages-visual-studio)」を参照してください。 VS SDK 参照アセンブリは、 [VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility)によって[nuget.org](https://www.nuget.org/)に公開されます。  
  
4. **パッケージソース**として**nuget.org**を使用して、目的の参照アセンブリに一致する nuget パッケージ名 (例: VisualStudio) を検索し、プロジェクトにインストールします。  NuGet では、初期アセンブリの依存関係を満たすために、複数の参照アセンブリを追加できます。  
  
     必要に応じて、VS SDK [メタパッケージ](https://www.nuget.org/packages/VSSDK_Reference_Assemblies)をインストールして、すべての vs sdk 参照アセンブリを一度に追加できます。  
  
5. また、VS SDK ビルドツールの NuGet バージョンを使用するように切り替えることもできます。 この NuGet [パッケージは、](https://www.nuget.org/packages/Microsoft.VSSDK.BuildTools) プロジェクトに追加されると、VS SDK がインストールされていないコンピューターで機能拡張プロジェクトをビルドできるようにするために必要なツールとターゲットファイルが含まれます。  
  
> [!NOTE]
> NuGet 参照アセンブリおよびツールを使用するために、既存の機能拡張プロジェクトを更新する必要はありません。  これらは、VS SDK と共にインストールされた参照アセンブリとツールを使用して、引き続きビルドできます。
