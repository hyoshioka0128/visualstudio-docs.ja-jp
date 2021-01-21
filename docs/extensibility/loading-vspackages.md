---
title: Vspackage | を読み込んでいますMicrosoft Docs
description: パフォーマンスを向上させるために使用される遅延読み込みなど、Visual Studio での Vspackage の読み込みについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 0aeab78a2f64be2df6f601ad8ed224f13071eb8c
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/17/2020
ms.locfileid: "97616105"
---
# <a name="load-vspackages"></a>Load Vspackage
Vspackage は、機能が必要な場合にのみ、Visual Studio に読み込まれます。 たとえば、VSPackage は、Visual Studio がプロジェクトファクトリまたは VSPackage が実装するサービスを使用するときに読み込まれます。 この機能は遅延読み込みと呼ばれます。これは、パフォーマンス向上のために可能な場合に使用されます。

> [!NOTE]
> Visual Studio では、VSPackage を読み込まずに VSPackage が提供するコマンドなど、特定の VSPackage 情報を確認できます。

 Vspackage は、ソリューションが開いているときなど、特定のユーザーインターフェイス (UI) コンテキストで自動読み込みするように設定できます。 属性は、 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> このコンテキストを設定します。

### <a name="autoload-a-vspackage-in-a-specific-context"></a>特定のコンテキストで VSPackage を自動読み込みします。

- `ProvideAutoLoad`属性を VSPackage 属性に追加します。

    ```csharp
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID
    public class MyAutoloadedPackage : Package
    {. . .}
    ```

     <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>UI コンテキストとその GUID 値の一覧については、の列挙型フィールドを参照してください。

- メソッドにブレークポイントを設定 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> します。

- VSPackage をビルドし、デバッグを開始します。

- ソリューションを読み込むか、ソリューションを作成します。

     VSPackage は、ブレークポイントで読み込みと停止を行います。

## <a name="force-a-vspackage-to-load"></a>VSPackage を強制的に読み込む
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

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
