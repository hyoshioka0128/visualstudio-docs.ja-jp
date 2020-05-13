---
title: 相互運用機能アセンブリを使用するコマンドとメニュー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, using interop assemblies
- interop assemblies, using in commands and menus
- commands, handling using interop assemblies
- command handling with interop assemblies
ms.assetid: 8f4af525-39e5-4e69-92c8-d3efabe80bb2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e6c381abe9b4c6ea2a58342e185d7427fa56a180
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709484"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>相互運用機能アセンブリを使用するコマンドとメニュー
相互運用機能アセンブリを使用してメニュー コマンドとツール バー コマンドを実装する VSPackage は、次の操作を行う必要があります。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) に、サポートするコマンドと、現在有効になっているかどうかを通知します。

- コマンドを処理するための規則 (コントラクト) に従ってください。

- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>または<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>インターフェイスを使用して、コマンド処理を明示的に実装します。

  次のセクションでは、これらのタスクを実行する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [相互運用機能アセンブリを使用してコマンドの状態を確認する](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)

 VSPackage がサポートするコマンドと、現在有効になっているかどうかについて、どのように IDE に通知するかについて説明します。

- [相互運用機能アセンブリのコマンド コントラクト](../../extensibility/internals/command-contracts-in-interop-assemblies.md)

 相互運用機能アセンブリを使用してコマンドを実装するすべての VSPackage で使用される基本的なコマンド コントラクトの定義を提供します。

- [コマンドの実装](../../extensibility/internals/command-implementation.md)

 VSPackage がコマンドを実装する方法の概要を説明します。

- [相互運用機能アセンブリのコマンド ハンドラーの登録](../../extensibility/internals/registering-interop-assembly-command-handlers.md)

 VSPackage がコマンド ハンドラーを提供することを IDE に通知するために必要なレジストリ エントリについて説明します。

## <a name="related-sections"></a>関連項目
- [コマンドの可用性](../../extensibility/internals/command-availability.md)

 使用可能な VSPackage コマンドと、それらを処理するオブジェクトを決定するために IDE によって使用される条件について説明します。

- [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 コマンド サポートを使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]する UI の作成方法について説明します。

- [VS パッケージでのコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)

 オブジェクトを正しいコマンド要求に関連付けるために使用されるプロセスの概要。
