---
title: サービスの要点 |Microsoft Docs
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
ms.sourcegitcommit: 3154387056160bf4c36ac8717a7fdc0cd9faf3f9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78409722"
---
# <a name="service-essentials"></a>サービスの基本情報
サービスは、2つの Vspackage 間のコントラクトです。 VSPackage は、別の VSPackage が使用するインターフェイスの特定のセットを提供します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、他の Vspackage にサービスを提供する Vspackage のコレクションです。

 たとえば、SVsActivityLog サービスを使用して IVsActivityLog インターフェイスを取得することができます。このインターフェイスを使用して、アクティビティログに書き込むことができます。 詳細については、「[方法: アクティビティログを使用する](../../extensibility/how-to-use-the-activity-log.md)」を参照してください。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、登録されていない組み込みのサービスも用意されています。 Vspackage は、サービスのオーバーライドを提供することによって、組み込みサービスやその他のサービスを置き換えることができます。 サービスに対して許可されるサービスオーバーライドは1つだけです。

 サービスには探索できません。 そのため、使用するサービスのサービス識別子 (SID) を把握しておく必要があります。また、どのインターフェイスが提供するかを把握しておく必要があります。 この情報は、本サービスのリファレンスドキュメントに記載されています。

- サービスを提供する Vspackage は、サービスプロバイダーと呼ばれます。

- 他の Vspackage に提供されるサービスは、グローバルサービスと呼ばれます。

- それらを実装する VSPackage、または作成した任意のオブジェクトにのみ使用できるサービスは、ローカルサービスと呼ばれます。

- 他のパッケージによって提供される組み込みのサービスやサービスを置き換えるサービスは、サービスの上書きと呼ばれます。

- サービス、またはサービスの上書きは、要求時に読み込まれます。つまり、サービスプロバイダーは、提供されたサービスが別の VSPackage によって要求されたときに読み込まれます。

- オンデマンド読み込みをサポートするために、サービスプロバイダーはそのグローバルサービスを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]に登録します。 詳細については、「[方法: サービスを提供する](../../extensibility/how-to-provide-a-service.md)」を参照してください。

- サービスを取得した後、必要なインターフェイスを取得するには、 [QueryInterface](/cpp/atl/queryinterface) (アンマネージコード) またはキャスト (マネージコード) を使用します。次に例を示します。

  ```vb
  TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)
  ```

  ```csharp
  GetService(typeof(SVsActivityLog)) as IVsActivityLog;
  ```

- マネージコードは、その型によってサービスを参照します。一方、アンマネージコードは GUID によってサービスを参照します。

- VSPackage を読み込む [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] と、サービスプロバイダーが VSPackage に渡され、グローバルサービスへのアクセスが VSPackage に与えられます。 これは、VSPackage の "サイト設定" と呼ばれます。

- Vspackage は、作成するオブジェクトのサービスプロバイダーにすることができます。 たとえば、フォームは、カラーサービスの要求をそのフレームに送信する場合があります。これにより、要求が [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]に渡される可能性があります。

- 深い入れ子になっている、またはまったく配置されていないマネージオブジェクトは、グローバルサービスに直接アクセスするために <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> を呼び出すことができます。

<a name="how-to-use-getglobalservice"></a>

## <a name="use-getglobalservice"></a>GetGlobalService を使用する

場合によっては、配置されていないツールウィンドウまたはコントロールコンテナーからサービスを取得する必要があります。そうしないと、必要なサービスがわからないサービスプロバイダーが配置されていることがあります。 たとえば、コントロール内からアクティビティログに書き込むことができます。 これらのシナリオとその他のシナリオの詳細については、「[方法: サービスのトラブルシューティング](../../extensibility/how-to-troubleshoot-services.md)」を参照してください。

ほとんどの Visual Studio サービスは、静的 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> メソッドを呼び出すことによって取得できます。

<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> は、パッケージから派生した VSPackage が最初に配置されるときに初期化されるキャッシュされたサービスプロバイダーに依存します。 この条件が満たされていることを保証するか、null サービス用に準備する必要があります。

幸いにも、ほとんどの場合、<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> は正常に機能します。

- VSPackage が別の VSPackage だけを認識するサービスを提供する場合、サービスを要求する VSPackage は、サービスを提供する VSPackage が読み込まれる前に配置されます。

- ツールウィンドウが VSPackage によって作成された場合、ツールウィンドウが作成される前に VSPackage が配置されます。

- コントロールコンテナーが、VSPackage によって作成されたツールウィンドウによってホストされている場合、VSPackage はコントロールコンテナーが作成される前に配置されます。

### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>ツールウィンドウまたはコントロールコンテナー内からサービスを取得するには

- コンストラクター、ツールウィンドウ、またはコントロールコンテナーに次のコードを挿入します。

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

    このコードは、SVsActivityLog サービスを取得し、それを IVsActivityLog インターフェイスにキャストします。これを使用してアクティビティログに書き込むことができます。 例については、「[方法: アクティビティログを使用する](../../extensibility/how-to-use-the-activity-log.md)」を参照してください。

## <a name="see-also"></a>参照

- [使用可能なサービスの一覧](../../extensibility/internals/list-of-available-services.md)
- [サービスの使用と提供](../../extensibility/using-and-providing-services.md)
- [キャストと型変換](/dotnet/csharp/programming-guide/types/casting-and-type-conversions)
- [キャスト](/cpp/cpp/casting)