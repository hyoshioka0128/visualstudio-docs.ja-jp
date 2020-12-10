---
title: '方法: サービスを取得する |Microsoft Docs'
description: さまざまな機能にアクセスするために Visual Studio サービスを取得する方法について説明します。 ほとんどのサービスは、VSPackage を使用して取得できます。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0a8f97900f1d400f3208a24ccc45ff9bbd774aeb
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994083"
---
# <a name="how-to-get-a-service"></a>方法: サービスを取得する

多くの場合、さまざまな機能にアクセスするために Visual Studio サービスを取得する必要があります。 一般に、Visual Studio サービスには、使用できる1つ以上のインターフェイスが用意されています。 ほとんどのサービスは VSPackage から取得できます。

から派生 <xref:Microsoft.VisualStudio.Shell.Package> し、正しく配置されているすべての VSPackage は、任意のグローバルサービスを要求できます。 クラスは `Package` を実装するため <xref:System.IServiceProvider> 、から派生するすべての VSPackage `Package` もサービスプロバイダーになります。

Visual Studio は、を読み込むと <xref:Microsoft.VisualStudio.Shell.Package> 、 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 初期化中にオブジェクトをメソッドに渡し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> ます。 これは、 *サイト設定* VSPackage と呼ばれます。 クラスは、 `Package` このサービスプロバイダーをラップし、 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> サービスを取得するためのメソッドを提供します。

## <a name="getting-a-service-from-an-initialized-vspackage"></a>初期化された VSPackage からのサービスの取得

1. すべての Visual Studio 拡張機能は、拡張機能アセットを含む VSIX デプロイプロジェクトから開始されます。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]という名前の VSIX プロジェクトを作成 `GetServiceExtension` します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[ **新しいプロジェクト** ] ダイアログで見つけることができます。

2. 次に、 **Getservicecommand** という名前のカスタムコマンド項目テンプレートを追加します。 [**新しい項目の追加**] ダイアログで、[ **Visual C#** の  >  **機能拡張**] にアクセスし、[**カスタムコマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を *GetServiceCommand.cs* に変更します。 カスタムコマンドを作成する方法の詳細については、「[メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

3. *GetServiceCommand.cs* で、メソッドの本体を削除 `MenuItemCommand` し、次のコードを追加します。

   ```csharp
   IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
   if (activityLog == null) return;
   System.Windows.Forms.MessageBox.Show("Found the activity log service.");

   ```

    このコードは、SVsActivityLog サービスを取得し、それをインターフェイスにキャストします。これを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> アクティビティログに書き込むことができます。 例については、「 [方法: アクティビティログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. 実験用インスタンスの [ **ツール** ] メニューで、[ **Getservicecommand の呼び出し** ] ボタンを探します。 このボタンをクリックすると、[**アクティビティログサービスが見つかりまし** た] というメッセージボックスが表示されます。

## <a name="getting-a-service-from-a-tool-window-or-control-container"></a>ツールウィンドウまたはコントロールコンテナーからサービスを取得する

場合によっては、配置されていないツールウィンドウまたはコントロールコンテナーからサービスを取得する必要があります。そうしないと、必要なサービスがわからないサービスプロバイダーが配置されていることがあります。 たとえば、コントロール内からアクティビティログに書き込むことができます。

静的メソッドは、 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> から派生したすべての VSPackage が配置されるときに初期化される、キャッシュされたサービスプロバイダーに依存し <xref:Microsoft.VisualStudio.Shell.Package> ます。

VSPackage コンストラクターは VSPackage が配置される前に呼び出されるため、通常、グローバルサービスは VSPackage コンストラクター内からは使用できません。 回避策については、「 [方法: サービスのトラブルシューティング](../extensibility/how-to-troubleshoot-services.md) 」を参照してください。

ツールウィンドウまたはその他の非 VSPackage 要素でサービスを取得する方法の例を次に示します。

```csharp
IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="getting-a-service-from-the-dte-object"></a>DTE オブジェクトからサービスを取得する

また、オブジェクトからサービスを取得することもでき <xref:EnvDTE.DTEClass> ます。 ただし、VSPackage から、または静的メソッドを呼び出すことによって、DTE オブジェクトをサービスとして取得する必要があり <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> ます。

DTE オブジェクトはを実装し <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> ます。これを使用すると、を使用してサービスを照会でき <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> ます。

ここでは、DTE オブジェクトからサービスを取得する方法について説明します。

```csharp
// Start with the DTE object, for example: 
// using EnvDTE;
// DTE dte = (DTE)GetService(typeof(DTE));

ServiceProvider sp = new ServiceProvider((Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);
if (sp != null)
{
    IVsActivityLog log = sp.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log != null)
    {
        System.Windows.Forms.MessageBox.Show("Found the activity log service.");
    }
}
```

## <a name="see-also"></a>こちらもご覧ください

- [方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)
- [サービスを使用して提供する](../extensibility/using-and-providing-services.md)
- [サービスの基本事項](../extensibility/internals/service-essentials.md)
