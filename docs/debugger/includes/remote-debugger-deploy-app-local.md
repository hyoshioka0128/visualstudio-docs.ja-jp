---
title: ローカル フォルダーに配置する
description: アプリをローカル フォルダーに配置する
services: ''
author: mikejo5000
ms.service: ''
ms.topic: include
ms.date: 05/23/2018
ms.author: mikejo
ms.custom: include file
ms.openlocfilehash: 3fa0569739ee81ec4b2aa0eec8157068ffc949cd
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149216"
---
1. **ソリューション エクスプローラー**で、プロジェクト ノードを右クリックし、 **[発行]** (Web フォームの場合は **[Web アプリの発行]** ) を選択します。

    以前に発行プロファイルを構成してある場合、 **[発行]** ウィンドウが表示されます。 **[新しいプロファイル]** をクリックします。

1. **[発行]** ダイアログ ボックスで **[フォルダー]** を選択し、 **[参照]** をクリックして、新しいフォルダー **C:\Publish** を作成します。

    ![RemoteDBG_Publish_Local](../media/remotedbg_publish_local.png "RemoteDBG_Publish_Local")

    Web フォーム アプリの場合は [発行] ダイアログ ボックスで **[カスタム]** を選択し、プロファイル名を入力して **[OK]** を選択します。

1. ドロップダウン リストの **[プロファイルの作成]** をクリックします ( **[発行]** が既定値です)。

1. **[発行]** ダイアログ ボックスで **[設定]** リンクをクリックし、 **[設定]** タブを選択します。

1. 構成を **[デバッグ]** に設定し、 **[発行前に既存のファイルをすべて削除する]** を選択してから **[保存]** をクリックします。

    > [!NOTE]
    > リリース ビルドを使用する場合は、発行時に web.config ファイルでデバッグを無効にします。

1. **[発行]** をクリックします。

    ![RemoteDBG_Publish_Debug_Config](../media/remotedbg_publish_debug_config.png "RemoteDBG_Publish_Debug_Config")

    アプリケーションによって、プロジェクトの **[デバッグ]** 構成がローカル フォルダーに発行されます。 出力ウィンドウに進行状況が表示されます。

1. Visual Studio コンピューターの ASP.NET プロジェクト ディレクトリを、Windows Server コンピューター上の ASP.NET アプリ用に構成されたローカル ディレクトリ (この例では **C:\Publish**) にコピーします。 このチュートリアルでは、手動でコピーすることを想定していますが、PowerShell、Xcopy、Robocopy などの他のツールを使用することもできます。

    > [!CAUTION]
    > コードの変更やリビルドが必要な場合は、再発行してこの手順を繰り返す必要があります。 リモート コンピューターにコピーした実行可能ファイルは、ローカルのソースとシンボルに正確に一致している必要があります。    これを行わないと、プロセスをデバッグしようとしたときに Visual Studio で `cannot find or open the PDB file` の警告が表示されます。

1. Windows Server 上のブラウザーでアプリを開いて、アプリを正しく実行できることを確認します。

    アプリが正常に動作しない場合は、サーバーにインストールされている ASP.NET のバージョンと Visual Studio マシンのバージョンが一致していないか、IIS または Web サイトの構成に問題がある可能性があります。 前述の手順を再確認してください。
