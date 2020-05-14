---
title: オートメーションモデルへの貢献 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d660edc740229c3e91b99e1f59eb37b4e9312098
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709270"
---
# <a name="contribute-to-the-automation-model"></a>オートメーションモデルへの貢献
Visual Studio には、環境をカスタマイズするための一連のオートメーション インターフェイスが用意されています。 オートメーション モデルは、エンド ユーザーが Visual Studio のアドインと拡張機能を作成できるようにするオブジェクト モデルです。

 さらに、VSPackage 開発者として、オートメーション モデルに貢献することは適切です。これにより、VSPackage のエンド ユーザーがアドインを作成できるようにし、一般的にで VSPackage を使用するときに一貫したユーザー モデル[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]エクスペリエンスを提供します。

 エンド ユーザー エクスペリエンスの一貫性を保つには、VSPackage のオートメーション モデルが のアイデアに従うように VSPackage を設計する際に[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、一連のガイドラインに従います。

## <a name="in-this-section"></a>このセクションの内容
- [オートメーション モデルの概要](../../extensibility/internals/automation-model-overview.md)

 オートメーション モデルを、共通環境の主要なファセットを制御するオブジェクトの関連グループとして定義します。 このオブジェクトのセットは、オートメーション モデルの図に示されています。

- [VS パッケージのオートメーションの提供](../../extensibility/internals/providing-automation-for-vspackages.md)

 VSPackage のオートメーションを提供する主な 2 つの方法について説明します。

- [プロジェクト オブジェクトを公開する](../../extensibility/internals/exposing-project-objects.md)

 VSPackage 固有のオブジェクトを作成するための手順について説明します。

- [プロジェクトモデリング](../../extensibility/internals/project-modeling.md)

 新しいプロジェクトの種類のオートメーションを作成するために必要な標準プロジェクト オブジェクトについて説明し、プロジェクトオートメーションが従うパスを示します。 このトピックでは、クラスの宣言と実装の一覧も示します。

- [イベントを公開する](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)

 オートメーション モデルのイベントを作成する手順について説明します。

- [オプション・ページの自動化サポート](../../extensibility/internals/automation-support-for-options-pages.md)

 VSPackage のカスタム**オプション**ダイアログ ボックスのプロパティをサポートするオートメーション オブジェクトを返す方法について説明、**ツール**メニュー`DTE.Properties`オブジェクトを拡張します。

- [コードの自動化を提供する](../../extensibility/internals/providing-automation-for-code.md)

 コードのオートメーション モデルを作成する必要がない場合について説明します。 ただし、コード モデルに関する洞察に満ちた情報を提供するリンクがこのトピックで提供されています。

- [方法 : Windows のオートメーションを提供する](../../extensibility/internals/how-to-provide-automation-for-windows.md)

 オートメーションオブジェクトをウィンドウで使用できるようにする場合、環境に既製のオートメーション オブジェクトが用意されていない場合は、オートメーションを提供することをお勧めします。 ツール ウィンドウとドキュメント ウィンドウのオートメーションについて説明します。

- [オートメーション モデルを使用する](../../extensibility/internals/using-the-automation-model.md)

 オートメーション コンシューマーが最初のプロジェクトオートメーション オブジェクトを取得する方法を示す 2 つのコード例を示します。

- [構成オブジェクトと SelectedItem オブジェクトのオートメーション](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)

 構成オブジェクトと SelectedItems オブジェクトのオートメーションに関する情報を提供します。

## <a name="reference"></a>リファレンス
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>VsPackage が DTE オートメーション オブジェクト モデルに参加する方法を示すコード サンプルを提供します。 パラメータ、戻り値、および選択された注釈を一覧表示します。
