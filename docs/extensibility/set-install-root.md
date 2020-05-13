---
title: VSIX v3 を使用して拡張機能フォルダーの外部にインストールする |マイクロソフトドキュメント
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa2c7d97dda9bba139ec613b367eedbc6307848a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700180"
---
# <a name="install-outside-the-extensions-folder"></a>拡張機能フォルダー外でのインストール

Visual Studio 2017 および VSIX v3 (バージョン 3) 以降では、拡張機能の資産を拡張機能フォルダーの外部にインストールできます。 現在、次の場所は有効なインストール場所として有効になっています (ここで [INSTALLDIR] は Visual Studio インスタンスのインストール ディレクトリに割り当てられます)。

* [インストールディレクトリ]\MSBuild
* [インストールディレクトリ]\Xml\スキーマ
* [インストールディレクトリ]\コモン7\IDE\パブリックアセンブリ
* [インストールディレクトリ]\ライセンス
* [インストールディレクトリ]\コモン7\IDE\リファレンスアセンブリ
* [インストールディレクトリ]\コモン7\IDE\リモートデバッガ
* [インストールディレクトリ]\Common7\IDE\VC\VCターゲット (Visual Studio 2017 でのみサポートされ、Visual Studio 2019 以降では使用されなくなりました)

> [!NOTE]
> VSIX 形式では、Visual Studio のインストール フォルダー構造の外部にインストールすることはできません。 

これらのディレクトリへのインストールをサポートするには、VSIX を「インスタンスごとマシンごと」インストールする必要があります。 これは、extension.vsixmanifest デザイナーの 「すべてのユーザー」 チェックボックスをオンにすることで有効にできます。

![すべてのユーザーを確認する](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>インストールルートを設定する方法

インストール ディレクトリを設定するには、Visual Studio の **[プロパティ]** ウィンドウを使用します。 たとえば、プロジェクト参照の`InstallRoot`プロパティを上記の場所のいずれかに設定できます。

![ルート プロパティのインストール](media/install-root-properties.png)

これにより、VSIX プロジェクトの .csproj ファイル内の対応する`ProjectReference`プロパティにいくつかのメタデータが追加されます。

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

> [!NOTE]
> 必要に応じて、.csproj ファイルを直接編集できます。

## <a name="how-to-set-a-subpath-under-the-installroot"></a>インストールルートの下にサブパスを設定する方法

下のサブパス`InstallRoot`にインストールする場合は、`VsixSubPath`プロパティをプロパティと同じように`InstallRoot`設定します。 たとえば、プロジェクト参照の出力を '[INSTALLDIR]\MSBuild\MyCOMPANY\MySDK\1.0' にインストールするとします。 この操作は、プロパティ デザイナーで簡単に行うことができます。

![サブパスを設定する](media/set-subpath.png)

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

プロパティ デザイナーの変更は、プロジェクト参照以外にも適用されます。プロジェクト内の`InstallRoot`項目のメタデータも設定できます (上記と同じ方法を使用)。
