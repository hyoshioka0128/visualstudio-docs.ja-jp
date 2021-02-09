---
title: 相互運用機能アセンブリを使用するコマンドとメニュー |Microsoft Docs
description: 相互運用機能アセンブリを使用して VSPackage でメニューおよびツールバーコマンドを実装するときに完了する必要があるタスクについて説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6ea48c77212927c14b4ad49c91ce2f4d988e36f5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99928225"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>相互運用機能アセンブリを使用するコマンドとメニュー
相互運用機能アセンブリを使用してメニューとツールバーのコマンドを実装する VSPackage は、次の操作を行う必要があります。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE: integrated development environment) がサポートしているコマンドと、現在有効になっているかどうかについて通知します。

- コマンドを処理するためのルール (コントラクト) に従います。

- インターフェイスまたはインターフェイスを使用して、コマンド処理を明示的に実装し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> ます。

  次のセクションでは、これらのタスクを実行する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [相互運用機能アセンブリを使用してコマンドの状態を確認する](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)

 VSPackage がどのコマンドをサポートしているか、および現在有効になっているかどうかを IDE に通知する方法について説明します。

- [相互運用機能アセンブリのコマンドコントラクト](../../extensibility/internals/command-contracts-in-interop-assemblies.md)

 相互運用機能アセンブリを使用してコマンドを実装するすべての Vspackage で使用される基本的なコマンドコントラクトの定義を提供します。

- [コマンドの実装](../../extensibility/internals/command-implementation.md)

 VSPackage がコマンドを実装する方法の概要について説明します。

- [相互運用機能アセンブリコマンドハンドラーの登録](../../extensibility/internals/registering-interop-assembly-command-handlers.md)

 VSPackage がコマンドハンドラーを提供することを IDE に通知するために必要なレジストリエントリについて説明します。

## <a name="related-sections"></a>関連項目
- [コマンドの可用性](../../extensibility/internals/command-availability.md)

 使用できる VSPackage コマンドと、それらを処理するオブジェクトを決定するために IDE によって使用される条件について説明します。

- [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 コマンドサポートを使用する UI を作成する方法の詳細について説明 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。

- [Vspackage でのコマンドルーティング](../../extensibility/internals/command-routing-in-vspackages.md)

 オブジェクトを適切なコマンド要求に関連付けるために使用されるプロセスの概要です。
