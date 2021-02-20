---
title: '方法: サービスを提供する |Microsoft Docs'
description: VSPackage は、他の Vspackage が使用できるサービスを提供できます。 VSPackage が Visual Studio にサービスを登録し、サービスを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7f16e05ecbd211652dbf5fb511211627a09137df
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952266"
---
# <a name="how-to-provide-a-service"></a>方法: サービスを提供する
VSPackage は、他の Vspackage が使用できるサービスを提供できます。 サービスを提供するには、VSPackage がサービスを Visual Studio に登録し、サービスを追加する必要があります。

 <xref:Microsoft.VisualStudio.Shell.Package>クラスは、との両方を実装し <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> <xref:System.ComponentModel.Design.IServiceContainer> ます。 <xref:System.ComponentModel.Design.IServiceContainer> 要求時にサービスを提供するコールバックメソッドを格納します。

 サービスの詳細については、「 [Service essentials](../extensibility/internals/service-essentials.md) 」を参照してください。

> [!NOTE]
> VSPackage がアンロードされるとき、Visual Studio は、VSPackage が提供するサービスのすべての要求が配信されるまで待機します。 これらのサービスに対して新しい要求を行うことはできません。 メソッドを明示的に呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A> アンロード時にサービスを取り消すことはできません。

## <a name="implement-a-service"></a>サービスを実装する

1. VSIX プロジェクトを作成します ([**ファイル**] [  >  **新しい**  >  **プロジェクト**] [  >  **Visual C#**] [拡張性] [  >    >  **vsix プロジェクト**])。

2. VSPackage をプロジェクトに追加します。 **ソリューションエクスプローラー** でプロジェクトノードを選択し、[**追加**] [  >  **新しい項目**] [  >  **visual C# 項目**] [拡張] [  >    >  **visual Studio パッケージ**] の順にクリックします。

3. サービスを実装するには、次の3種類を作成する必要があります。

   - サービスを説明するインターフェイス。 これらのインターフェイスの多くは空です。つまり、メソッドがありません。

   - サービスインターフェイスを記述するインターフェイス。 このインターフェイスには、実装するメソッドが含まれています。

   - サービスとサービスインターフェイスの両方を実装するクラス。

     次の例は、3つの型の基本的な実装を示しています。 サービスクラスのコンストラクターは、サービスプロバイダーを設定する必要があります。

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

### <a name="register-a-service"></a>サービスを登録する

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

### <a name="add-a-service"></a>サービスの追加

1. VSPackage 初期化子で、サービスを追加し、コールバックメソッドを追加してサービスを作成します。 メソッドに対して行う変更は <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 次のとおりです。

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);
    . . .
    }
    ```

2. サービスを作成して返す必要があるコールバックメソッドを実装します。または、作成できない場合は null を実装します。

    ```csharp
    private object CreateService(IServiceContainer container, Type serviceType)
    {
        if (typeof(SMyService) == serviceType)
            return new MyService(this);
        return null;
    }
    ```

    > [!NOTE]
    > Visual Studio は、要求を拒否してサービスを提供できます。 これは、別の VSPackage が既にサービスを提供している場合に行います。

3. これで、サービスを取得し、そのメソッドを使用できるようになりました。 次の例は、初期化子でサービスを使用する方法を示していますが、サービスを使用する任意の場所でサービスを取得できます。

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

     の値は `helloString` "Hello" にする必要があります。

## <a name="see-also"></a>関連項目
- [方法: サービスを取得する](../extensibility/how-to-get-a-service.md)
- [サービスを使用して提供する](../extensibility/using-and-providing-services.md)
- [サービスの基本事項](../extensibility/internals/service-essentials.md)
