---
title: ユーザーインターフェイスを更新しています |Microsoft Docs
description: VSPackage に新しいコマンドを実装した後に、ユーザーインターフェイスを更新するコードを追加する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: fae228b3fab1e25f92c02da2512abdd78edda0db
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97716030"
---
# <a name="updating-the-user-interface"></a>ユーザー インターフェイスの更新
コマンドを実装したら、新しいコマンドの状態を使用してユーザーインターフェイスを更新するコードを追加できます。

 一般的な Win32 アプリケーションでは、コマンドセットを継続的にポーリングできます。また、個々のコマンドの状態は、ユーザーが表示するときに調整できます。 ただし、シェルで [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ホストできる vspackage の数に制限はありません。そのため、広範なポーリングによって応答性が低下する可能性があります。特に、マネージコードと COM 間の相互運用機能アセンブリ間でのポーリングです。

### <a name="to-update-the-ui"></a>UI を更新するには

1. 次のいずれかの操作を実行します。

    - <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> メソッドを呼び出します。

         次のように、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> サービスからインターフェイスを取得でき <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> ます。

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

         のパラメーター <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> が0以外 () の場合、 `TRUE` 更新は同期的に、直ちに実行されます。 `FALSE`適切なパフォーマンスを維持するために、このパラメーターにはゼロ () を渡すことをお勧めします。 キャッシュを回避する場合は、 `DontCache` vsct ファイルでコマンドを作成するときにフラグを適用します。 それでも、フラグは慎重に使用するか、パフォーマンスが低下する可能性があります。 コマンドフラグの詳細については、 [コマンドフラグ要素](../extensibility/command-flag-element.md) のドキュメントを参照してください。

    - ウィンドウでインプレースアクティブ化モデルを使用して ActiveX コントロールをホストする Vspackage では、メソッドを使用する方が便利な場合があり <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> ます。 インターフェイスの <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> メソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> とインターフェイスのメソッドは機能的に <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> 同等です。 どちらの場合も、環境はすべてのコマンドの状態を再クエリします。 通常、更新プログラムはすぐには実行されません。 代わりに、アイドル時間まで更新が遅延されます。 シェルは、良好なパフォーマンスを維持するために、コマンドの状態をキャッシュします。 キャッシュを回避する場合は、 `DontCache` vsct ファイルでコマンドを作成するときにフラグを適用します。 ただし、パフォーマンスが低下する可能性があるため、フラグは慎重に使用してください。

         インターフェイスを取得するに <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> `QueryInterface` は、オブジェクトでメソッドを呼び出す <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> か、またはサービスからインターフェイスを取得し <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> ます。

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [実装](../extensibility/internals/command-implementation.md)
