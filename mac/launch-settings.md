---
title: launchSettings.json のサポート
description: このドキュメントでは、Visual Studio for Mac での launchSettings.json のサポートについて説明します
author: sayedihashimi
ms.author: sayedha
ms.date: 09/18/2019
ms.assetid: a556f9d7-86a8-408e-aa54-392584845889
ms.openlocfilehash: d35bfed901dca960ae21b4e2cf2fa75067c1b3ee
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "73715934"
---
# <a name="launchsettingsjson"></a>launchSettings.json

ASP.NET Core プロジェクトを開発するときは、launchSettings.json ファイルの内容をカスタマイズすることで、開発シナリオ内でプロジェクトを開始する方法を構成できます。 Visual Studio for Mac では、プロジェクト オプション UI を使用するか、ファイルを直接編集することで、このファイルを更新できます。 このファイルは、Windows 上で Visual Studio を実行する場合、または `dotnet` を使用してコマンド ラインから実行する場合に使用できる構成ファイルと同じです。 このファイルは、プロジェクトの Properties フォルダーの下に保存されます。

詳細については、「[ASP.NET Core で複数の環境を使用する](/aspnet/core/fundamentals/environments)」を参照してください。 この記事では、Visual Studio for Mac でこのファイルを更新する方法について説明します。

## <a name="update-the-start-configuration-by-using-visual-studio-for-mac"></a>Visual Studio for Mac を使用して開始構成を更新する

Visual Studio for Mac で launchSettings.json ファイルを直接編集することも、プロジェクト オプションを使用して編集することもできます。 プロジェクト オプションを表示するには、プロジェクトを右クリックし、 **[オプション]** を選択します。

!["オプション" が選択されているプロジェクトのショートカット メニュー](media/vsmac-ctx-proj-options.png)

**[実行]**  >  **[構成]**  >  **[既定値]** の順に選択します。

![プロジェクト オプションの "実行"、"構成"、および "既定値"](media/vsmac-run-config-default.png)

ここでは主に、次の 2 つを構成します。

 - 環境変数
 - プロジェクトのアプリの URL

## <a name="configure-environment-variables"></a>環境変数を構成する

グリッドを使用して、環境変数の値を指定することができます。 これらの環境変数は、Visual Studio for Mac 内でアプリケーションを起動するときに設定されます。 ASP.NET Core アプリケーションを開発する場合は、特殊な `ASPNETCORE_ENVIRONMENT` 環境変数に注意する必要があります。 詳細については、「[ASP.NET Core で複数の環境を使用する](/aspnet/core/fundamentals/environments)」を参照してください。


## <a name="configure-the-start-url"></a>開始 URL を構成する

アプリケーションの開始に使用する URL を構成するには、 **[ASP.NET Core]** タブにアクセスします。

![プロジェクト オプションのアプリケーションの URL](media/vsmac-run-config-default-aspnetcore.png)

ここでは、アプリケーションによって、その開始時にリッスンされる URL を指定できます。