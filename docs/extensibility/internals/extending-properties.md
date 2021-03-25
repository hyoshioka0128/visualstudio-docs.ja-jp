---
title: プロパティの拡張 |Microsoft Docs
description: Visual Studio プロパティウィンドウのプロパティの一覧を拡張するために実装する必要があるインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3b1006f74cd2de03b4fe74e090d7ffcd1c921e5d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069648"
---
# <a name="extend-properties"></a>プロパティの拡張
[ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **プロパティ** ] ウィンドウは、com コンポーネントと com + コンポーネントのユニバーサルプロパティブラウザーであり、すべての製品をサポートし [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 [ **プロパティ** ] ウィンドウでは、 `ITypeInfo` 型情報と com + メタデータを使用して、統合開発環境 (IDE) の他のウィンドウで現在選択されているオブジェクトのデザイン時プロパティを一覧表示します。

 [**プロパティ**] ウィンドウは、キーボードの **F4** キーを押すか、[**表示**] メニューの [**プロパティウィンドウ]** をクリックして開くことができます。このウィンドウでは、選択したオブジェクトの構成に依存しないデザイン時のプロパティやイベントを表示および編集できます。 ソリューションおよびプロジェクトに関連付けられている構成依存プロパティは、 [プロパティページ](../../extensibility/internals/property-pages.md)に表示されます。 詳細については、「 [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

 ![プロパティウィンドウの概要](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow") プロパティ ウィンドウ

 このセクションでは、[ **プロパティ** ] ウィンドウの個々の領域に関連する詳細情報と、を実装して、ウィンドウにデータを読み込むために呼び出す必要があるインターフェイスについて説明します。

## <a name="in-this-section"></a>このセクションの内容
- [プロパティウィンドウの概要](../../extensibility/internals/properties-window-overview.md)

 ツールウィンドウとドキュメントウィンドウを基準とした [ **プロパティ** ] ウィンドウの目的について説明します。

- [テンプレートポリシーとプロパティウィンドウ](../../extensibility/internals/template-policy-and-the-properties-window.md)

 エンタープライズテンプレートプロジェクトにプロジェクトを含める方法と、エンタープライズテンプレートプロジェクトでポリシーを適用する方法について説明します。

- [プロパティウィンドウのフィールドとインターフェイス](../../extensibility/internals/properties-window-fields-and-interfaces.md)

 [ **プロパティ** ] ウィンドウに表示する情報を決定する選択の基準について説明します。

- [プロパティウィンドウオブジェクトの一覧](../../extensibility/internals/properties-window-object-list.md)

 [ **プロパティ** ] ウィンドウオブジェクトリストの目的について説明します。このリストの別のオブジェクトが呼び出しをトリガーするときに、環境に新しいオブジェクトが選択されたことが通知されます。

- [プロパティウィンドウボタン](../../extensibility/internals/properties-window-buttons.md)

 [ **プロパティ** ] ウィンドウのツールバーに表示される4つの既定のボタンの目的について説明します。

- [プロパティ表示グリッド](../../extensibility/internals/properties-display-grid.md)

 プロパティ名とプロパティ値のフィールドがグリッド内で検出される場所について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 IDE の構成要素としてのプロジェクトについて説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- [コンパイルとビルド](../../ide/compiling-and-building-in-visual-studio.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]アプリケーションをビルドするときに、アプリケーションを継続的にテストおよびデバッグするためにプラットフォームを使用する方法について説明します。

- [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)

 最初に `IDispatch` オートメーションをサポートするように設計されたインターフェイスについて説明します。このインターフェイスは、オブジェクトのメソッドおよびプロパティに関する情報にアクセスしたり、情報を取得したりするための遅延バインディング機構を提供します。

- [アプリケーション設定の管理 (.NET)](../../ide/managing-application-settings-dotnet.md)

 アプリケーションの設定の概要を説明します。これにより、アプリケーションのコンパイル済みコードではなく、外部構成ファイルにプロパティ値が格納されるようにアプリケーションを構成できます。

- [ソリューションおよびプロジェクト](../../ide/solutions-and-projects-in-visual-studio.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソリューションとプロジェクトを通じて、開発作業に必要な参照、データ接続、フォルダー、ファイルなどの項目を効率的に管理する方法について説明します。

- [Visual Studio の他の部分を拡張する](../../extensibility/extending-other-parts-of-visual-studio.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] サービスを使用して、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の他の部分に相当する UI 要素を作成する方法について説明します。
