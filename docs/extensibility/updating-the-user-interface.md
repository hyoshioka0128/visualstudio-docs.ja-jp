---
title: ユーザーインターフェイスの更新 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, updating
- commands, updating UI
ms.assetid: 376e2f56-e7bf-4e62-89f5-3dada84a404b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1c51ae790eb35645fbe9aec5d9c422e1051aaa69
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698880"
---
# <a name="updating-the-user-interface"></a>ユーザー インターフェイスの更新
コマンドを実装した後、新しいコマンドの状態でユーザー インターフェイスを更新するコードを追加できます。

 一般的な Win32 アプリケーションでは、コマンド セットを継続的にポーリングでき、個々のコマンドの状態をユーザーが表示する際に調整できます。 ただし、シェルは[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]無制限の数の VSPackage をホストできるため、広範なポーリングは応答性を低下させる可能性があります。

### <a name="to-update-the-ui"></a>UI を更新するには

1. 次のいずれかの操作を実行します。

    - <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> メソッドを呼び出します。

         次<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>のように、サービスからインターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>取得できます。

        ```csharp
        void UpdateUI(Microsoft.VisualStudio.Shell.ServiceProvider sp)
        {
            IVsUIShell vsShell = (IVsUIShell)sp.GetService(typeof(IVsUIShell));
            if (vsShell != null)
            {
                int hr = vsShell.UpdateCommandUI(0);
                Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr);
            }
        }

        ```

         のパラメータ<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A>が 0 以外の場合`TRUE`( ) の場合、更新は同期的かつ即時に実行されます。 このパラメータのパフォーマンスを維持するために`FALSE`、このパラメータに 0 ( ) を渡すことをお勧めします。 キャッシュを回避する場合は、.vsct ファイルでコマンドを作成するときに`DontCache`フラグを適用します。 ただし、フラグを慎重に使用するか、パフォーマンスが低下する可能性があります。 コマンド フラグの詳細については、コマンド[フラグ要素](../extensibility/command-flag-element.md)のドキュメントを参照してください。

    - ウィンドウ内のインプレース アクティブ化モデルを使用して ActiveX コントロールをホストする VSPackages では、<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A>メソッドを使用する方が便利な場合があります。 インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A>の<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>メソッドと<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A><xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager>インターフェイスのメソッドは、機能的に同等です。 いずれの場合も、環境はすべてのコマンドの状態を再照会します。 通常、更新はすぐには実行されません。 代わりに、更新はアイドル時間まで遅延します。 シェルは、良好なパフォーマンスを維持するためにコマンドの状態をキャッシュします。 キャッシュを回避する場合は、.vsct ファイルでコマンドを作成するときに`DontCache`フラグを適用します。 ただし、パフォーマンスが低下する可能性があるため、このフラグは慎重に使用してください。

         オブジェクトの<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager>`QueryInterface`メソッドを呼び出すか、サービスからインターフェイスを取得することによって、インターフェイスを取得できることに<xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager>注意してください。 <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager>

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [実装](../extensibility/internals/command-implementation.md)
