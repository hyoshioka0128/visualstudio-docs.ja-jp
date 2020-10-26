---
title: '方法: サービスを取得する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 46ef86b8cde506aad3e00aa6b5dbc6470c0087de
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204187"
---
# <a name="how-to-get-a-service"></a>方法: サービスを取得する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

多くの場合、さまざまな機能にアクセスするために Visual Studio サービスを取得する必要があります。 一般に、Visual Studio サービスには、使用できる1つ以上のインターフェイスが用意されています。 ほとんどのサービスは VSPackage から取得できます。  
  
 から派生 <xref:Microsoft.VisualStudio.Shell.Package> し、正しく配置されているすべての VSPackage は、任意のグローバルサービスを要求できます。 パッケージクラスはを実装しているため <xref:System.IServiceProvider> 、パッケージから派生したすべての VSPackage はサービスプロバイダーでもあります。  
  
 Visual Studio は、を読み込むと <xref:Microsoft.VisualStudio.Shell.Package> 、 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 初期化中にオブジェクトをメソッドに渡し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> ます。 これは、 *サイト設定* VSPackage と呼ばれます。 パッケージクラスは、このサービスプロバイダーをラップし、 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> サービスを取得するためのメソッドを提供します。  
  
## <a name="getting-a-service-from-an-initialized-vspackage"></a>初期化された VSPackage からのサービスの取得  
  
1. すべての Visual Studio 拡張機能は、拡張機能アセットを含む VSIX デプロイプロジェクトから開始されます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]という名前の VSIX プロジェクトを作成 `GetServiceExtension` します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。  
  
2. 次に、 **Getservicecommand**という名前のカスタムコマンド項目テンプレートを追加します。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[拡張機能** ] にアクセスし、[ **カスタムコマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を **GetServiceCommand.cs**に変更します。 カスタムコマンドを作成する方法の詳細については、「[メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。  
  
3. GetServiceCommand.cs で、MenuItemCommand メソッドの本体を削除し、次のコードを追加します。  
  
    ```csharp  
    IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
    if (activityLog == null) return;  
    System.Windows.Forms.MessageBox.Show("Found the activity log service.");  
  
    ```  
  
     このコードは、SVsActivityLog サービスを取得し、それをインターフェイスにキャストします。これを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> アクティビティログに書き込むことができます。 例については、「 [方法: アクティビティログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。  
  
4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。  
  
5. 実験用インスタンスの [ツール] メニューで、[ **GetServiceCommand の呼び出し** ] ボタンを探します。 このボタンをクリックすると、[**アクティビティログサービスが見つかりまし**た] というメッセージボックスが表示されます。  
  
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
  
## <a name="see-also"></a>参照  
 [方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)   
 [サービスの使用と提供](../extensibility/using-and-providing-services.md)   
 [サービスの基本情報](../extensibility/internals/service-essentials.md)
