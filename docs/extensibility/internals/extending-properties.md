---
title: プロパティの拡張 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7064128c54434b0a7bb8799e62b751e765511c48
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708427"
---
# <a name="extend-properties"></a>プロパティを拡張する
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **[プロパティ]** ウィンドウは、COM および COM+ コンポーネント用の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]汎用プロパティ ブラウザであり、すべての製品をサポートします。 [**プロパティ]** ウィンドウ`ITypeInfo`は、型情報と COM+ メタデータを操作して、統合開発環境 (IDE) の他のウィンドウで現在選択されているオブジェクトのデザイン時プロパティを一覧表示します。

 キーボードの**F4**キーを押すか、[**表示**] メニューの **[プロパティ ウィンドウ]** をクリックして開くことができる **[プロパティ**] ウィンドウは、選択したオブジェクトの構成に依存しないデザイン時のプロパティとイベントを表示および編集するために使用します。 ソリューションおよびプロジェクトに関連付けられた構成依存プロパティは、[プロパティ ページ](../../extensibility/internals/property-pages.md)に表示されます。 詳細については、「[構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

 ![[プロパティ] ウィンドウの概要](../../extensibility/internals/media/vspropertieswindow.png "ウィンドウ")[プロパティ] ウィンドウ

 ここでは、**プロパティ**ウィンドウの個々の領域と、ウィンドウを設定するために実装および呼び出す必要があるインターフェイスに関する詳細情報を提供します。

## <a name="in-this-section"></a>このセクションの内容
- [[プロパティ] ウィンドウの概要](../../extensibility/internals/properties-window-overview.md)

 ツール ウィンドウとドキュメント ウィンドウに対する**プロパティ**ウィンドウの目的について説明します。

- [テンプレート ポリシーと [プロパティ] ウィンドウ](../../extensibility/internals/template-policy-and-the-properties-window.md)

 エンタープライズ テンプレート プロジェクトにプロジェクトを含む方法、およびエンタープライズ テンプレート プロジェクトがポリシーを適用する方法について説明します。

- [プロパティ ウィンドウのフィールドとインターフェイス](../../extensibility/internals/properties-window-fields-and-interfaces.md)

 **[プロパティ]** ウィンドウに表示される情報を決定する選択の基礎について説明します。

- [プロパティ ウィンドウ オブジェクト リスト](../../extensibility/internals/properties-window-object-list.md)

 **[プロパティ]** ウィンドウのオブジェクト一覧の目的について説明し、このリストの別のオブジェクトが呼び出しをトリガーしたときに、新しいオブジェクトが選択されたことが環境に通知される方法について説明します。

- [[プロパティ] ウィンドウのボタン](../../extensibility/internals/properties-window-buttons.md)

 **[プロパティ]** ウィンドウのツール バーに表示される既定の 4 つのボタンの目的について説明します。

- [プロパティ表示グリッド](../../extensibility/internals/properties-display-grid.md)

 グリッド内でプロパティ名フィールドとプロパティ値フィールドが見つかる場所について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 IDE のビルド ブロックとしてのプロジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]について説明します。

- [コンパイルとビルド](../../ide/compiling-and-building-in-visual-studio.md)

 アプリケーションをビルドするときに、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]継続的にテストおよびデバッグするためにプラットフォームを使用する方法について説明します。

- [Idispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)

 オートメーションを`IDispatch`サポートするために最初に設計されたインターフェイスについて説明し、オブジェクトのメソッドとプロパティに関する情報にアクセスして取得するための遅延バインディング機構を提供します。

- [アプリケーション設定の管理 (.NET)](../../ide/managing-application-settings-dotnet.md)

 アプリケーションのコンパイル済みコードではなく、外部構成ファイルにプロパティ値が格納されるようにアプリケーション設定の概要を説明します。

- [ソリューションとプロジェクト](../../ide/solutions-and-projects-in-visual-studio.md)

 ソリューションや[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プロジェクトを通じて開発作業に必要な参照、データ接続、フォルダ、ファイルなどの項目を効率的に管理する方法について説明します。

- [ビジュアル スタジオの他の部分を拡張します。](../../extensibility/extending-other-parts-of-visual-studio.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] サービスを使用して、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の他の部分に相当する UI 要素を作成する方法について説明します。
