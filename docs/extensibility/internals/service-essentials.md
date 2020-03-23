---
title: サービスの基本 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, essentials
ms.assetid: fbe84ad9-efe1-48b1-aba3-b50b90424d47
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8817ca48ff0a3f44a973986a173e647ce89c662c
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301633"
---
# <a name="service-essentials"></a>サービスの基本情報
サービスは、2 つの VSPackages 間のコントラクトです。 1 つの VSPackage は、別の VSPackage が使用するインターフェイスの特定のセットを提供します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、他の VS パッケージにサービスを提供する VSPackages のコレクションです。

 たとえば、SVsActivityLog サービスを使用して IVsActivityLog インターフェイスを取得し、これを使用してアクティビティ ログに書き込むことができます。 詳細については、「方法[: アクティビティ ログを使用する](../../extensibility/how-to-use-the-activity-log.md)」を参照してください。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]また、登録されていない組み込みサービスも提供します。 VSPackage は、サービスのオーバーライドを提供することで、組み込みサービスやその他のサービスを置き換えることができます。 サービスのオーバーライドは、1 つのサービスに対してのみ許可されます。

 サービスには検出可能性がありません。 したがって、使用するサービスのサービス識別子 (SID) を知っている必要があり、サービスが提供するインターフェイスを知っている必要があります。 サービスのリファレンス ドキュメントでは、この情報が提供されます。

- サービスを提供する VS パッケージは、サービス プロバイダーと呼ばれます。

- 他の VSPackage に提供されるサービスは、グローバル サービスと呼ばれます。

- それらを実装する VSPackage、またはそれを実装するオブジェクトでのみ使用可能なサービスは、ローカル サービスと呼ばれます。

- 組み込みのサービスや他のパッケージが提供するサービスを置き換えるサービスは、サービスのオーバーライドと呼ばれます。

- サービス、またはサービスのオーバーライドは、要求に応じて読み込まれる、つまり、サービス プロバイダーは、提供するサービスが別の VSPackage によって要求されたときに読み込まれます。

- オンデマンド読み込みをサポートするために、サービス プロバイダはグローバル サービスを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]に登録します。 詳細については、「[方法 : サービスを提供する](../../extensibility/how-to-provide-a-service.md)」を参照してください。

- サービスを取得したら、次の例に示すように[、QueryInterface](/cpp/atl/queryinterface) (アンマネージ コード) またはキャスト (マネージ コード) を使用して、目的のインターフェイスを取得します。

  ```vb
  TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)
  ```

  ```csharp
  GetService(typeof(SVsActivityLog)) as IVsActivityLog;
  ```

- マネージ コードはサービスをその型で参照しますが、アンマネージ コードは GUID でサービスを参照します。

- VSPackage を読み込むとき[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、VSPackage にサービス プロバイダーを渡して、VSPackage にグローバル サービスへのアクセスを許可します。 これは VSPackage を "座っている" と呼ばれます。

- VSPackages は、作成するオブジェクトのサービス プロバイダーにすることができます。 たとえば、フォームがカラー サービスの要求をフレームに送信し、その要求を に渡す[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]場合があります。

- 深くネストされている、またはまったくサイト化されていないマネージ オブジェクトは、グローバル<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>サービスへの直接アクセスを必要とします。

<a name="how-to-use-getglobalservice"></a>

## <a name="use-getglobalservice"></a>サービスを使用します。

サイトが配置されていないツール ウィンドウまたはコントロール コンテナーからサービスを取得する必要がある場合や、必要なサービスを認識していないサービス プロバイダーに配置されている場合があります。 たとえば、コントロール内からアクティビティ ログに書き込む場合があります。 これらのシナリオおよびその他のシナリオの詳細については、「[方法 : サービスのトラブルシューティング 」を参照](../../extensibility/how-to-troubleshoot-services.md)してください。

静的<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>メソッドを呼び出すことによって、ほとんどの Visual Studio サービスを取得できます。

<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>パッケージから派生した VSPackage が初めてサイト化される場合に初期化されるキャッシュされたサービス プロバイダーに依存します。 この条件が満たされていることを保証するか、または NULL サービスに備える必要があります。

幸いなことに<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>、ほとんどの場合、正しく動作します。

- VSPackage が別の VSPackage にのみ既知のサービスを提供する場合、サービスを要求する VSPackage は、サービスを提供する VSPackage が読み込まれる前にサイト化されます。

- ツール ウィンドウが VSPackage によって作成された場合、VSPackage は、ツール ウィンドウが作成される前にサイト化されます。

- コントロール コンテナーが VSPackage によって作成されたツール ウィンドウによってホストされている場合、コントロール コンテナーが作成される前に、VSPackage が配置されます。

### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>ツール ウィンドウまたはコントロール コンテナー内からサービスを取得するには

- コンストラクター、ツール ウィンドウ、またはコントロール コンテナーに次のコードを挿入します。

    ```csharp
    IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
        if (log == null) return;
    ```

    ```vb
    Dim log As IVsActivityLog = TryCast(Package.GetGlobalService(GetType(SVsActivityLog)), IVsActivityLog)
    If log Is Nothing Then
        Return
    End If
    ```

    このコードは、SVsActivityLog サービスを取得し、アクティビティ ログへの書き込みに使用できる IVsActivityLog インターフェイスにキャストします。 例については、「方法[: アクティビティ ログを使用する」を参照してください。](../../extensibility/how-to-use-the-activity-log.md)

## <a name="see-also"></a>関連項目

- [使用可能なサービスの一覧](../../extensibility/internals/list-of-available-services.md)
- [サービスの使用と提供](../../extensibility/using-and-providing-services.md)
- [キャストと型変換](/dotnet/csharp/programming-guide/types/casting-and-type-conversions)
- [キャスト](/cpp/cpp/casting)