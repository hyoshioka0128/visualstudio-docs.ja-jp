---
title: Visual Studio SDK のインストール | Microsoft Docs
description: Visual Studio Software Development Kit をインストールするためのオプション (Visual Studio のインストール中など) について説明します。
ms.custom: SEO-VS-2020
ms.date: 07/12/2018
ms.topic: overview
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 331a219210c990aed2f9601cd1f9b1f0bc5710ed
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079164"
---
# <a name="install-the-visual-studio-sdk"></a>Visual Studio SDK のインストール

Visual Studio SDK (ソフトウェア開発キット) は、Visual Studio セットアップのオプション機能です。 VS SDK は、後でインストールすることもできます。

## <a name="install-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>Visual Studio のインストールの一環で Visual Studio SDK をインストールする

Visual Studio のインストールに VS SDK を含めるには、 **[他のツールセット]** で **[Visual Studio 拡張機能の開発]** ワークロードをインストールします。 このワークロードによって、Visual Studio SDK と必要な前提条件がインストールされます。 **[概要]** ビューからコンポーネントを選択または選択解除することで、インストールをさらに調整することができます。

## <a name="install-the-visual-studio-sdk-after-installing-visual-studio"></a>Visual Studio をインストールした後に Visual Studio SDK をインストールする

Visual Studio のインストールが完了した後に Visual Studio SDK をインストールするには、Visual Studio インストーラーを再実行し、 **[Visual Studio 拡張機能の開発]** ワークロードを選択します。

## <a name="install-the-visual-studio-sdk-from-a-solution"></a>ソリューションから Visual Studio SDK をインストールする

最初に VS SDK をインストールせずに機能拡張プロジェクトを含むソリューションを開くと、 **[見つからない機能のインストール]** ダイアログが表示され、 **[Visual Studio 拡張機能の開発]** ワークロードをインストールするように求められます。

![拡張機能の開発をインストールする](../extensibility/media/install-extension-development.png "拡張機能の開発をインストールする")

## <a name="install-the-visual-studio-sdk-from-the-command-line"></a>コマンド ラインから Visual Studio SDK をインストールする

他の Visual Studio ワークロードまたはコンポーネントと同様に、 **[Visual Studio 拡張機能の開発]** ワークロード (ID: Microsoft.VisualStudio.Workload.VisualStudioExtension) をコマンド ラインからインストールすることもできます。 適切なコマンドライン スイッチの詳細と、ワークロードまたはコンポーネントの識別子を決定する場合の一般的な手順については、「[コマンド ライン パラメーターを使用して Visual Studio をインストールする](../install/use-command-line-parameters-to-install-visual-studio.md)」を参照してください。

インストールされている Visual Studio のバージョンと一致する Visual Studio インストーラーを使用する必要があることにご注意ください。 たとえば、コンピューターに Visual Studio Enterprise がインストールされている場合は、Visual Studio Enterprise インストーラー (*vs_enterprise.exe*) を実行する必要があります。
