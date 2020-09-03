---
title: 出荷拡張機能 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c7154395be43f6a0b07e9f2557d94fa594ef5ba4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150786"
---
# <a name="shipping-visual-studio-extensions"></a>Visual Studio 拡張機能の配布
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**注**: Visual Studio ギャラリーは Visual Studio Marketplace に置き換えられています。 詳細については、このトピックの最新バージョンを参照してください。

拡張機能の開発が完了したら、他のコンピューターにインストールしたり、友人や同僚と共有したり、Visual Studio ギャラリーで公開したりすることができます。 このセクションでは、拡張機能を発行して維持するために必要なすべての操作について説明します。 .vsix ファイルの使用、発行、ローカライズ、および更新です。

## <a name="working-with-vsix-extensions"></a>VSIX 拡張機能の使用
 VSIX 拡張機能を作成するには、空の VSIX プロジェクトを作成してから、別の項目テンプレートを追加します。 詳細については、「 [VSIX プロジェクトテンプレート](../extensibility/vsix-project-template.md)」を参照してください。

 VSIX 形式を使用すると、プロジェクトテンプレート、項目テンプレート、Vspackage、Managed Extensibility Framework (MEF) コンポーネント、 **ツールボックス** コントロール、アセンブリ、およびカスタム型 (カスタムスタートページを含む) をパッケージ化できます。 VSIX 形式では、ファイルベースの配置が使用されます。 VSIX パッケージの詳細については、「 [Vsix パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)」を参照してください。

 VSIX 形式では、コードスニペットのインストールはサポートされていません。 また、グローバルアセンブリキャッシュ (GAC) への書き込みやシステムレジストリへの書き込みなど、他の特定のシナリオもサポートしていません。 のインストールで GAC またはレジストリに書き込む必要がある場合は、Windows インストーラーを使用する必要があります。 詳細については、「 [Windows インストーラー展開用の拡張機能の準備](../extensibility/preparing-extensions-for-windows-installer-deployment.md)」を参照してください。

## <a name="publishing-your-extension-to-the-visual-studio-gallery"></a>拡張機能を Visual Studio ギャラリーに発行する
 拡張機能を他のユーザーに配布するには、.vsix ファイルを郵送するか、サーバーに配置します。 しかし、多くの人の手でコードを取得する最善の方法は、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)に配置することです。 Visual studio ギャラリーの拡張機能は **、拡張機能と更新プログラム**を通じて visual studio ユーザーが使用できます。 詳細については、「 [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)」を参照してください。

 拡張機能を Visual Studio ギャラリーにアップロードする方法を示す完全な例については、「 [チュートリアル: Visual Studio 拡張機能の発行](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)」を参照してください。

## <a name="private-galleries"></a>Private Galleries
 コントロール、テンプレート、およびツールを開発するときに、イントラネット上のプライベートギャラリーに投稿することで、それらを組織と共有できます。 詳細については、「 [Private Galleries](../extensibility/private-galleries.md)」を参照してください。

## <a name="localizing-your-extension"></a>拡張機能のローカライズ
 拡張機能を別のロケールでリリースする予定の場合は、ローカライズを検討する必要があります。 関連項目の詳細については、「 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="updating-and-versioning-your-extension"></a>拡張機能の更新とバージョン管理
 拡張機能を発行した後、更新する必要がある時間が発生します。 Visual Studio ギャラリーで公開されている拡張機能を更新する方法については、「 [方法: 拡張機能を更新](../extensibility/how-to-update-a-visual-studio-extension.md)する」を参照してください。

 拡張機能は、複数のバージョンの Visual Studio をサポートするように設定できます。 詳細については、「 [Visual Studio の複数のバージョンのサポート](../extensibility/supporting-multiple-versions-of-visual-studio.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[VSIX プロジェクトのテンプレートの概要](../extensibility/getting-started-with-the-vsix-project-template.md)|VSIX プロジェクトテンプレートを使用してカスタムプロジェクトテンプレートをインストールする方法について説明します。|
|[VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)|VSIX パッケージのコンポーネントについて説明します。|
|[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)|拡張機能をパッケージ化および発行する手順について説明します。|
|[VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)|Vsixlangpack ファイルを使用して、インストールプロセスにローカライズされたテキストを提供する方法について説明します。|
|[方法: 拡張機能を更新する](../extensibility/how-to-update-a-visual-studio-extension.md)|システムの拡張機能を更新する方法と、既存の Visual Studio 拡張機能に更新プログラムを配置する方法について説明します。|
|[方法: VSIX パッケージへの依存関係の追加](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|VSIX 配置パッケージへの参照を追加する方法について説明します。|
|[Windows インストーラーの配置に関する拡張機能を準備する](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|Windows インストーラーを使用して拡張機能をデプロイする方法について説明します。|
|[VSIX パッケージの署名](../extensibility/signing-vsix-packages.md)|VSIX パッケージに署名する方法について説明します。|
|[プライベート ギャラリー](../extensibility/private-galleries.md)|拡張機能用のプライベートギャラリーを作成する方法について説明します。|
|[複数バージョンの Visual Studio をサポートする](../extensibility/supporting-multiple-versions-of-visual-studio.md)|拡張機能で Visual Studio の複数のバージョンをサポートする方法を示します。|
