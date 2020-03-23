---
title: VS パッケージの登録と登録解除 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 701700ba9d5c6db1e5858a2419e1b2c0fa950ae5
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301585"
---
# <a name="register-and-unregister-vspackages"></a>VS パッケージの登録と登録解除
VSPackage を登録するには属性を使用しますが、

## <a name="register-a-vspackage"></a>VS パッケージの登録
 属性を使用して、管理 VSPackages の登録を制御できます。 すべての登録情報は *.pkgdef*ファイルに含まれています。 ファイルベースの登録の詳細については、 [CreatePkgDef ユーティリティ](../extensibility/internals/createpkgdef-utility.md)を参照してください。

 次のコードは、VSPackage を登録する標準の登録属性を使用する方法を示しています。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]
public sealed class BasicPackage : Package
{
    // ...
}
```

## <a name="unregister-an-extension"></a>拡張機能の登録解除
 多くの異なる VSPackage を試していて、それらを実験用インスタンスから削除する場合は **、Reset**コマンドを実行するだけです。 コンピューターのスタート ページで**Visual Studio の実験用インスタンスのリセット**を探すか、コマンド ラインから次のコマンドを実行します。

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp
```

 Visual Studio の開発インスタンスにインストールした拡張機能をアンインストールする場合は、[**ツール** > **拡張機能と更新プログラム**] に移動し、拡張機能を見つけて [**アンインストール**] をクリックします。

 何らかの理由でこれらのメソッドのどちらも、拡張機能のアンインストールに成功しない場合は、次のようにコマンド ラインから VSPackage アセンブリの登録を解除できます。

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg" /unregister <pathToVSPackage assembly>
```

<a name="using-a-custom-registration-attribute-to-register-an-extension"></a>

## <a name="use-a-custom-registration-attribute-to-register-an-extension"></a>カスタム登録属性を使用して拡張機能を登録する

場合によっては、拡張機能の新しい登録属性を作成する必要があります。 登録属性を使用して、新しいレジストリ キーを追加したり、既存のキーに新しい値を追加したりできます。 新しい属性は から<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>派生する必要があり、<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A>メソッド<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A>と メソッドをオーバーライドする必要があります。

### <a name="create-a-custom-attribute"></a>カスタム属性を作成する

次のコードは、新しい登録属性を作成する方法を示しています。

```csharp
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]
public class CustomRegistrationAttribute : RegistrationAttribute
{
}
```

 <xref:System.AttributeUsageAttribute>属性クラスで使用され、属性が関係するプログラム要素 (クラス、メソッドなど)、複数回使用できるかどうか、および継承できるかどうかを指定します。

### <a name="create-a-registry-key"></a>レジストリ キーを作成する

次のコードでは、カスタム属性は、登録されている VSPackage のキーの下に**カスタム**サブキーを作成します。

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

### <a name="create-a-new-value-under-an-existing-registry-key"></a>既存のレジストリ キーの下に新しい値を作成する

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
