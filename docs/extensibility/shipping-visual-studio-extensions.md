---
title: 出荷の Visual Studio 拡張機能 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 767bb24bb5cb47f1af1452aa04ebdc91c778e284
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700120"
---
# <a name="shipping-visual-studio-extensions"></a>Visual Studio 拡張機能の配布
拡張機能の開発が完了したら、他のコンピューターにインストールしたり、友人や同僚と共有したり、Visual Studio マーケットプレースで公開したりすることができます。 このセクションでは、拡張子を公開および維持するために必要な作業について、.vsix ファイルの操作、公開、ローカライズ、更新などについて説明します。

## <a name="working-with-vsix-extensions"></a>VSIX 拡張機能の使用
 空白の VSIX プロジェクトを作成し、別の項目テンプレートを追加することで、VSIX 拡張機能を作成できます。 詳細については、「 [VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

 VSIX 形式を使用して、プロジェクト テンプレート、項目テンプレート、VSPackage、マネージ機能拡張フレームワーク (MEF) コンポーネント、**ツールボックス**コントロール、アセンブリ、およびカスタム型 (Visual Studio 2017 のカスタム スタート ページを含む) をパッケージ化できます。 VSIX 形式では、ファイル ベースの配置が使用されます。 VSIX パッケージの詳細については、「 [VSIX パッケージの解剖学](../extensibility/anatomy-of-a-vsix-package.md)」を参照してください。

 VSIX 形式では、コード スニペットのインストールはサポートされていません。 また、グローバル アセンブリ キャッシュ (GAC) やシステム レジストリへの書き込みなど、その他の特定のシナリオもサポートしていません。 インストールで GAC またはレジストリに書き込む必要がある場合は、Windows インストーラを使用する必要があります。 詳細については、「 [Windows インストーラの展開用の拡張機能の準備](../extensibility/preparing-extensions-for-windows-installer-deployment.md)」を参照してください。

## <a name="publishing-your-extension-to-the-visual-studio-marketplace"></a>拡張機能を Visual Studio マーケットプレースに発行する
 .vsix ファイルを送信するか、サーバーに配置するだけで、他のユーザーに拡張機能を配布できます。 しかし、多くの人々の手であなたのコードを得るための最良の方法は[、Visual Studioマーケットプレイスにそれを置くことです](https://marketplace.visualstudio.com/vs)。 Visual Studio マーケットプレース拡張機能は、**拡張機能と更新**プログラム を通じて Visual Studio ユーザーが使用できます。 詳細については、「 [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)」を参照してください。

 拡張機能を Visual Studio マーケットプレースにアップロードする方法を示す完全な例については、「[チュートリアル: Visual Studio 拡張機能の発行](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)」を参照してください。

## <a name="private-galleries"></a>Private Galleries
 コントロール、テンプレート、およびツールを開発する際に、イントラネットのプライベート ギャラリーにポストすることで、それらを組織と共有できます。 詳細については、「 [Private Galleries](../extensibility/private-galleries.md)」を参照してください。

## <a name="localizing-your-extension"></a>拡張機能のローカライズ
 異なるロケールで拡張機能をリリースする場合は、ローカライズを検討する必要があります。 関連する内容の詳細については、「 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="updating-and-versioning-your-extension"></a>拡張機能の更新とバージョン管理
 拡張機能を公開した後、更新が必要な時期が来ます。 Visual Studio マーケットプレースで公開されている拡張機能を更新する方法については、「[方法: 拡張機能を更新する](../extensibility/how-to-update-a-visual-studio-extension.md)」を参照してください。

 複数のバージョンの Visual Studio をサポートするように拡張機能を設定できます。 詳細については、「 [Visual Studio の複数バージョンのサポート](../extensibility/supporting-multiple-versions-of-visual-studio.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[VSIX プロジェクトのテンプレートの概要](../extensibility/getting-started-with-the-vsix-project-template.md)|VSIX プロジェクト テンプレートを使用してカスタム プロジェクト テンプレートをインストールする方法について説明します。|
|[VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)|VSIX パッケージのコンポーネントについて説明します。|
|[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)|拡張機能をパッケージ化して発行する手順について説明します。|
|[VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)|extension.vsixlangpack ファイルを使用して、インストール プロセスにローカライズされたテキストを提供する方法について説明します。|
|[方法: 拡張機能を更新する](../extensibility/how-to-update-a-visual-studio-extension.md)|システムの拡張機能を更新する方法と、既存の Visual Studio 拡張機能に更新プログラムを配置する方法について説明します。|
|[方法: VSIX パッケージへの依存関係の追加](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|VSIX 配置パッケージへの参照を追加する方法について説明します。|
|[Windows インストーラーの配置に関する拡張機能を準備する](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|Windows インストーラーを使用して拡張機能を配置する方法について説明します。|
|[VSIX パッケージの署名](../extensibility/signing-vsix-packages.md)|VSIX パッケージに署名する方法について説明します。|
|[プライベート ギャラリー](../extensibility/private-galleries.md)|拡張機能用のプライベート ギャラリーを作成する方法について説明します。|
|[複数バージョンの Visual Studio をサポートする](../extensibility/supporting-multiple-versions-of-visual-studio.md)|拡張機能で複数のバージョンの Visual Studio をサポートする方法について説明します。|
|[Visual Studio の検出](locating-visual-studio.md)|カスタム拡張機能の配置用の Visual Studio インスタンスを検索する方法について説明します。|
