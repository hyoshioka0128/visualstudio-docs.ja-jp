---
title: VSIX v3 を使用した extensions フォルダー以外のインストール |Microsoft Docs
description: 拡張機能フォルダーの外部および有効な場所に Visual Studio SDK 拡張機能アセットをインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 73bfb963122762c3185a964826a11dca5e771717
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97716017"
---
# <a name="install-outside-the-extensions-folder"></a>拡張機能フォルダー外でのインストール

Visual Studio 2017 および VSIX v3 (バージョン 3) 以降では、拡張機能のアセットを extensions フォルダーの外部にインストールできます。 現在、次の場所は有効なインストール場所として有効になっています ([INSTALLDIR] は Visual Studio インスタンスのインストールディレクトリにマップされます)。

* [INSTALLDIR] \ MSBuild
* [INSTALLDIR] \ xmlnoschema
* [INSTALLDIR] \Common7\IDE\PublicAssemblies
* [INSTALLDIR] \ ライセンス
* [INSTALLDIR] \Common7\IDE\ReferenceAssemblies
* [INSTALLDIR] \Common7\IDE\RemoteDebugger
* [INSTALLDIR] \Common7\IDE\VC\VCTargets (Visual Studio 2017 でのみサポートされています。 Visual Studio 2019 以降では非推奨)

> [!NOTE]
> VSIX 形式では、Visual Studio インストールフォルダー構造の外部にインストールすることはできません。 

これらのディレクトリへのインストールをサポートするには、VSIX を "コンピューターごとにインスタンスごとに" インストールする必要があります。 これを有効にするには、source.extension.vsixmanifest デザイナーで [すべてのユーザー] チェックボックスをオンにします。

![すべてのユーザーを確認する](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>InstallRoot を設定する方法

インストールディレクトリを設定するには、Visual Studio の [ **プロパティ** ] ウィンドウを使用します。 たとえば、 `InstallRoot` プロジェクト参照のプロパティを上記のいずれかの場所に設定できます。

![ルートプロパティのインストール](media/install-root-properties.png)

これにより `ProjectReference` 、VSIX プロジェクトの .csproj ファイル内の対応するプロパティにいくつかのメタデータが追加されます。

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

> [!NOTE]
> 必要に応じて、.csproj ファイルを直接編集できます。

## <a name="how-to-set-a-subpath-under-the-installroot"></a>InstallRoot の下にサブパスを設定する方法

の下にあるサブパスにをインストールする場合は、プロパティと同様に `InstallRoot` プロパティを設定し `VsixSubPath` `InstallRoot` ます。 たとえば、プロジェクト参照の出力を ' [INSTALLDIR] \MSBuild\MyCompany\MySDK\1.0 ' にインストールする必要があるとします。 これは、プロパティデザイナーで簡単に実行できます。

![サブパスの設定](media/set-subpath.png)

対応する .csproj の変更は次のようになります。

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>追加情報

プロパティデザイナーの変更は、プロジェクト参照以外にも適用されます。 `InstallRoot` プロジェクト内の項目のメタデータも設定できます (上記と同じ方法を使用します)。
