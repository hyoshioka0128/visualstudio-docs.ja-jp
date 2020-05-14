---
title: VS パッケージを読み込む |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, loading
ms.assetid: f4c3dcea-5051-4065-898f-601269649d92
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b1c221bf06ef3b7e37e2afc1856f3e54fe5ad95e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702959"
---
# <a name="load-vspackages"></a>VS パッケージを読み込む
VS パッケージは、その機能が必要な場合にのみ、Visual Studio に読み込まれます。 たとえば、VSPackage を実装するプロジェクト ファクトリまたはサービスを使用する場合、VSPackage が読み込まれます。 この機能は遅延読み込みと呼ばれ、パフォーマンスを向上させるために可能な限り使用されます。

> [!NOTE]
> Visual Studio は、VSPackage を読み込まずに、VSPackage が提供するコマンドなどの特定の VSPackage 情報を決定できます。

 VSPackage は、特定のユーザー インターフェイス (UI) コンテキストで、たとえばソリューションが開いているときに自動読み込むように設定できます。 属性<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>は、このコンテキストを設定します。

### <a name="autoload-a-vspackage-in-a-specific-context"></a>特定のコンテキストで VSPackage を自動読み込む

- `ProvideAutoLoad` VSPackage 属性に属性を追加します。

    ```csharp
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID
    public class MyAutoloadedPackage : Package
    {. . .}
    ```

     UI コンテキストとその GUID<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>値の一覧については、列挙されたフィールドを参照してください。

- メソッドにブレークポイントを設定<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>します。

- VSPackage をビルドし、デバッグを開始します。

- ソリューションを読み込むか、ソリューションを作成します。

     VSPackage は、ブレークポイントで読み込みと停止します。

## <a name="force-a-vspackage-to-load"></a>VS パッケージを強制的に読み込む
 状況によっては、VSPackage が別の VSPackage を強制的に読み込む必要があります。 たとえば、軽量の VSPackage は、CMDUI コンテキストとして使用できないコンテキストで大きな VSPackage を読み込む可能性があります。

 このメソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackage%2A>使用して、強制的に VSPackage を読み込むことができます。

- 別の VSPackage<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>を強制的に読み込む VSPackage のメソッドにこのコードを挿入します。

    ```csharp
    IVsShell shell = GetService(typeof(SVsShell)) as IVsShell;
    if (shell == null) return;

    IVsPackage package = null;
    Guid PackageToBeLoadedGuid =
        new Guid(Microsoft.PackageToBeLoaded.GuidList.guidPackageToBeLoadedPkgString);
    shell.LoadPackage(ref PackageToBeLoadedGuid, out package);

    ```

     VSPackage が初期化されると、強制的`PackageToBeLoaded`に読み込まれます。

     VSPackage 通信には強制読み込みを使用しないでください。 代わりに[使用してサービスを提供](../extensibility/using-and-providing-services.md)します。

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
