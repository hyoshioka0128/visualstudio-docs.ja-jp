---
title: ローカル フォルダーに配置する
description: Visual Studio からフォルダーに ASP.NET、ASP.NET Core、.NET Core、Python アプリを発行するために [発行] ツールを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, local folder
ms.assetid: adb461c4-812a-4b8c-b2ab-96002379f6a9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 23ef2036af7b93ee6eeaaa14cb8733a4e0ced638
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249510"
---
# <a name="deploy-an-app-to-a-folder-using-visual-studio"></a>Visual Studio を使用してアプリをフォルダーに配置する

Visual Studio からフォルダーに ASP.NET、ASP.NET Core、.NET Core、および Python アプリを発行するには、 **[発行]** ツールを使用します。 Node.js では、この手順はサポートされていますが、ユーザー インターフェイスが異なります。

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]
::: moniker range=">=vs-2017"
> [!NOTE]
> フォルダーに Windows デスクトップ アプリケーションを発行する必要がある場合、[ClickOnce を使用したデスクトップ アプリの配置](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)に関するページ (C# または Visual Basic) を参照してください。 C++/CLR については、[ClickOnce を使用したネイティブ アプリの配置](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)に関するページを、C/C++ については、[セットアップ プロジェクトを使用したネイティブ アプリの配置](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)に関するページを参照してください。

::: moniker-end

::: moniker range=">=vs-2019"
> [!NOTE]
> .NET Core 3.1、またはそれ以降の Windows デスクトップ アプリケーションをフォルダーに発行する必要がある場合、「[ClickOnce を使用して .NET Windows アプリケーションを配置する](quickstart-deploy-using-clickonce-folder.md)」を参照してください。

::: moniker-end

## <a name="deploy-to-a-local-folder"></a>ローカル フォルダーに配置する

1. ソリューション エクスプローラーで、プロジェクトを右クリックして、 **[発行]** を選択します (または **[ビルド]**  >  **[発行]** メニュー項目を使用します)。

    ![ソリューション エクスプローラーのプロジェクト コンテキスト メニューにある [発行] コマンド](../deployment/media/quickstart-publish.png "[発行] を選択する")

1. 以前に発行プロファイルを構成してある場合、 **[発行]** ウィンドウが表示されます。 **[新規]** を選択します。

1. **[発行]** ウィンドウで、 **[フォルダー]** を選択します。

   ![発行先としてフォルダーを選択する](../deployment/media/quickstart-publish-folder-new.png "フォルダーの選択")

   ::: moniker range=">=vs-2019"

   .NET Core 3.1 以降の Windows アプリケーションを配置するとき、場合によっては、 **[特定のターゲット]** ウィンドウで **[フォルダー]** を選択する必要があります。

   ![特定のターゲットとしてフォルダーを選択する](../deployment/media/quickstart-publish-folder-targets.png "特定のターゲットの選択")

   ClickOnce を使用して .NET Core 3.1、またはそれ以降の Windows アプリケーションを発行する場合は、「[ClickOnce を使用して .NET Windows アプリケーションを配置する](quickstart-deploy-using-clickonce-folder.md)」を参照してください。
   ::: moniker-end

1. パスを入力するか、 **[参照]** を選択してフォルダーを指定します。

   ![フォルダーのパスを指定する](../deployment/media/quickstart-publish-folder-path.png "フォルダーの選択")

   ::: moniker range=">=vs-2019"
   **[完了]** をクリックし、プロファイルを保存します。

   ![プロファイルの概要を示す [発行] プロパティ ウィンドウ](../deployment/media/quickstart-publish-folder-summary.png)
   ::: moniker-end

1. **[発行]** を選びます。 プロジェクトがビルドされ、指定したフォルダーに発行されます。

   ::: moniker range="vs-2017"
   プロジェクトのプロパティの **[発行]** ウィンドウが表示され、プロファイルの概要が表示されます。

   ![プロファイルの概要を示す [発行] プロパティ ウィンドウ](../deployment/media/quickstart-publish-folder-summary.png)
   ::: moniker-end

1. デプロイ設定を構成するには、発行プロファイルの概要の **[編集]** を選択し、 **[設定]** タブを選択します。

   表示される設定は、アプリケーションの種類によって異なります。 次の図は、ASP.NET Core アプリの設定例を示しています。

    ![プロファイルの設定](../deployment/media/quickstart-profile-settings.png "プロファイルの設定")

    .NET で設定を選択するための追加のヘルプを参照するには、次を参照してください。

    - [フレームワーク依存と自己完結型の展開](/dotnet/core/deploying/)
    - [ターゲット ランタイム識別子 (ポータブル RID など)](/dotnet/core/rid-catalog)
    - [デバッグ構成とリリース構成](../ide/understanding-build-configurations.md)

1. デバッグまたはリリースの構成を配置するかどうかなどのオプションを構成し、 **[保存]** を選択します。

1. 再発行するには、 **[発行]** を選択します。

発行したファイルは、任意の方法で展開できます。 たとえば、 *.zip* ファイルにパッケージ化したり、シンプルなコピー コマンドを使用したり、任意のインストール パッケージで展開したりできます。

## <a name="next-steps"></a>次の手順

.NET アプリの場合:

- [発行ツールを使用して .NET Core アプリケーションを配置する](/dotnet/core/deploying/deploy-with-vs)
- [.NET Core アプリケーションの発光 (フレームワーク依存と自己完結型の展開)](/dotnet/core/deploying/)
- [.NET Framework およびアプリケーションの配置](/dotnet/framework/deployment/)
::: moniker range=">=vs-2019"
- [ClickOnce を使用して .NET Windows アプリケーションを配置する](quickstart-deploy-using-clickonce-folder.md)。
 ::: moniker-end
