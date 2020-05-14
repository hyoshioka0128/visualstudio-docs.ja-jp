---
title: '方法 : サービスを提供する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 60cae5e8048a0234114e1f9e7d97728e26ee40f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710771"
---
# <a name="how-to-provide-a-service"></a>方法: サービスを提供する
VS パッケージは、他の VS パッケージを使用できるサービスを提供できます。 サービスを提供するには、VSPackage は Visual Studio でサービスを登録し、サービスを追加する必要があります。

 クラス<xref:Microsoft.VisualStudio.Shell.Package>は、 と<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider><xref:System.ComponentModel.Design.IServiceContainer>の両方を実装します。 <xref:System.ComponentModel.Design.IServiceContainer>には、必要に応じてサービスを提供するコールバック メソッドが含まれています。

 サービスの詳細については、「[サービスの基本](../extensibility/internals/service-essentials.md)事項」を参照してください。

> [!NOTE]
> VSPackage がアンロードされる間、Visual Studio は、VSPackage が提供するすべてのサービス要求が配信されるまで待機します。 これらのサービスに対する新しい要求は許可されません。 アンロード時にサービスを<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A>取り消すメソッドを明示的に呼び出してはいけません。

## <a name="implement-a-service"></a>サービスの実装

1. VSIX プロジェクト (**ファイル** > **新しい** > **プロジェクト** > **の Visual C#** > **拡張機能** > **VSIX プロジェクト**) を作成します。

2. VSPackage をプロジェクトに追加します。 **ソリューション エクスプローラー**でプロジェクト ノードを選択し、[**新しい項目** > の**追加** > **] Visual C# アイテム** > **機能拡張** > **Visual Studio パッケージ**] をクリックします。

3. サービスを実装するには、次の 3 つのタイプを作成する必要があります。

   - サービスを記述するインターフェイス。 これらのインターフェイスの多くは空です、つまりメソッドがありません。

   - サービス インターフェイスを記述するインターフェイス。 このインターフェイスには、実装するメソッドが含まれています。

   - サービスとサービス インターフェイスの両方を実装するクラス。

     次の例は、3 つの型の基本的な実装を示しています。 サービス クラスのコンストラクターは、サービス プロバイダーを設定する必要があります。

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

### <a name="register-a-service"></a>サービスの登録

1. サービスを登録するには、サービス<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>を提供する VSPackage に を追加します。 たとえば次のようになります。

    ```csharp
    [ProvideService(typeof(SMyService))]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [Guid(VSPackage1.PackageGuidString)]
    public sealed class VSPackage1 : Package
    {. . . }
    ```

     この属性は、Visual Studio に登録されます`SMyService`。

    > [!NOTE]
    > 同じ名前の別のサービスを置き換えるサービスを登録するには<xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute>、 . サービスのオーバーライドは 1 つのみ許可されることに注意してください。

### <a name="add-a-service"></a>サービスの追加

1. VSPackage 初期化子で、サービスを追加し、サービスを作成するコールバック メソッドを追加します。 メソッドに加える変更は<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>次のとおりです。

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);
    . . .
    }
    ```

2. サービスを作成して返すコールバック メソッドを実装します。

    ```csharp
    private object CreateService(IServiceContainer container, Type serviceType)
    {
        if (typeof(SMyService) == serviceType)
            return new MyService(this);
        return null;
    }
    ```

    > [!NOTE]
    > Visual Studio は、サービスを提供する要求を拒否できます。 別の VSPackage が既にサービスを提供している場合は、この処理を行います。

3. これで、サービスを取得して、そのメソッドを使用できます。 次の例は、初期化子でのサービスの使用を示していますが、サービスを使用する任意の場所でサービスを取得できます。

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);

        MyService myService = (MyService) this.GetService(typeof(SMyService));
        myService.Hello();
        string helloString = myService.Goodbye();

        base.Initialize();
    }
    ```

     の値`helloString`は"こんにちは"でなければなりません。

## <a name="see-also"></a>関連項目
- [方法: サービスを取得する](../extensibility/how-to-get-a-service.md)
- [サービスの使用と提供](../extensibility/using-and-providing-services.md)
- [サービスの必需品](../extensibility/internals/service-essentials.md)
