---
title: 相互運用機能アセンブリを使用してコマンドの状態を確認する |Microsoft Docs
description: IOleCommandTarget インターフェイスを使用して、VSPackage で処理されるコマンドの状態を確認する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, determining command status
- command handling with interop assemblies, status
ms.assetid: 2f5104d1-7b4c-4ca0-a626-50530a8f7f5c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e46252cea550a2caaa81c92853220db4fa2b5b1a
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328380"
---
# <a name="determine-command-status-by-using-interop-assemblies"></a>相互運用機能アセンブリを使用してコマンドの状態を確認する
VSPackage は、処理可能なコマンドの状態を追跡する必要があります。 環境では、VSPackage 内で処理されたコマンドが有効または無効になるタイミングを判断できません。 **切り取り**、**コピー**、**貼り付け** などの一般的なコマンドの状態など、コマンドの状態について環境に通知するのは、VSPackage の役割です。

## <a name="status-notification-sources"></a>状態通知のソース
 環境は、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> インターフェイスの VSPackage の実装の一部である vspackage ' メソッドを使用して、コマンドに関する情報を受け取り <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。 環境は、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 次の2つの条件下で VSPackage のメソッドを呼び出します。

- ユーザーがメインメニューまたはコンテキストメニュー (右クリック) を開くと、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> そのメニューのすべてのコマンドに対してメソッドが実行され、その状態が決定されます。

- VSPackage は、環境が現在のユーザーインターフェイス (UI) を更新することを要求します。 この更新は、現在ユーザーに表示されているコマンドとして実行されます。たとえば、[標準] ツールバーの [ **切り取り**]、[ **コピー**]、[ **貼り付け** ] の各グループ化が、コンテキストとユーザーの操作に応じて有効または無効になります。

  シェルは複数の Vspackage をホストするため、各 VSPackage をポーリングしてコマンドの状態を確認する必要があった場合、シェルのパフォーマンスが低下する可能性があります。 代わりに、VSPackage は、変更時に UI が変更されたときに環境に対して積極的に通知する必要があります。 更新通知の詳細については、「 [ユーザーインターフェイスを更新する](../../extensibility/updating-the-user-interface.md)」を参照してください。

## <a name="status-notification-failure"></a>状態通知エラー
 VSPackage がコマンドの状態の変更を環境に通知するのに失敗すると、UI が不整合な状態になる可能性があります。 メニューまたはコンテキストメニューのコマンドは、ユーザーがツールバー上に配置できることに注意してください。 そのため、メニューまたはコンテキストメニューが開いている場合にのみ UI を更新するだけでは十分ではありません。

## <a name="see-also"></a>関連項目
- [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [実装](../../extensibility/internals/command-implementation.md)
