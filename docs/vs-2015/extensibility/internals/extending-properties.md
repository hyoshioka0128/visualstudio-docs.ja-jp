---
title: プロパティの拡張 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b5d2e7d15f7b479941c3186d8cd694c92f762bbf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690988"
---
# <a name="extending-properties"></a>プロパティの拡張
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **プロパティ** ] ウィンドウは、com コンポーネントと com + コンポーネントのユニバーサルプロパティブラウザーであり、すべての製品をサポートし [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 [ **プロパティ** ] ウィンドウでは、 `ITypeInfo` 型情報と com + メタデータを使用して、統合開発環境 (IDE) の他のウィンドウで現在選択されているオブジェクトのデザイン時プロパティを一覧表示します。  
  
 [**プロパティ**] ウィンドウは、キーボードの F4 キーを押すか、[**表示**] メニューの [**プロパティウィンドウ]** をクリックして開くことができます。このウィンドウでは、選択したオブジェクトの構成に依存しないデザイン時のプロパティやイベントを表示および編集できます。 ソリューションおよびプロジェクトに関連付けられている構成依存プロパティは、 [プロパティページ](../../extensibility/internals/property-pages.md)に表示されます。 詳細については、「 [NIB: プロジェクトプロパティ](https://msdn.microsoft.com/fb126574-24ad-4c96-9b2b-6e1f3879ba50)」、「 [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」、および「 [NIB: プロジェクトでの項目管理](https://msdn.microsoft.com/762e606b-7f44-4b66-97a1-e30a703654a0)」を参照してください。  
  
 ![プロパティ ウィンドウの概要](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow")  
[プロパティ] ウィンドウ  
  
 このセクションでは、[ **プロパティ** ] ウィンドウの個々の領域に関連する詳細情報と、を実装して、ウィンドウにデータを読み込むために呼び出す必要があるインターフェイスについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [プロパティ ウィンドウの概要](../../extensibility/internals/properties-window-overview.md)  
 ツールウィンドウとドキュメントウィンドウを基準とした [ **プロパティ** ] ウィンドウの目的について説明します。  
  
 [テンプレート ポリシーとプロパティ ウィンドウ](../../extensibility/internals/template-policy-and-the-properties-window.md)  
 エンタープライズテンプレートプロジェクトにプロジェクトを含める方法と、エンタープライズテンプレートプロジェクトでポリシーを適用する方法について説明します。  
  
 [プロパティ ウィンドウのフィールドとインターフェイス](../../extensibility/internals/properties-window-fields-and-interfaces.md)  
 [ **プロパティ** ] ウィンドウに表示する情報を決定する選択の基準について説明します。  
  
 [プロパティ ウィンドウのオブジェクト一覧](../../extensibility/internals/properties-window-object-list.md)  
 [ **プロパティ** ] ウィンドウオブジェクトリストの目的について説明します。このリストの別のオブジェクトが呼び出しをトリガーするときに、環境に新しいオブジェクトが選択されたことが通知されます。  
  
 [プロパティ ウィンドウのボタン](../../extensibility/internals/properties-window-buttons.md)  
 [ **プロパティ** ] ウィンドウのツールバーに表示される4つの既定のボタンの目的について説明します。  
  
 [プロパティ表示グリッド](../../extensibility/internals/properties-display-grid.md)  
 プロパティ名とプロパティ値のフィールドがグリッド内で検出される場所について説明します。  
  
 [プロパティ ウィンドウの選択の追跡の発表](../../misc/announcing-property-window-selection-tracking.md)  
 [ **プロパティ** ] ウィンドウの選択の追跡について説明します。  
  
 [子プロパティを持つ非表示のプロパティ](../../misc/hiding-properties-that-have-child-properties.md)  
 インターフェイスを実装することによって、子プロパティを持つプロパティを非表示にする方法について説明し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> ます。  
  
 [カスタム プロパティ ウィンドウの提供](../../misc/providing-a-custom-properties-window.md)  
 独自のプロパティブラウザーを提供する手順について詳しく説明します。  
  
 [[プロパティ] ウィンドウからのフィールドの説明の取得](../../misc/getting-field-descriptions-from-the-properties-window.md)  
 選択したプロパティフィールドに関連する情報を表示する説明領域の検索場所について説明します。  
  
 [[プロパティ] ウィンドウでプロパティ値を更新](../../misc/updating-property-values-in-the-properties-window.md)  
 **プロパティウィンドウを**プロパティ値の変更と同期させておくための2つの方法について、手順を追って説明します。  
  
## <a name="related-sections"></a>関連項目  
 [プロジェクトの種類](../../extensibility/internals/project-types.md)  
 IDE の構成要素としてのプロジェクトについて説明し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
 [コードのコンパイルとビルド](../../ide/compiling-and-building-in-visual-studio.md)  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]アプリケーションをビルドするときに、アプリケーションを継続的にテストおよびデバッグするためにプラットフォームを使用する方法について説明します。  
  
 [HTML の [DOCUMENT] プロパティ ([プロパティ] ウィンドウ)](https://msdn.microsoft.com/library/46e3d164-a1a7-42f9-87b0-344e10a37b62)  
 プロパティウィンドウから直接 HTML ドキュメントを編集する手順について説明し、プロパティウィンドウ内の HTML ドキュメント内のフィールドの詳細を示す表を示します。  
  
 [IDispatch](https://msdn.microsoft.com/ebbff4bc-36b2-4861-9efa-ffa45e013eb5)  
 最初に `IDispatch` オートメーションをサポートするように設計されたインターフェイスについて説明します。このインターフェイスは、オブジェクトのメソッドおよびプロパティに関する情報にアクセスしたり、情報を取得したりするための遅延バインディング機構を提供します。  
  
 [NIB: 動的プロパティの概要 (Visual Studio)](https://msdn.microsoft.com/f5102027-1431-4195-ae40-9b991de46d3a)  
 アプリケーションのコンパイル済みコードではなく外部構成ファイルにプロパティ値が格納されるようにアプリケーションを構成するための動的プロパティの概要について説明します。  
  
 [NIB: コンテナーとしてのプロジェクト](https://msdn.microsoft.com/87d40f63-f487-4767-8963-64beec27ba1b)  
 アプリケーションを構成する項目を論理的に管理、ビルド、およびデバッグするためのソリューション内のコンテナーとしてのプロジェクトの役割について説明します。  
  
 [NIB: プロジェクトのプロパティ](https://msdn.microsoft.com/fb126574-24ad-4c96-9b2b-6e1f3879ba50)  
 プロジェクト全体に適用されるプロパティと、プロジェクトの特定のビルド構成に限定されるプロパティを制御できるようにする設定をプロジェクトで管理する方法について説明します。  
  
 [ソリューションとプロジェクト](../../ide/solutions-and-projects-in-visual-studio.md)  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]ソリューションとプロジェクトを通じて、開発作業に必要な参照、データ接続、フォルダー、ファイルなどの項目を効率的に管理する方法について説明します。  
  
 [Visual Studio の他の部分の拡張](../../extensibility/extending-other-parts-of-visual-studio.md)  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] サービスを使用して、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]の他の部分に相当する UI 要素を作成する方法について説明します。
