---
title: Vspackage | を読み込んでいますMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, loading
ms.assetid: f4c3dcea-5051-4065-898f-601269649d92
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e20caff476e116ad59430692719bdbbe22c4914c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841700"
---
# <a name="loading-vspackages"></a>VSPackage の読み込み
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Vspackage は、機能が必要な場合にのみ、Visual Studio に読み込まれます。 たとえば、VSPackage は、Visual Studio がプロジェクトファクトリまたは VSPackage が実装するサービスを使用するときに読み込まれます。 この機能は遅延読み込みと呼ばれます。これは、パフォーマンス向上のために可能な場合に使用されます。  
  
> [!NOTE]
> Visual Studio では、VSPackage を読み込まずに VSPackage が提供するコマンドなど、特定の VSPackage 情報を確認できます。  
  
 Vspackage は、ソリューションが開いているときなど、特定のユーザーインターフェイス (UI) コンテキストで自動読み込みするように設定できます。 属性は、 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> このコンテキストを設定します。  
  
### <a name="autoloading-a-vspackage-in-a-specific-context"></a>特定のコンテキストで VSPackage を自動読み込みします。  
  
- `ProvideAutoLoad`属性を VSPackage 属性に追加します。  
  
    ```csharp  
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID  
    public class MyAutoloadedPackage : Package  
    {. . .}  
    ```  
  
     <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>UI コンテキストとその GUID 値の一覧については、の列挙型フィールドを参照してください。  
  
- メソッドにブレークポイントを設定 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> します。  
  
- VSPackage をビルドし、デバッグを開始します。  
  
- ソリューションを読み込むか、ソリューションを作成します。  
  
     VSPackage は、ブレークポイントで読み込みと停止を行います。  
  
## <a name="forcing-a-vspackage-to-load"></a>VSPackage を強制的に読み込む  
 状況によっては、VSPackage が別の VSPackage を強制的に読み込む必要がある場合があります。 たとえば、簡易 VSPackage は、CMDUIContext として使用できないコンテキストで、より大きな VSPackage を読み込む場合があります。  
  
 メソッドを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackage%2A> 、VSPackage に強制的に読み込むことができます。  
  
- 次のコードを <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> VSPackage のメソッドに挿入して、別の VSPackage を強制的に読み込みます。  
  
    ```csharp  
    IVsShell shell = GetService(typeof(SVsShell)) as IVsShell;  
    if (shell == null) return;  
  
    IVsPackage package = null;  
    Guid PackageToBeLoadedGuid =   
        new Guid(Microsoft.PackageToBeLoaded.GuidList.guidPackageToBeLoadedPkgString);  
    shell.LoadPackage(ref PackageToBeLoadedGuid, out package);  
  
    ```  
  
     VSPackage が初期化されると、強制的 `PackageToBeLoaded` に読み込まれます。  
  
     VSPackage 通信には、強制読み込みを使用しないでください。 代わりに [、を使用してサービスを提供して](../extensibility/using-and-providing-services.md) ください。  
  
## <a name="using-a-custom-attribute-to-register-a-vspackage"></a>カスタム属性を使用して VSPackage を登録する  
 場合によっては、拡張機能の新しい登録属性を作成する必要があります。 登録属性を使用して、新しいレジストリキーを追加したり、既存のキーに新しい値を追加したりすることができます。 新しい属性はから派生する必要があり、 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> メソッドとメソッドをオーバーライドする必要があり <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> ます。  
  
## <a name="creating-a-registry-key"></a>レジストリキーの作成  
 次のコードでは、カスタム属性によって、登録されている VSPackage のキーの下に **カスタム** サブキーが作成されます。  
  
```csharp  
public override void Register(RegistrationAttribute.RegistrationContext context)  
{  
    Key packageKey = null;  
    try  
    {   
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + @"}\Custom");  
        packageKey.SetValue("NewCustom", 1);  
    }  
    finally  
    {  
        if (packageKey != null)  
            packageKey.Close();  
    }  
}  
  
public override void Unregister(RegistrationContext context)  
{  
    context.RemoveKey(@"Packages\" + context.ComponentType.GUID + @"}\Custom");  
}  
  
```  
  
## <a name="creating-a-new-value-under-an-existing-registry-key"></a>既存のレジストリキーの下に新しい値を作成する  
 既存のキーにカスタム値を追加できます。 次のコードは、VSPackage 登録キーに新しい値を追加する方法を示しています。  
  
```csharp  
public override void Register(RegistrationAttribute.RegistrationContext context)  
{  
    Key packageKey = null;  
    try  
    {   
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + "}");  
        packageKey.SetValue("NewCustom", 1);  
    }  
    finally  
    {  
        if (packageKey != null)  
            packageKey.Close();  
                }  
}  
  
public override void Unregister(RegistrationContext context)  
{  
    context.RemoveValue(@"Packages\" + context.ComponentType.GUID, "NewCustom");  
}  
```  
  
## <a name="see-also"></a>参照  
 [VSPackages](../extensibility/internals/vspackages.md)
