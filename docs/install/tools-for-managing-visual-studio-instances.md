---
title: Visual Studio インスタンスの検出および管理用のツール
titleSuffix: ''
description: クライアント コンピューター上の Visual Studio のインストールを検出して管理するために使用できるツールについて説明します。
ms.date: 08/14/2017
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 85686707-14C0-4860-9B7A-66485D43D241
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: d6e46c95584cb3732d6339a02f6098976f2bab85
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76115033"
---
# <a name="tools-for-detecting-and-managing-visual-studio-instances"></a>Visual Studio インスタンスの検出および管理用のツール

クライアント コンピューターでの Visual Studio のインストールの検出と管理に使用できるツールは複数あります。

## <a name="detecting-existing-visual-studio-instances"></a>既存の Visual Studio インスタンスの検出

クライアント コンピューターにインストールされている Visual Studio インスタンスを検出して管理するために役立つ複数のツールが用意されています。

* [vswhere](https://github.com/microsoft/vswhere): Visual Studio に組み込まれているか、個別のディストリビューションで使用可能な実行可能ファイルです。特定のコンピューター上のすべての Visual Studio インスタンスの場所を見つけるのに役立ちます。
* [VSSetup.PowerShell](https://github.com/microsoft/vssetup.powershell):セットアップ構成 API を使用して Visual Studio のインストール済みインスタンスを識別する PowerShell スクリプトです。
* [VS-Setup-Samples](https://github.com/microsoft/vs-setup-samples):セットアップ構成 API を使用して既存のインストールを照会する方法を示す C# と C++ のサンプルです。

さらに、[セットアップ構成 API](<xref:Microsoft.VisualStudio.Setup.Configuration>) は、Visual Studio インスタンスを問い合わせるために独自のユーティリティを構築する開発者向けのインターフェイスを提供します。

## <a name="using-vswhereexe"></a>vswhere.exe の使用

`vswhere.exe` は Visual Studio (Visual Studio 2017 バージョン 15.2 以降のバージョン) に自動的に取り込まれます。またはそれを [vswhere リリース ページ](https://github.com/Microsoft/vswhere/releases)からダウンロードすることもできます。 ツールのヘルプ情報を取得する場合は `vswhere -?` を使用します。 たとえば、このコマンドでは以前のバージョンの製品やプレリリースを含む、Visual Studio のすべてのリリースが表示され、JSON 形式で結果が出力されます。

```cmd
C:\Program Files (x86)\Microsoft Visual Studio\Installer> vswhere.exe -legacy -prerelease -format json
```

::: moniker range="vs-2017"

> [!TIP]
> Visual Studio 2017 のインストールの詳細については、[Visual Studio セットアップのアーカイブ](https://devblogs.microsoft.com/setup/tag/vs2017/)に関するブログ記事を参照してください。

::: moniker-end

## <a name="editing-the-registry-for-a-visual-studio-instance"></a>Visual Studio インスタンスのレジストリの編集

Visual Studio ではレジストリ設定はプライベートな場所に保存されているため、同じバージョンの Visual Studio の複数のインスタンスを side-by-side で同じコンピューターで使用できます。

これらのエントリはグローバル レジストリには保存されないため、レジストリ エディターを使用してレジストリ設定を変更するための特別な指示があります。

1. Visual Studio で開いているインスタンスがある場合は、閉じてください。

1. `regedit.exe` を起動します。

1. `HKEY_LOCAL_MACHINE` ノードを選択します。

1. レジストリ エディターのメイン メニューから **[ファイル]**  >  **[ハイブの読み込み...]** を選択して、**AppData\Local** フォルダーに保存されているプライベート レジストリ ファイルを選択します。 次に例を示します。

   ```
   %localappdata%\Microsoft\VisualStudio\<config>\privateregistry.bin
   ```

   > [!NOTE]
   > `<config>` は参照する Visual Studio のインスタンスに対応します。

分離されたハイブの名前になるハイブ名を指定するように求められます。 これを行うと、作成した分離されたハイブの下にあるレジストリを参照できるようになります。

> [!IMPORTANT]
> Visual Studio を再度開始する前に、作成した分離されたハイブをアップロードする必要があります。 これを行うには、レジストリ エディターのメイン メニューから **[ファイル]**  >  **[ハイブのアンロード]** の順に選択します。 (これを行わない場合、ファイルがロックされたままになり、Visual Studio で開始することができません。)

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
