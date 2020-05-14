---
title: 相互運用機能アセンブリのコマンド コントラクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command handling with interop assemblies, command contracts
- interop assemblies, command contracts
ms.assetid: 57245708-f539-42dc-8963-2754a48f0189
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4f20a4f479d62cd1b64c3b13ff6e1a949656a668
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709687"
---
# <a name="command-contracts-in-interop-assemblies"></a>相互運用機能アセンブリのコマンド コントラクト
<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>インターフェイスを介してコマンドを処理するための基本的なコントラクトは、環境が<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>メソッドを呼び出して、コマンドがサポートされているかどうかを判断し、サポートされている場合は、その状態とテキストを決定することです。 次に、環境は、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>コマンドを実行するメソッドを呼び出します。

 メソッド<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>は、すべてのコマンドで同じように処理されます。 さらに通信は、必要に応じて(例えば、ドロップダウンリストを使用して)、適切な<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>パラメータを用いてメソッドを呼び出すことによって管理される。 これらのパラメータの解釈は、指定されたコマンドによって異なります。

 コマンド・ターゲットが output パラメーターに値を戻す場合、呼び出し元は割り振られたリソースを解放する責任を常に負います。 このパラメータはバリアントであるため、バリアントをクリアするとリソースが解放されます。

 階層ウィンドウ内でコマンドを操作する必要がある場合は<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>、そのインターフェイスを使用する必要があります。 インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>には、同様の方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>と .

## <a name="see-also"></a>関連項目
- [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VS パッケージでのコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)
- [コマンドの実装](../../extensibility/internals/command-implementation.md)
