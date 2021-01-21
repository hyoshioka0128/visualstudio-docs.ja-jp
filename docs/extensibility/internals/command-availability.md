---
title: コマンドの可用性 |Microsoft Docs
description: 現在のプロジェクト、現在のエディター、およびその他の要因に基づいて変更されるコマンドコンテキストについて説明します。これにより、Visual Studio で使用できるコマンドが決まります。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- commands, context
- menu items, visibility contexts
ms.assetid: c74e3ccf-d771-48c8-a2f9-df323b166784
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1da4d48b41b4b42a3c3f049f64ca76e1d9eba6eb
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96189941"
---
# <a name="command-availability"></a>コマンドの可用性

Visual Studio のコンテキストによって、使用できるコマンドが決まります。 コンテキストは、現在のプロジェクト、現在のエディター、読み込まれている Vspackage、および統合開発環境 (IDE) のその他の側面によって変わります。

## <a name="command-contexts"></a>コマンドコンテキスト

最も一般的なコマンドコンテキストは次のとおりです。

- IDE: IDE によって提供されるコマンドは常に使用できます。

- VSPackage: Vspackage では、コマンドを表示するか非表示にするかを定義できます。

- Project: プロジェクトコマンドは、現在選択されているプロジェクトに対してのみ表示されます。

- エディター: 一度にアクティブにできるエディターは1つだけです。 アクティブなエディターのコマンドを使用できます。 エディターは言語サービスと密接に連携します。 言語サービスは、関連付けられているエディターのコンテキストでコマンドを処理する必要があります。

- ファイルの種類: エディターは、複数の種類のファイルを読み込むことができます。 使用可能なコマンドは、ファイルの種類によって変わることがあります。

- アクティブウィンドウ: 最後のアクティブなドキュメントウィンドウは、キーバインドのユーザーインターフェイス (UI) コンテキストを設定します。 ただし、内部 web ブラウザーに似たキーバインドテーブルを持つツールウィンドウでは、UI コンテキストを設定することもできます。 HTML エディターなどの複数タブのドキュメントウィンドウでは、すべてのタブに異なるコマンドコンテキスト GUID があります。 ツールウィンドウが登録されると、常に [ **表示** ] メニューから使用できるようになります。

- UI コンテキスト: UI コンテキストは、クラスの値によって識別されます。 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT> たとえば、 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid> ソリューションがビルドされているときや、 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid> デバッガーがアクティブになっているときなどです。 複数の UI コンテキストを同時にアクティブにすることができます。

## <a name="define-custom-context-guids"></a>カスタムコンテキスト Guid を定義する

適切なコマンドコンテキスト GUID がまだ定義されていない場合は、VSPackage で定義してから、コマンドの表示を制御するために必要に応じてアクティブまたは非アクティブになるようにプログラムを設定できます。

1. メソッドを呼び出してコンテキスト Guid を登録 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> します。

2. メソッドを呼び出して、コンテキスト GUID の状態を取得し <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> ます。

3. メソッドを呼び出して、コンテキスト Guid のオンとオフを切り替え <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> ます。

> [!CAUTION]
> VSPackage が既存のコンテキスト Guid に影響しないことを確認してください。他の Vspackage が依存している可能性があります。

## <a name="see-also"></a>関連項目

- [選択コンテキストオブジェクト](../../extensibility/internals/selection-context-objects.md)
- [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
