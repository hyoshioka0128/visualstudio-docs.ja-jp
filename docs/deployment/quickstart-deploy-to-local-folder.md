---
title: ローカル フォルダーに配置する
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, local folder
ms.assetid: adb461c4-812a-4b8c-b2ab-96002379f6a9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 862310c8c763ce366798bfacd4f4759d606bb33c
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "71128203"
---
# <a name="deploy-an-app-to-a-local-folder-using-visual-studio"></a>Visual Studio を使用してアプリをローカル フォルダーに配置する

Visual Studio からローカル フォルダーに ASP.NET、ASP.NET Core、.NET Core、および Python アプリを発行するには、 **[発行]** ツールを使用します。 Node.js では、この手順はサポートされていますが、ユーザー インターフェイスが異なります。

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]

> [!NOTE]
> ローカル フォルダーに Windows デスクトップ アプリケーションを発行する必要がある場合、[ClickOnce を使用したデスクトップ アプリの配置](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)に関するページ (C# または Visual Basic) を参照してください。 C++/CLI については、[ClickOnce を使用したネイティブ アプリの配置](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)に関するページを、C/C++ については、[セットアップ プロジェクトを使用したネイティブ アプリの配置](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)に関するページを参照してください。

## <a name="deploy-to-a-local-folder"></a>ローカル フォルダーに配置する

1. ソリューション エクスプローラーで、プロジェクトを右クリックして、 **[発行]** を選択します (または **[ビルド]**  >  **[発行]** メニュー項目を使用します)。

    ![ソリューション エクスプローラーのプロジェクト コンテキスト メニューにある [発行] コマンド](../deployment/media/quickstart-publish.png "[発行] を選択する")

1. 以前に発行プロファイルを構成してある場合、 **[発行]** ウィンドウが表示されます。 **[新しいプロファイルの作成]** を選択します。

1. **[発行先を選択]** ダイアログ ボックスで **[フォルダー]** を選択します。

    ![発行先としてローカル フォルダーを選択する](../deployment/media/quickstart-publish-folder.png "フォルダーの選択")

1. パスを入力するか、 **[参照]** を選択してローカル フォルダーを指定します。

1. **[発行]** を選びます。 プロジェクトがビルドされ、指定したフォルダーに発行されます。 プロジェクトのプロパティの **[発行]** ウィンドウが表示され、プロファイルの概要が表示されます。

    ![プロファイルの概要を示す [発行] プロパティ ウィンドウ](../deployment/media/quickstart-publish-folder-summary.png)

1. 配置設定を構成するには、プロファイルの概要の **[構成]** を選択し、 **[設定]** タブを選択します。

    ![プロファイルの設定](../deployment/media/quickstart-profile-settings.png "プロファイルの設定")

1. デバッグまたはリリースの構成を配置するかどうかなどのオプションを構成し、 **[保存]** を選択します。

1. 再発行するには、 **[発行]** を選択します。

発行したファイルは、任意の方法で展開できます。 たとえば、 *.zip* ファイルにパッケージ化したり、シンプルなコピー コマンドを使用したり、任意のインストール パッケージで展開したりできます。

## <a name="next-steps"></a>次の手順

- [発行ツールを使用して .NET Core アプリケーションを配置する](/dotnet/core/deploying/deploy-with-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Microsoft ストアのデスクトップ アプリをパッケージ化する (デスクトップ ブリッジ)](/windows/uwp/porting/desktop-to-uwp-packaging-dot-net?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- (.NET) [Framework およびアプリケーションの配置](/dotnet/framework/deployment/)
