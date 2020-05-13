---
title: のインストールに関する情報 |マイクロソフトドキュメント
ms.date: 07/12/2018
ms.topic: conceptual
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2f391708abbd8a9b66f2dfd5aaa6559cb075910d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710341"
---
# <a name="install-the-visual-studio-sdk"></a>Visual Studio SDK のインストール

Visual Studio SDK (ソフトウェア開発キット) は、Visual Studio のセットアップのオプション機能です。 VS SDK は後でインストールすることもできます。

## <a name="install-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>インストールの一部として Visual Studio SDK をインストールする

VS SDK を Visual Studio のインストールに含めるには **、Visual Studio 拡張機能開発**ワークロードを **[その他のツールセット**] の下にインストールします。 このワークロードは、Visual Studio SDK と必要な前提条件をインストールします。 **[概要]** ビューでコンポーネントを選択または選択解除することで、インストールをさらに調整できます。

## <a name="install-the-visual-studio-sdk-after-installing-visual-studio"></a>インストール後に Visual Studio SDK をインストールする

Visual Studio のインストールが完了した後に Visual Studio SDK をインストールするには、Visual Studio インストーラーを再実行し **、Visual Studio 拡張機能の開発**ワークロードを選択します。

## <a name="install-the-visual-studio-sdk-from-a-solution"></a>ソリューションから Visual Studio SDK をインストールする

VS SDK をインストールせずに機能拡張プロジェクトを含むソリューションを開くと **、Visual Studio 拡張機能開発**ワークロードをインストールする [**見つからない機能のインストール**] ダイアログ ボックスが表示されます。

![拡張機能の開発をインストールする](../extensibility/media/install-extension-development.png "拡張機能の開発をインストールする")

## <a name="install-the-visual-studio-sdk-from-the-command-line"></a>コマンド ラインから Visual Studio SDK をインストールする

他の Visual Studio のワークロードまたはコンポーネントと同様に、コマンド ラインから**Visual Studio 拡張機能の開発**ワークロード (ID: 適切なコマンド ライン スイッチと、ワークロードまたはコンポーネント識別子の決定に関する一般的な手順については、「コマンド ライン[パラメーターを使用して Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md)をインストールする」を参照してください。

インストールされているバージョンの Visual Studio と一致する Visual Studio インストーラーを使用する必要があることに注意してください。 たとえば、コンピューターに Visual Studio エンタープライズがインストールされている場合は、Visual Studio エンタープライズ インストーラー (*vs_enterprise.exe*) を実行する必要があります。
