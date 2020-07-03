---
title: Visual Studio SDK のインストール |Microsoft Docs
ms.date: 07/12/2018
ms.topic: overview
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31df92b011336320d759461ed16ce2a3c8f61017
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905542"
---
# <a name="install-the-visual-studio-sdk"></a>Visual Studio SDK のインストール

Visual Studio SDK (ソフトウェア開発キット) は、Visual Studio セットアップのオプション機能です。 VS SDK は、後でインストールすることもできます。

## <a name="install-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>Visual studio のインストールの一部として Visual Studio SDK をインストールする

Visual Studio のインストールに VS SDK を追加するには、**他のツールセット**の下に**visual studio 拡張機能の開発**ワークロードをインストールします。 このワークロードでは、Visual Studio SDK と必要な前提条件がインストールされます。 [**概要**] ビューでコンポーネントを選択または選択解除することにより、インストールをさらに調整できます。

## <a name="install-the-visual-studio-sdk-after-installing-visual-studio"></a>Visual Studio のインストール後に Visual Studio SDK をインストールする

Visual studio のインストールが完了した後に Visual Studio SDK をインストールするには、Visual Studio インストーラーを再実行し、 **Visual studio 拡張機能の開発**ワークロードを選択します。

## <a name="install-the-visual-studio-sdk-from-a-solution"></a>ソリューションから Visual Studio SDK をインストールする

VS SDK を最初にインストールせずに、機能拡張プロジェクトでソリューションを開くと、 **Visual Studio 拡張**機能の開発ワークロードをインストールするための [**見つからない機能のインストール**] ダイアログが表示されます。

![拡張機能の開発のインストール](../extensibility/media/install-extension-development.png "拡張機能の開発のインストール")

## <a name="install-the-visual-studio-sdk-from-the-command-line"></a>コマンドラインから Visual Studio SDK をインストールする

Visual Studio のワークロードまたはコンポーネントと同様に、コマンドラインから**Visual studio 拡張機能の開発**ワークロード (ID: VisualStudio. VisualStudioExtension) をインストールすることもできます。 適切なコマンドラインスイッチの詳細については、「[コマンドラインパラメーターを使用した Visual Studio のインストール](../install/use-command-line-parameters-to-install-visual-studio.md)」を参照してください。また、ワークロードまたはコンポーネント識別子を決定するための一般的な手順を参照してください。

インストールされている Visual Studio のバージョンに対応する Visual Studio インストーラーを使用する必要があることに注意してください。 たとえば、コンピューターに Visual Studio Enterprise がインストールされている場合は、Visual Studio Enterprise インストーラー (*vs_enterprise.exe*) を実行する必要があります。
