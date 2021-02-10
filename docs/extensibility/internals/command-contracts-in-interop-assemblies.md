---
title: 相互運用機能アセンブリのコマンドコントラクト |Microsoft Docs
description: IOleCommandTarget インターフェイスを使用してコマンドを処理するための基本的なコントラクトについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command handling with interop assemblies, command contracts
- interop assemblies, command contracts
ms.assetid: 57245708-f539-42dc-8963-2754a48f0189
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9ed9435f4f0618ee0c0f4bc47cdb21e2cbf92f77
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940126"
---
# <a name="command-contracts-in-interop-assemblies"></a>相互運用機能アセンブリのコマンドコントラクト
インターフェイスを使用してコマンドを処理するための基本的なコントラクトは、環境がメソッドを呼び出して、コマンドがサポートされているかどうかを判断し、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> サポートされている場合はその状態とテキストを判断することです。 次に、環境はメソッドを呼び出して <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> コマンドを実行します。

 メソッドは、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> すべてのコマンドで同じように処理されます。 必要に応じて (ドロップダウンリストを使用するなど)、さらに通信を行うには、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 適切なパラメーターを指定してメソッドを呼び出します。 これらのパラメーターの解釈は、指定されたコマンドによって異なります。

 コマンドターゲットが出力パラメーターの値を返す場合、呼び出し元は、割り当てられたリソースを常に解放する必要があります。 このパラメーターはバリアントであるため、variant をクリアするとリソースが解放されます。

 コマンドが階層ウィンドウ内で動作する必要がある場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> インターフェイスを使用する必要があります。 インターフェイスには同様の <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> コントラクトがあり、同様のメソッドとがあり <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> ます。

## <a name="see-also"></a>関連項目
- [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Vspackage でのコマンドルーティング](../../extensibility/internals/command-routing-in-vspackages.md)
- [コマンドの実装](../../extensibility/internals/command-implementation.md)
