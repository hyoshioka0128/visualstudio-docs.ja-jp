---
title: '方法: サービスを提供する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 565a8a91797c826b6419dc5a8488d7d3baf9cddc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841716"
---
# <a name="how-to-provide-a-service"></a>方法: サービスを提供する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage は、他の Vspackage が使用できるサービスを提供できます。 サービスを提供するには、VSPackage がサービスを Visual Studio に登録し、サービスを追加する必要があります。  
  
 <xref:Microsoft.VisualStudio.Shell.Package>クラスは、との両方を実装し <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> <xref:System.ComponentModel.Design.IServiceContainer> ます。 <xref:System.ComponentModel.Design.IServiceContainer> 要求時にサービスを提供するコールバックメソッドを格納します。  
  
 サービスの詳細については、「 [Service Essentials](../extensibility/internals/service-essentials.md) 」を参照してください。  
  
> [!NOTE]
> VSPackage がアンロードされるとき、Visual Studio は、VSPackage が提供するサービスのすべての要求が配信されるまで待機します。 これらのサービスに対して新しい要求を行うことはできません。 メソッドを明示的に呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A> アンロード時にサービスを取り消すことはできません。  
  
#### <a name="implementing-a-service"></a>サービスの実装  
  
1. VSIX プロジェクトを作成します ([ファイル]、[新規作成]、[プロジェクト]、[Visual C#]、[Extensiblity]、[**Vsix プロジェクト**])。  
  
2. VSPackage をプロジェクトに追加します。 **ソリューションエクスプローラー**でプロジェクトノードを選択し、[追加]、[新しい項目]、[Visual C# 項目]、[機能拡張]、[ **visual Studio パッケージ**] の順にクリックします。  
  
3. サービスを実装するには、次の3種類を作成する必要があります。  
  
   - サービスを説明するインターフェイス。 これらのインターフェイスの多くは空です。つまり、メソッドがありません。  
  
   - サービスインターフェイスを記述するインターフェイス。 このインターフェイスには、実装するメソッドが含まれています。  
  
   - サービスとサービスインターフェイスの両方を実装するクラス。  
  
     次の例は、3種類の基本的な実装を示しています。 サービスクラスのコンストラクターは、サービスプロバイダーを設定する必要があります。  
  
   ```csharp  
   public class MyService : SMyService, IMyService  
   {  
       private Microsoft.VisualStudio.OLE.Interop.IServiceProvider serviceProvider;  
       private string myString;  
       public MyService(Microsoft.VisualStudio.OLE.Interop.IServiceProvider sp)  
       {  
           Trace.WriteLine(  
                  "Constructing a new instance of MyService");  
           serviceProvider = sp;  
       }  
       public void Hello()  
       {  
           myString = "hello";  
       }  
       public string Goodbye()  
       {  
          return "goodbye";  
       }  
   }  
   public interface SMyService  
   {  
   }  
   public interface IMyService  
   {  
       void Hello();  
       string Goodbye();  
   }  
  
   ```  
  
### <a name="registering-a-service"></a>サービスの登録  
  
1. サービスを登録するには、 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> サービスを提供する VSPackage にを追加します。 たとえば次のようになります。  
  
    ```csharp  
    [ProvideService(typeof(SMyService))]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [Guid(VSPackage1.PackageGuidString)]  
    public sealed class VSPackage1 : Package  
    {. . . }  
    ```  
  
     この属性は `SMyService` 、Visual Studio に登録されます。  
  
    > [!NOTE]
    > 同じ名前の別のサービスを置き換えるサービスを登録するには、を使用し <xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute> ます。 サービスのオーバーライドは1つしか許可されないことに注意してください。  
  
### <a name="adding-a-service"></a>サービスの追加  
  
1. 1.  VSPackage 初期化子で、サービスを追加し、コールバックメソッドを追加してサービスを作成します。 メソッドに対して行う変更は <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 次のとおりです。  
  
    ```csharp  
    protected override void Initialize()  
    {  
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);  
  
        ((IServiceContainer)this).AddService(typeof(SMyService), callback);  
    . . .  
    }  
    ```  
  
2. サービスを作成して返す必要があるコールバックメソッドを実装します。または、作成できない場合は null を実装します。  
  
    ```  
    private object CreateService(IServiceContainer container, Type serviceType)  
    {  
        if (typeof(SMyService) == serviceType)  
            return new SMyService(this);  
        return null;  
    }  
    ```  
  
    > [!NOTE]
    > Visual Studio は、要求を拒否してサービスを提供できます。 これは、別の VSPackage が既にサービスを提供している場合に行います。  
  
3. これで、サービスを取得し、そのメソッドを使用できるようになりました。 これを初期化子に示しますが、サービスを使用する任意の場所でサービスを取得することができます。  
  
    ```csharp  
    protected override void Initialize()  
    {  
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);  
  
        ((IServiceContainer)this).AddService(typeof(SMyService), callback);  
  
        MyService myService = (MyService) this.GetService(typeof(SMyService));  
        myService.Hello();  
        string helloString = myService.myString;  
  
        base.Initialize();  
    }  
    ```  
  
     の値は `helloString` "Hello" にする必要があります。  
  
## <a name="see-also"></a>参照  
 [方法: サービスを取得する](../extensibility/how-to-get-a-service.md)   
 [サービスの使用と提供](../extensibility/using-and-providing-services.md)   
 [サービスの基本情報](../extensibility/internals/service-essentials.md)
