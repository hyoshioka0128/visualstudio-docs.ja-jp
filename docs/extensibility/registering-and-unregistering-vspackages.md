---
title: Vspackage | の登録と登録解除Microsoft Docs
description: 使用する属性や、pkgdef ファイルなど、Vspackage の登録と登録解除について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9b60844826387c2807eedcb47fe24c11a58af80f
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97862871"
---
# <a name="register-and-unregister-vspackages"></a>Vspackage の登録と登録解除
属性を使用して VSPackage を登録しますが、

## <a name="register-a-vspackage"></a>VSPackage を登録する
 属性を使用して、マネージ Vspackage の登録を制御できます。 すべての登録情報は、 *pkgdef* ファイルに含まれています。 ファイルベースの登録の詳細については、「 [Createpkgdef ユーティリティ](../extensibility/internals/createpkgdef-utility.md)」を参照してください。

 次のコードは、標準の登録属性を使用して VSPackage を登録する方法を示しています。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]
public sealed class BasicPackage : Package
{
    // ...
}
```

## <a name="unregister-an-extension"></a>拡張機能の登録解除
 さまざまな Vspackage を実験していて、実験用インスタンスから削除する必要がある場合は、 **Reset** コマンドを実行するだけで済みます。 コンピューターのスタートページで **Visual Studio の実験用インスタンスをリセット** するか、コマンドラインから次のコマンドを実行します。

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp
```

 Visual Studio の開発インスタンスにインストールした拡張機能をアンインストールする場合は、[ツール] [   >  **拡張機能と更新プログラム**] にアクセスし、拡張機能を見つけて、[**アンインストール**] をクリックします。

 何らかの理由で、拡張機能のアンインストールでこれらのメソッドのいずれも成功しない場合は、次のようにコマンドラインから VSPackage アセンブリの登録を解除できます。

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg" /unregister <pathToVSPackage assembly>
```

<a name="using-a-custom-registration-attribute-to-register-an-extension"></a>

## <a name="use-a-custom-registration-attribute-to-register-an-extension"></a>カスタム登録属性を使用して拡張機能を登録する

場合によっては、拡張機能の新しい登録属性を作成する必要があります。 登録属性を使用して、新しいレジストリキーを追加したり、既存のキーに新しい値を追加したりすることができます。 新しい属性はから派生する必要があり、 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> メソッドとメソッドをオーバーライドする必要があり <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> ます。

### <a name="create-a-custom-attribute"></a>カスタム属性を作成する

次のコードは、新しい登録属性を作成する方法を示しています。

```csharp
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]
public class CustomRegistrationAttribute : RegistrationAttribute
{
}
```

 は、属性 <xref:System.AttributeUsageAttribute> クラスで、属性が関連するプログラム要素 (クラス、メソッドなど)、複数回使用できるかどうか、および継承できるかどうかを指定するために使用されます。

### <a name="create-a-registry-key"></a>レジストリキーを作成する

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

### <a name="create-a-new-value-under-an-existing-registry-key"></a>既存のレジストリキーの下に新しい値を作成する

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

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
