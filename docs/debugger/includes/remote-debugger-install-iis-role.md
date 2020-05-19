---
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: 13ca035b01ec8af1277d70b3c792293a1af4687a
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149227"
---
ここでは、IIS の基本的な構成に関する手順のみを説明します。 詳細情報や Windows デスクトップ マシンへのインストールについては、[IIS への発行](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)に関する記事または「[ASP.NET 3.5 および ASP.NET 4.5 を使用する IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)」を参照してください。

Windows Server オペレーティング システムの場合は、**サーバー マネージャー**の **[管理]** リンクまたは **[ダッシュボード]** リンクから**役割と機能の追加**ウィザードを使用します。 **[サーバーの役割]** のステップで、 **[Web サーバー (IIS)]** チェック ボックスをオンにします。

![[サーバーの役割の選択] のステップで Web サーバー IIS の役割を選択します。](../media/remotedbg-server-roles-ws2012.png)

**[役割サービス]** のステップで、希望する IIS の役割サービスを選択するか、既定の役割サービスをそのまま使用します。 発行の設定と [Web 配置] を使用して配置を有効にする場合は、 **[IIS 管理スクリプトおよびツール]** が選択されていることを確認します。

確認のステップを経て Web サーバーの役割とサービスをインストールします。 Web サーバー (IIS) の役割をインストールした後、サーバーと IIS の再起動は必要ありません。