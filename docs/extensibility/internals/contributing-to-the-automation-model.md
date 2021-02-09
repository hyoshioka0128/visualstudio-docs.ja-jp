---
title: オートメーションモデルへの貢献 |Microsoft Docs
description: VSPackage を設計する際の一連のガイドラインに従って、Visual Studio オートメーションモデルに貢献する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 38ea8d477b377f78f5c836ec4661989cdbf8999c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99884612"
---
# <a name="contribute-to-the-automation-model"></a>オートメーションモデルに貢献する
Visual Studio には、環境をカスタマイズするための一連のオートメーションインターフェイスが用意されています。 オートメーションモデルは、エンドユーザーが Visual Studio のアドインと拡張機能を作成できるようにするオブジェクトモデルです。

 また、VSPackage の開発者がオートメーションモデルに貢献するのに適しています。これにより、VSPackage のエンドユーザーがアドインを作成できるようになります。また、で VSPackage を使用する場合は、通常、一貫したユーザーモデルエクスペリエンスが提供さ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] れます。

 エンドユーザーエクスペリエンスの一貫性を確保するために、VSPackage の設計時に一連のガイドラインに従って、VSPackage のオートメーションモデルがのアイデアに従うようにすることができ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="in-this-section"></a>このセクションの内容
- [オートメーションモデルの概要](../../extensibility/internals/automation-model-overview.md)

 共通環境の主要なファセットを制御するオブジェクトの関連グループとしてオートメーションモデルを定義します。 この一連のオブジェクトは、オートメーションモデルの図に示されています。

- [Vspackage の自動化を提供する](../../extensibility/internals/providing-automation-for-vspackages.md)

 VSPackage の自動化を実現する2つの主な方法について説明します。

- [プロジェクトオブジェクトの公開](../../extensibility/internals/exposing-project-objects.md)

 VSPackage 固有のオブジェクトを作成する手順について説明します。

- [プロジェクトモデリング](../../extensibility/internals/project-modeling.md)

 新しいプロジェクトの種類のオートメーションを作成するために必要な標準プロジェクトオブジェクトについて説明し、プロジェクトオートメーションが従うパスを示します。 このトピックでは、クラスの宣言と実装の一覧も示します。

- [イベントの公開](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)

 オートメーションモデルのイベントを作成する手順について説明します。

- [オプションページのオートメーションサポート](../../extensibility/internals/automation-support-for-options-pages.md)

 オブジェクトを拡張することによって、**ツール** メニューの VSPackage の [カスタム **オプション**] ダイアログボックスのサポートプロパティのオートメーションオブジェクトを返す方法について説明し `DTE.Properties` ます。

- [コードの自動化を提供する](../../extensibility/internals/providing-automation-for-code.md)

 コードのオートメーションモデルを作成する必要がないことについて説明します。 ただし、このトピックでは、コードモデルに関する洞察が得られる情報を提供するリンクが提供されています。

- [方法: Windows の自動化を提供する](../../extensibility/internals/how-to-provide-automation-for-windows.md)

 オートメーションオブジェクトをウィンドウで使用できるようにし、環境が既製のオートメーションオブジェクトを提供していない場合は常に、オートメーションを提供することをお勧めします。 ツールウィンドウとドキュメントウィンドウの自動化について説明します。

- [オートメーションモデルを使用する](../../extensibility/internals/using-the-automation-model.md)

 オートメーションコンシューマーが初期のプロジェクトオートメーションオブジェクトを取得する方法を示す2つのコード例を示します。

- [構成オブジェクトと SelectedItem オブジェクトのオートメーション](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)

 Configuration オブジェクトと SelectedItems オブジェクトのオートメーションに関する情報を提供します。

## <a name="reference"></a>リファレンス
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> VSPackage が DTE オートメーションオブジェクトモデルにどのように参加するかを示すコードサンプルを提供します。 パラメーター、戻り値、および選択された解説を一覧表示します。
