---
title: レイヤーモデル拡張機能の配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams, deploying extensions
- layer models, deploying extensions
ms.assetid: 00a4675b-d20e-487e-8fd5-be2b1e0ba238
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5c11c952223854ff1b4b963e24615e7abe831496
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669861"
---
# <a name="deploy-a-layer-model-extension"></a>レイヤー モデル拡張機能の配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の他のユーザーは、Visual Studio を使って作成されたレイヤー モデリング拡張機能をインストールできます。

## <a name="installing-your-extension"></a>拡張機能のインストール
 拡張機能をコンパイルすると VSIX ファイルが作成され、これを他のコンピューターにインストールできます。 また、このファイルを開発用コンピューターにインストールし、Visual Studio のメイン インスタンスで拡張機能を使用できるようにすることもできます。

#### <a name="to-install-the-extension"></a>拡張機能をインストールするには

1. **ソース .vsix**が含まれているプロジェクトで、ファイルエクスプローラー**で \\ \\ bin*** を開きます。

2. 拡張機能をインストールするコンピューターに** \* .vsix**ファイルをコピーします。

3. ターゲット コンピューターの Windows エクスプローラーで *.vsix をダブルクリックします。

    VSIX インストーラーが起動します。

#### <a name="to-uninstall-the-extension"></a>拡張機能をアンインストールするには

1. Visual Studio の [ **ツール** ] メニューで、[ **拡張機能と更新プログラム**] をクリックします。

2. 拡張機能の名前をクリックし、[ **アンインストール**] をクリックします。

## <a name="installing-an-extension-on-a-team-foundation-build-server"></a>Team Foundation ビルド サーバーへの拡張機能のインストール
 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] 通常、サーバーには Visual Studio がインストールされていないため、VSIX をダブルクリックしてインストールすることはできません。 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] のインストールには VSIX 拡張機能を実行できるコンポーネントがいくつか含まれますが、拡張機能のインストールは手動で行う必要があります。

#### <a name="to-install-your-layer-extension-on-a-esprbuild-server"></a>レイヤー拡張機能を [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] サーバーにインストールするには

1. 開発用コンピューターからコンピューターに **.vsix**ファイルをコピーします。 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)]

     VSIX ファイルを次のいずれかの場所に置きます。

    - すべてのユーザーおよびサービスを対象にインストールする場合:

         %ProgramFiles%\Microsoft Visual Studio [バージョン]\Common7\IDE\Extensions\Microsoft

    - [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] を実行するネットワーク サービスだけを対象にインストールする場合:

         %WinDir%\ServiceProfiles\NetworkService\AppData\Local\Microsoft\VisualStudio \\ [バージョン] \Extensions\Microsoft

    - [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] が特定のユーザーとして対話モードで実行されるように構成されており、そのユーザーだけを対象にインストールする場合:

         %LocalAppData%\Microsoft\VisualStudio \\ [バージョン] \Extensions\Microsoft

        > [!NOTE]
        > % LocalAppData% は通常 *DriveName*: Users ユーザー*名*AppDataLocal です。

2. 各 VSIX ファイルを同じ場所のフォルダーに展開します。

    1. ファイル名拡張子を **.vsix** から **.zip**に変更します。

    2. .zip ファイルの内容をフォルダーに抽出します。

    3. .zip ファイルを削除します。

3. [!INCLUDE[esprbuild](../includes/esprbuild-md.md)]を再起動します。
