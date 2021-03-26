---
title: 言語サービスとエディターの拡張機能を使ってみる
description: 任意のコンテンツタイプに言語サービス機能を追加し、Visual Studio エディターの外観と動作をカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 6b151891-c06d-40b1-9867-42298caa8492
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1afec04882d5d52bffac509dd1d1202ccf9ea449
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057612"
---
# <a name="get-started-with-language-service-and-editor-extensions"></a>言語サービスとエディターの拡張機能を使ってみる

エディター拡張機能を使用すると、独自のプログラミング言語または任意のコンテンツタイプに、アウトライン、かっこの一致、IntelliSense、電球などの言語サービス機能を追加できます。 また、テキストの色分け、余白、装飾、その他のビジュアル要素など、Visual Studio エディターの外観と動作をカスタマイズすることもできます。 また、独自の種類のコンテンツを定義し、コンテンツが表示されるテキストビューの外観と動作を指定することもできます。

 エディター拡張機能の記述を開始するには、Visual Studio SDK の一部としてインストールされているエディタープロジェクトテンプレートを使用します。 Visual Studio SDK は、Vspackage を使用するか Managed Extensibility Framework (MEF) を使用して、Visual Studio 拡張機能の開発を容易にするダウンロード可能なツールのセットです。

> [!NOTE]
> Visual Studio SDK の詳細については、「 [Visual STUDIO sdk](../extensibility/visual-studio-sdk.md)」を参照してください。

 独自のエディター拡張機能を作成する前に、次の概念とテクノロジについて学習することをお勧めします。

## <a name="the-windows-presentation-foundation-wpf-and-editor-extensions"></a>Windows Presentation Foundation (WPF) とエディターの拡張機能

 Visual Studio エディターのユーザーインターフェイス (UI) は、Windows Presentation Foundation (WPF) を使用して実装されます。 WPF は、ビジネスロジックからコードの視覚的な側面を分離する、豊富なビジュアルエクスペリエンスと一貫したプログラミングモデルを提供します。 エディター拡張機能を作成するときに、多くの WPF 要素と機能を使用できます。 詳細については、「 [Windows Presentation Foundation](/dotnet/framework/wpf/index)」を参照してください。

## <a name="the-managed-extensibility-framework-mef-and-editor-extensions"></a>Managed Extensibility Framework (MEF) とエディターの拡張機能

 Visual Studio エディターは、Managed Extensibility Framework (MEF) を使用してそのコンポーネントと拡張機能を管理します。 MEF を使用すると、開発者は Visual Studio などのホストアプリケーションの拡張機能を簡単に作成することもできます。 このフレームワークでは、MEF コントラクトに従って拡張機能を定義し、MEF コンポーネントパーツとしてエクスポートします。 ホストアプリケーションは、コンポーネントを検索して登録し、適切なコンテキストに適用されていることを確認することで、コンポーネントのパーツを管理します。

> [!NOTE]
> エディターでの MEF の詳細については、 [エディターでの Managed Extensibility Framework](../extensibility/managed-extensibility-framework-in-the-editor.md)に関する説明を参照してください。

## <a name="visual-studio-editor-extension-points-and-extensions"></a>Visual Studio エディターの拡張ポイントと拡張機能

 エディター拡張ポイントは、カスタマイズおよび拡張できる MEF コンポーネント部分です。 場合によっては、インターフェイスを実装し、適切なメタデータと共にエクスポートすることによって、拡張ポイントを拡張します。 それ以外の場合は、拡張を宣言し、特定の型としてエクスポートするだけです。

 エディター拡張機能の基本的な種類を次に示します。

- 余白とスクロールバー

- タグ

- 修飾

- オプション

- IntelliSense

  エディターの拡張点の詳細については、「 [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)」を参照してください。

## <a name="deploying-editor-extensions"></a>エディター拡張機能の配置

 Visual Studio では、 *source.extension.vsixmanifest* という名前のメタデータファイルをソリューションに追加し、ソリューションをビルドした後、visual studio で認識されているフォルダーにバイナリファイルとマニフェストのコピーを追加することによって、エディター拡張機能を配置します。 マニフェストファイルでは、拡張機能に関する基本的な情報 (名前、作成者、バージョン、コンテンツの種類など) を定義します。 VSIX マニフェストファイルと拡張機能の配置方法の詳細については、「 [Visual Studio 拡張機能](../extensibility/shipping-visual-studio-extensions.md)の配布」を参照してください。

 コンピューターに拡張機能をインストールする場合は、Visual Studio が認識しているフォルダーのサブフォルダーにバイナリとマニフェストを含めます。

> [!WARNING]
> Visual Studio に含まれているエディター拡張機能テンプレートの1つを使用する場合、マニフェストと配置場所の詳細について心配する必要はありません。 テンプレートには、拡張機能を登録して展開するために必要なすべてが含まれています。

## <a name="run-extensions-in-the-experimental-instance"></a>実験用インスタンスで拡張機能を実行する

 拡張機能を開発している間に、Visual Studio の作業バージョンを分離するには、次の実験的なフォルダー (Windows Vista および Windows 7) にデプロイします。

 *{% LOCALAPPDATA%} \VisualStudio\10.0Exp\Extensions \\ {Company} \\ {extensionid}*

 ここで、 *% Localappdata%* はログオンユーザーの名前、 *company* は拡張機能を所有する会社の名前、 *EXTENSIONID* は拡張機能の id です。

 実験的な場所に拡張機能をデプロイすると、デバッグモードで実行されます。 Visual Studio の2番目のインスタンスが起動され、 **Microsoft Visual Studio の実験用インスタンス** という名前が付けられます。

## <a name="manage-extensions"></a>拡張機能の管理

 Visual Studio の拡張機能は、[**ツール**] メニューの [**拡張機能と更新プログラム**] に一覧表示されます。 実験用インスタンスで拡張機能をテストする場合は、実験用インスタンスの [ **拡張機能と更新プログラム** ] に一覧表示されますが、開発インスタンスには記載されていません。

 詳細については、「 [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)」を参照してください。

## <a name="use-templates-to-create-editor-extensions"></a>テンプレートを使用してエディター拡張機能を作成する

 エディターテンプレートを使用して、分類子、装飾、および余白をカスタマイズする MEF 拡張機能を作成できます。 C# プロジェクトと Visual Basic プロジェクトの両方のテンプレートがあります。 詳細については、「 [エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

 また、VSIX プロジェクトテンプレートを使用して拡張機能を作成することもできます。 このテンプレートは、あらゆる種類の拡張機能を配置するために必要な要素のみを提供します。また、 *source.extension.vsixmanifest* ファイル、必要なアセンブリ参照、および拡張機能を配置するためのビルドタスクを含むプロジェクトファイルを含めることができます。 詳細については、「[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

 また、Visual Studio パッケージ拡張機能からエディター MEF コンポーネントを作成することもできます。 詳細については、次のチュートリアルを参照してください。

- [チュートリアル: エディター拡張機能でのシェルコマンドの使用](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)

- [チュートリアル: エディター拡張機能でのショートカットキーの使用](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)

## <a name="see-also"></a>こちらもご覧ください

- [言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md)
