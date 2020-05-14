---
title: '方法 : サービスを取得する |マイクロソフトドキュメント'
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e8e6f20eaa08d6bb7aaa0cc9e560856daa5959e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710959"
---
# <a name="how-to-get-a-service"></a>方法: サービスを取得する

多くの場合、さまざまな機能にアクセスするには、Visual Studio サービスを取得する必要があります。 一般に、Visual Studio サービスは、使用できる 1 つ以上のインターフェイスを提供します。 VSPackage からほとんどのサービスを取得できます。

から<xref:Microsoft.VisualStudio.Shell.Package>派生し、正しくサイト化された VSPackage は、グローバル サービスを要求できます。 クラスは`Package`<xref:System.IServiceProvider>を実装しているため、派生`Package`元の VSPackage もサービス プロバイダーです。

Visual Studio が<xref:Microsoft.VisualStudio.Shell.Package>読み込むとき、<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>初期化中に<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>メソッドにオブジェクトが渡されます。 これは VSPackage*の座りと*呼ばれます。 クラス`Package`はこのサービス プロバイダーをラップし、サービス<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>を取得するためのメソッドを提供します。

## <a name="getting-a-service-from-an-initialized-vspackage"></a>初期化された VSPackage からサービスを取得する

1. すべての Visual Studio 拡張機能は、拡張機能の資産を含む VSIX 配置プロジェクトで開始します。 という名前[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]`GetServiceExtension`の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログで見つけることができます。

2. 次に **、GetServiceCommand**という名前のカスタム コマンド項目テンプレートを追加します。 [**新しい項目の追加]** ダイアログで **、[Visual C#** > **の機能拡張**] に移動し、[**カスタム コマンド**] を選択します。 ウィンドウの下部にある [**名前]** フィールドで、コマンド ファイル名を*GetServiceCommand.cs*に変更します。 カスタム コマンドを作成する方法の詳細については、[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)

3. *GetServiceCommand.cs*で、メソッドの本体を`MenuItemCommand`削除し、次のコードを追加します。

   ```csharp
   IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
   if (activityLog == null) return;
   System.Windows.Forms.MessageBox.Show("Found the activity log service.");

   ```

    このコードは SVsActivityLog サービスを取得し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>インターフェイスにキャストします。 例については、「[方法: アクティビティ ログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. 実験用インスタンスの **[ツール**] メニューで **、[GetServiceCommand の呼び出し**] ボタンを見つけます。 このボタンをクリックすると、**アクティビティ ログ サービスが見つかりました**というメッセージ ボックスが表示されます。

## <a name="getting-a-service-from-a-tool-window-or-control-container"></a>ツール ウィンドウまたはコントロール コンテナーからのサービスの取得

サイトが配置されていないツール ウィンドウまたはコントロール コンテナーからサービスを取得する必要がある場合や、必要なサービスを認識していないサービス プロバイダーに配置されている場合があります。 たとえば、コントロール内からアクティビティ ログに書き込む場合があります。

静的<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>メソッドは、最初に派生した VSPackage がサイト化されたとき初期化されるキャッシュされたサービス<xref:Microsoft.VisualStudio.Shell.Package>プロバイダーに依存します。

VSPackage のコンストラクターは、VSPackage が配置される前に呼び出されるため、VSPackage コンストラクター内からグローバル サービスを使用できないのが一般的です。 回避策については[、「方法: サービスのトラブルシューティング](../extensibility/how-to-troubleshoot-services.md)」を参照してください。

ツール ウィンドウまたはその他の非 VSPackage 要素でサービスを取得する方法の例を次に示します。

```csharp
IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="getting-a-service-from-the-dte-object"></a>DTE オブジェクトからのサービスの取得

オブジェクトから<xref:EnvDTE.DTEClass>サービスを取得することもできます。 ただし、VsPackage から、または静的<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>メソッドを呼び出すことによって、サービスとして DTE オブジェクトを取得する必要があります。

DTE オブジェクトは、<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>を使用してサービスのクエリを実行するために使用<xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A>できる を実装します。

DTE オブジェクトからサービスを取得する方法を次に示します。

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

## <a name="see-also"></a>関連項目

- [方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)
- [サービスの使用と提供](../extensibility/using-and-providing-services.md)
- [サービスの必需品](../extensibility/internals/service-essentials.md)
