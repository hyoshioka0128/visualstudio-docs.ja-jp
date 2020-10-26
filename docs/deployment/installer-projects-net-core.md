---
title: Visual Studio インストーラープロジェクトと .NET Core 3.1
ms.date: 08/18/2020
ms.topic: conceptual
helpviewer_keywords:
- installer projects
- installer projects, .NETCore
author: MSLukeWest
ms.author: lukewest
manager: MSLukeWest
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: a057e655df643c5ddfd85064ba84260a2644dffd
ms.sourcegitcommit: 1803a67b516f67b209d8f4cf147314e604ef1927
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89641577"
---
# <a name="visual-studio-installer-projects-extension-and-net-core-31"></a>Visual Studio Installer Projects 拡張機能 と .NET Core 3.1

アプリケーションを MSI としてパッケージ化することは、多くの場合、Visual Studio インストーラー Projects 拡張機能を使用して行われます。

拡張機能は、 [Visual Studio インストーラープロジェクト](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2017InstallerProjects)にダウンロードできます。

## <a name="update-for-net-core"></a>.NET Core 用の更新プログラム
.NET Core には、発行用に2つの異なるモデルがあります。

- フレームワークに依存する展開

- 自己完結型アプリケーションには、ランタイムが含まれます。

これらのデプロイ方法の詳細については、「 [.Net Core アプリケーション公開の概要](/dotnet/core/deploying/)」を参照してください。

### <a name="workflow-changes-for-net-core-31"></a>.NET Core 3.1 のワークフローの変更

1. .NET Core 3.1 プロジェクトの正しい出力を取得するには、[**プライマリ出力**ではなく**項目を発行**する] を選択します。  このダイアログを表示するには**Add**、  >  プロジェクトのコンテキストメニューから [**プロジェクト出力**の追加] を選択します。

    ![[プロジェクト出力グループの追加] ダイアログの [発行アイテム] 出力グループ](../deployment/media/installer-projects-net-core-publish-items-output.png "発行アイテムの選択")

2. 自己完結型のインストーラーを作成するには、適切なプロパティが設定された発行プロファイルの相対パスを使用して、セットアッププロジェクトの [**アイテムの発行**] ノードの**PublishProfilePath**プロパティを設定します。

    ![Publish Items プロジェクトの出力アイテムに発行プロファイルを設定する](../deployment/media/installer-projects-net-core-publish-profile.png "発行プロファイルの設定")

### <a name="prerequisites-for-net-core-31"></a>.NET Core 3.1 の前提条件

フレームワークに依存する .NET Core 3.1 アプリに必要なランタイムをインストーラーでインストールできるようにする場合は、 [前提条件](../deployment/application-deployment-prerequisites.md)を使用してこれを行うことができます。  インストーラープロジェクトの [プロパティ] ダイアログボックスで [ **前提条件...** ] ダイアログを開くと、次のエントリが表示されます。

![[前提条件] ダイアログの [.NET Core] 項目](../deployment/media/installer-projects-net-core-prerequisites.png ".NET Core の前提条件")

WPF/WinForms アプリケーションの場合は、[ **.Net Core ランタイム...** ] オプションを選択して [コンソールアプリケーション]、[ **.net デスクトップランタイム...** ] を選択する必要があります。

>[!NOTE]
>これらの項目は、Visual Studio 2019 Update 7 リリース以降で提供されています。

## <a name="see-also"></a>関連項目

- [[必須コンポーネント] ダイアログ ボックス](../ide/reference/prerequisites-dialog-box.md)
- [アプリケーションの展開の前提条件](../deployment/application-deployment-prerequisites.md)