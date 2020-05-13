---
title: 相互運用機能アセンブリを使用してコマンドの状態を確認する |マイクロソフトドキュメント
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
ms.openlocfilehash: 52bea32997b083cd13349a37201411e357f94a90
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708710"
---
# <a name="determine-command-status-by-using-interop-assemblies"></a>相互運用機能アセンブリを使用してコマンドの状態を確認する
VSPackage は、処理できるコマンドの状態を追跡する必要があります。 VSPackage 内で処理されたコマンドが有効または無効になるタイミングを環境で判断できません。 コマンドの状態 (**たとえば、切り取り**、**コピー**、**貼り付け**など) の状態を環境に通知するのは、VSPackage の役割です。

## <a name="status-notification-sources"></a>ステータス通知のソース
 環境は、VSPackage のインターフェイスの実装の一<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>部である VSPackages のメソッドを介してコマンドに関<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>する情報を受け取ります。 環境は、次<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>の 2 つの条件で VSPackage のメソッドを呼び出します。

- ユーザーがメイン メニューまたはコンテキスト メニューを開くと (右クリック)、環境はそのメニュー<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>のすべてのコマンドでメソッドを実行して状態を決定します。

- VSPackage が、環境が現在のユーザー インターフェイス (UI) を更新することを要求するとき。 この更新は、標準ツールバーの**切り取り**、**コピー**、**および貼り付け**などのユーザーに現在表示されているコマンドが、コンテキストとユーザーの操作に応じて有効になり、無効になった場合に発生します。

  シェルは複数の VSPackage をホストするため、コマンドの状態を判断するために各 VSPackage をポーリングする必要がある場合、シェルのパフォーマンスは許容できないほど低下します。 代わりに、VSPackage は、変更時に UI が変更されたときに環境にアクティブに通知する必要があります。 更新通知の詳細については、ユーザー[インターフェイスの更新を](../../extensibility/updating-the-user-interface.md)参照してください。

## <a name="status-notification-failure"></a>ステータス通知の失敗
 コマンド状態の変更の環境を通知する VSPackage の失敗は、UI を不整合状態に置くことができます。 メニューまたはコンテキスト メニューのコマンドは、ユーザーがツールバーに配置できることを覚えておいてください。 そのため、メニューまたはコンテキスト メニューが開いたときにのみ UI を更新するだけでは不十分です。

## <a name="see-also"></a>関連項目
- [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [実装](../../extensibility/internals/command-implementation.md)
