---
title: 言語サービスおよびエディター拡張機能の概要 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 6b151891-c06d-40b1-9867-42298caa8492
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7894efc477e0c406cf8e85f4d3d31df4f2ef97c5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711311"
---
# <a name="get-started-with-language-service-and-editor-extensions"></a>言語サービスとエディター拡張機能の概要
エディター拡張機能を使用して、アウトライン、かっこの一致、IntelliSense、電球などの言語サービス機能を、独自のプログラミング言語または任意のコンテンツ タイプに追加できます。 また、テキストの色分け、余白、表示要素、その他のビジュアル要素など、Visual Studio エディターの外観と動作をカスタマイズすることもできます。 また、独自のタイプのコンテンツを定義したり、コンテンツが表示されるテキストビューの外観と動作を指定したりすることもできます。

 エディター拡張機能の作成を開始するには、Visual Studio SDK の一部としてインストールされているエディター プロジェクト テンプレートを使用します。 Visual Studio SDK は、VSPackage を使用するか、マネージ機能拡張フレームワーク (MEF) を使用して、Visual Studio 拡張機能を簡単に開発できるようにするツールのダウンロード可能なセットです。

> [!NOTE]
> Visual Studio SDK の詳細については[、「Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

 独自のエディター拡張機能を作成する前に、次の概念とテクノロジについて学習することをお勧めします。

## <a name="the-windows-presentation-foundation-wpf-and-editor-extensions"></a>Windows プレゼンテーション ファウンデーション (WPF) およびエディター拡張機能
 Visual Studio エディターのユーザー インターフェイス (UI) は、Windows プレゼンテーション ファウンデーション (WPF) を使用して実装されます。 WPF は、豊富なビジュアル エクスペリエンスと、コードの視覚的側面とビジネス ロジックを分離する一貫したプログラミング モデルを提供します。 エディター拡張機能を作成するときに、多くの WPF 要素と機能を使用できます。 詳細については、「 [Windows プレゼンテーション ファウンデーション](/dotnet/framework/wpf/index)」を参照してください。

## <a name="the-managed-extensibility-framework-mef-and-editor-extensions"></a>マネージ機能拡張フレームワーク (MEF) およびエディター拡張機能
 Visual Studio エディターは、マネージ機能拡張フレームワーク (MEF) を使用して、そのコンポーネントと拡張機能を管理します。 MEF を使用すると、開発者は Visual Studio などのホスト アプリケーションの拡張機能をより簡単に作成できます。 このフレームワークでは、MEF コントラクトに従って拡張を定義し、MEF コンポーネントパーツとしてエクスポートします。 ホスト アプリケーションは、コンポーネント パーツを検索して登録し、正しいコンテキストに適用されるようにしてコンポーネントパーツを管理します。

> [!NOTE]
> エディターでの MEF の詳細については、エディターの[マネージ機能拡張フレームワークを](../extensibility/managed-extensibility-framework-in-the-editor.md)参照してください。

## <a name="visual-studio-editor-extension-points-and-extensions"></a>Visual Studio エディターの拡張機能ポイントと拡張機能
 エディター拡張ポイントは、カスタマイズおよび拡張できる MEF コンポーネントパーツです。 場合によっては、インターフェイスを実装し、適切なメタデータと共にエクスポートすることによって、拡張ポイントを拡張します。 他のケースでは、単に拡張機能を宣言し、特定の型としてエクスポートします。

 以下は、エディタ拡張機能の基本的な種類の一部です。

- 余白とスクロール バー

- Tags

- 装飾

- オプション

- IntelliSense

  エディター拡張ポイントの詳細については、[言語サービスとエディター拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)を参照してください。

## <a name="deploying-editor-extensions"></a>エディター拡張機能の展開
 Visual Studio では、ソリューションに*source.extension.vsixmanifest*という名前のメタデータ ファイルを追加し、ソリューションをビルドし、Visual Studio に認識されているフォルダーにバイナリ ファイルとマニフェストのコピーを追加することで、エディター拡張機能を配置します。 マニフェスト ファイルは、拡張機能に関する基本的な情報 (名前、作成者、バージョン、コンテンツの種類など) を定義します。 VSIX マニフェスト ファイルの詳細と拡張機能を配置する方法については、「 [Visual Studio 拡張機能の出荷](../extensibility/shipping-visual-studio-extensions.md)」を参照してください。

 コンピューターに拡張機能をインストールする場合は、Visual Studio に認識されているフォルダーのサブフォルダーにバイナリとマニフェストを含めます。

> [!WARNING]
> Visual Studio に含まれているエディター拡張機能テンプレートのいずれかを使用する場合、マニフェストと配置場所の詳細について心配する必要はありません。 テンプレートには、拡張機能の登録と展開に必要なすべてが含まれています。

## <a name="run-extensions-in-the-experimental-instance"></a>実験用インスタンスでの拡張機能の実行
 拡張機能を開発中に、Visual Studio の作業バージョンを保護するには、次の実験用フォルダー (Windows Vista および Windows 7) に展開します。

 *{%ローカルアプリケーションデータ%}\VisualStudio\10.0Exp\拡張機能\\{会社\\} {拡張ID}*

 *%LOCALAPPDATA%* はログオン ユーザーの名前、*会社*は拡張機能を所有する会社の名前、*拡張 ID*は拡張機能の ID です。

 実験的な場所に拡張機能を配置すると、デバッグ モードで実行されます。 Visual Studio の 2 番目のインスタンスが起動し **、"Microsoft Visual Studio - 実験用インスタンス" という名前が付けられています**。

## <a name="manage-extensions"></a>拡張機能の管理
 Visual Studio の拡張機能は、[**ツール**] メニューの **[拡張機能と更新プログラム**] に表示されます。 実験用インスタンスで拡張をテストする場合、そのエクステンションは実験用インスタンスの **「拡張および更新」** にリストされますが、開発インスタンスにはリストされません。

 詳細については、「 [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)」を参照してください。

## <a name="use-templates-to-create-editor-extensions"></a>テンプレートを使用してエディター拡張機能を作成する
 エディター テンプレートを使用して、分類子、表示要素、および余白をカスタマイズする MEF 拡張機能を作成できます。 C# プロジェクトと Visual Basic プロジェクトの両方のテンプレートがあります。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

 また、VSIX プロジェクト テンプレートを使用して拡張機能を作成することもできます。 このテンプレートは、あらゆる種類の拡張機能を配置するために必要な要素のみを提供し *、source.extension.vsixmanifest*ファイル、必要なアセンブリ参照、および拡張機能を展開するためのビルド タスクを含むプロジェクト ファイルを含めます。 詳細については[、「VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

 また、エディター MEF コンポーネントを Visual Studio パッケージ拡張機能から作成することもできます。 詳細については、次のチュートリアルを参照してください。

- [チュートリアル: エディター拡張機能でのシェル コマンドの使用](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)

- [チュートリアル: エディター拡張機能でショートカット キーを使用する](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
