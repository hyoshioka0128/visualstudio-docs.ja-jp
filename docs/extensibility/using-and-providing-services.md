---
title: サービスの利用と提供 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], services
- Visual Studio, services
- services
ms.assetid: c0b415ba-b825-4da0-9faf-8a60a663e302
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8741d8d66af96ad4c6abea44b238393a34c5aa95
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698739"
---
# <a name="using-and-providing-services"></a>サービスの使用と提供
サービスは、2 つの VSPackages 間のコントラクトです。 1 つの VSPackage は、別の VSPackage が使用するインターフェイスの特定のセットを提供します。 たとえば、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]読み込<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>む VSPackage にサービスを提供します。 このサービスは<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>、アクティビティ ログへの書き込みに使用できるインターフェイスを提供します。 詳細については、「方法[: アクティビティ ログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

 VSPackage は、インターフェイスを使用して独自の<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService>サービスを提供できます。

 Visual Studio には、次のような重要なサービスが用意されています。

|IDE サービス|説明|
|-----------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|基本機能、VSPackages、およびレジストリを扱う IDE サービスへのアクセスを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|ツールやドキュメント ウィンドウの作成機能など、IDE のウィンドウと UI に関連する基本的な機能を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|プロジェクトの列挙、新しいプロジェクトの作成、プロジェクトの変更の監視など、ソリューションに関連する基本的な機能を提供します。|

## <a name="in-this-section"></a>このセクションの内容
- [サービスの必需品](../extensibility/internals/service-essentials.md)Visual Studio サービスの重要な要素を示します。

- [方法 : サービスを取得する](../extensibility/how-to-get-a-service.md)サービスを要求 (使用) する方法について説明します。

- [方法 : サービスを提供する](../extensibility/how-to-provide-a-service.md)サービスを提供する方法について説明します。

- [方法 : 非同期の Visual Studio サービスを提供する](../extensibility/how-to-provide-an-asynchronous-visual-studio-service.md)非同期サービスを提供する方法について説明します。

- [方法 : サービスのトラブルシューティング](../extensibility/how-to-troubleshoot-services.md)一般的な問題について説明し、それらの問題に対する解決策を示します。

## <a name="related-sections"></a>関連項目
- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)
