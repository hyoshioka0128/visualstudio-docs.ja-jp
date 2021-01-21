---
title: Visual Studio 2017 の機能拡張における重大な変更
description: Visual Studio 2017 の機能拡張モデルに加えられた重大な変更の技術的な詳細と、それらに対処するための方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 54d5af60-0b44-4ae1-aa57-45aa03f89f3d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3121189b1d73543d2a01bbf0b149c6a98eab6909
ms.sourcegitcommit: 5027eb5c95e1d2da6d08d208fd6883819ef52d05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94973747"
---
# <a name="changes-in-visual-studio-2017-extensibility"></a>Visual Studio 2017 の拡張機能の変更点

Visual studio 2017 では、 [より高速で軽量な Visual studio インストールエクスペリエンス](https://devblogs.microsoft.com/visualstudio/faster-leaner-visual-studio-installer) が提供されます。これにより、ユーザーは、インストールされているワークロードと機能に対してより多くの選択肢を提供できるだけではありません。 これらの機能強化をサポートするために、いくつかの重大な変更を含め、拡張モデルを変更しました。 この記事では、これらの変更の技術的な詳細と、それらに対処するために実行できる操作について説明します。

> [!NOTE]
> 一部の情報は、特定の時点の実装の詳細であり、後で変更される可能性があります。

## <a name="changes-affecting-vsix-format-and-installation"></a>VSIX の形式とインストールに影響を与える変更

Visual Studio 2017 では、ライトウェイトインストールエクスペリエンスをサポートするために、VSIX v3 (バージョン 3) 形式が導入されました。

VSIX 形式の変更は次のとおりです。

* セットアップの前提条件の宣言。 軽量で、Visual Studio を迅速にインストールできるようにするために、インストーラーはより多くの構成オプションをユーザーに提供するようになりました。 そのため、拡張機能に必要な機能とコンポーネントがインストールされていることを確認するには、拡張機能に依存関係を宣言する必要があります。

  * Visual Studio 2017 インストーラーでは、拡張機能のインストールの一環として、ユーザーに必要なコンポーネントを取得してインストールするように自動的に提供されます。
  * 新しい VSIX v3 形式を使用してビルドされていない拡張機能をインストールしようとすると、ユーザーにも警告が表示されます。これは、バージョン15.0 のターゲットとしてマニフェストでマークされている場合でも同様です。

* VSIX 形式の機能が拡張されました。 サイドバイサイドインストールもサポートしている Visual Studio の [影響の少ないインストール](https://devblogs.microsoft.com/visualstudio/anatomy-of-a-low-impact-visual-studio-install) を実現するために、ほとんどの構成データをシステムレジストリに保存することなく、visual studio 固有のアセンブリを GAC から移動しました。 また、VSIX 形式と VSIX インストールエンジンの機能が向上しました。これにより、MSI や EXE を使用して、一部のインストールの種類の拡張機能をインストールすることができます。

新しい機能は次のとおりです。

* 指定された Visual Studio インスタンスに登録します。
* [Extensions フォルダー](set-install-root.md)の外にインストールします。
* プロセッサアーキテクチャの検出。
* 言語を区別した言語パックに依存します。
* [NGEN サポート](ngen-support.md)によるインストール。

## <a name="build-an-extension-for-visual-studio-2017"></a>Visual Studio 2017 の拡張機能をビルドする

新しい VSIX v3 マニフェスト形式を作成するためのデザイナーツールは、Visual Studio 2017 で使用できます。 「 [方法: 機能拡張プロジェクトを Visual Studio 2017 に移行](how-to-migrate-extensibility-projects-to-visual-studio-2017.md) する」を参照してください。デザイナーツールの使用方法や、プロジェクトとマニフェストを手動で更新して VSIX v3 拡張機能を開発する方法の詳細については、「」を参照してください。

## <a name="change-visual-studio-user-data-path"></a>変更: Visual Studio ユーザーデータパス

以前は、各コンピューターには、Visual Studio のメジャーリリースが1つだけインストールされていました。 Visual Studio 2017 のサイドバイサイドインストールをサポートするために、ユーザーのコンピューターに Visual Studio の複数のユーザーデータパスが存在する場合があります。

Visual studio のプロセス内で実行されているコードは、Visual Studio の設定マネージャーを使用するように更新する必要があります。 Visual Studio プロセスの外部で実行されているコードは、 [こちらのガイダンスに従って](locating-visual-studio.md)、特定の visual studio インストールのユーザーパスを見つけることができます。

## <a name="change-global-assembly-cache-gac"></a>変更: グローバルアセンブリキャッシュ (GAC)

ほとんどの Visual Studio コアアセンブリは、GAC にインストールされなくなりました。 次の変更は、Visual Studio プロセスで実行されるコードが実行時に必要なアセンブリを見つけることができるようにするために行われました。

> [!NOTE]
> 下の [INSTALLDIR] は、Visual Studio のインストールルートディレクトリを示しています。 *VSIXInstaller.exe* によって自動的に設定されますが、カスタムデプロイコードを記述するには、「 [Visual Studio の検索](locating-visual-studio.md)」を参照してください。

* GAC にのみインストールされたアセンブリ:

  これらのアセンブリは <em>、[INSTALLDIR] \Common7\IDE \* 、* [INSTALLDIR] \Common7\IDE\PublicAssemblies</em> または *[INSTALLDIR] \Common7\IDE\PrivateAssemblies* の下にインストールされるようになりました。 これらのフォルダーは、Visual Studio プロセスのプローブパスの一部です。

* 非プローブパスと GAC にインストールされたアセンブリ:

  * GAC のコピーがセットアップから削除されました。
  * アセンブリのコードベースエントリを指定するために、 *pkgdef* ファイルが追加されました。

    次に例を示します。

    ```
    [$RootKey$\RuntimeConfiguration\dependentAssembly\codeBase\{UniqueGUID}]
    "name"="AssemblyName" "codeBase"="$PackageFolder$\AssemblyName.dll"
    "publicKeyToken"="Public Key Token"
    "culture"="neutral"
    "version"=15.0.0.0
    ```

    実行時に、Visual Studio .pkgdef サブシステムは、これらのエントリを、要素として Visual Studio プロセスのランタイム構成ファイル ( *[Vsappdata] \devenv.exe.config*) にマージし [`<codeBase>`](/dotnet/framework/configure-apps/file-schema/runtime/codebase-element) ます。 これは、Visual Studio プロセスでアセンブリを検索するために推奨される方法です。プローブパスの検索が回避されるためです。

### <a name="reacting-to-this-breaking-change"></a>この重大な変更への対応

* 拡張機能が Visual Studio プロセス内で実行されている場合:

  * コードでは、Visual Studio のコアアセンブリを見つけることができます。
  * 必要に応じて、 *pkgdef* ファイルを使用してアセンブリへのパスを指定することを検討してください。

* 拡張機能が Visual Studio プロセス外で実行されている場合:

  構成ファイルまたはアセンブリリゾルバーを使用して <em>、[INSTALLDIR] \Common7\IDE \* 、* [INSTALLDIR] \Common7\IDE\PublicAssemblies</em> または *[INSTALLDIR] \Common7\IDE\PrivateAssemblies* の下で Visual Studio コアアセンブリを検索することを検討してください。

## <a name="change-reduce-registry-impact"></a>変更: レジストリの影響を軽減する

### <a name="global-com-registration"></a>グローバル COM 登録

* 以前は、Visual Studio では、ネイティブ COM 登録をサポートするために、多くのレジストリキーが HKEY_CLASSES_ROOT および HKEY_LOCAL_MACHINE ハイブにインストールされていました。 この影響を避けるために、Visual Studio では、 [COM コンポーネントの登録を不要にしたアクティベーション](/previous-versions/dotnet/articles/ms973913(v=msdn.10))が使用されるようになりました。
* その結果、既定では、Visual Studio によって、% ProgramFiles (x86)% \ Common .OLB v の下にあるほとんどの TLB//DLL ファイルがインストールされなくなりました。 これらのファイルは、Visual Studio ホストプロセスで使用される Registration-Free COM マニフェストと共に [INSTALLDIR] の下にインストールされるようになりました。
* その結果、Visual Studio COM インターフェイスのグローバル COM 登録に依存する外部コードは、これらの登録を見つけることができなくなります。 Visual Studio プロセス内で実行されているコードに違いはありません。

### <a name="visual-studio-registry"></a>Visual Studio レジストリ

* 以前は、visual Studio では、Visual studio 固有のキーの下に、システムの **HKEY_LOCAL_MACHINE** と **HKEY_CURRENT_USER** ハイブに多くのレジストリキーがインストールされていました。

  * **HKLM\Software\Microsoft\VisualStudio \{Version}**: MSI インストーラーおよびコンピューターごとの拡張機能によって作成されたレジストリキー。
  * **HKCU\Software\Microsoft\VisualStudio \{Version}**: ユーザー固有の設定を格納するために Visual Studio によって作成されたレジストリキー。
  * **HKCU\Software\Microsoft\VisualStudio \{バージョン} _Config**: 上の Visual STUDIO HKLM キーのコピーに加え、拡張子によって、 *pkgdef* ファイルからマージされたレジストリキーがあります。

* レジストリへの影響を軽減するために、Visual Studio では、 [Regloadappkey](/windows/desktop/api/winreg/nf-winreg-regloadappkeya) 関数を使用して、レジストリキーを *[vsappdata] \privateregistry.bin* の下のプライベートバイナリファイルに格納するようになりました。 システムレジストリに含まれる Visual Studio 固有のキーの数はごくわずかです。
* Visual Studio プロセス内で実行されている既存のコードは影響を受けません。 Visual Studio は、HKCU Visual Studio 固有のキーの下にあるすべてのレジストリ操作をプライベートレジストリにリダイレクトします。 他のレジストリの場所の読み取りと書き込みでは、システムレジストリが引き続き使用されます。
* 外部コードは、Visual Studio レジストリエントリのためにこのファイルの読み込みと読み取りを行う必要があります。

### <a name="react-to-this-breaking-change"></a>この重大な変更に対処する

* 外部コードは、COM コンポーネントの Registration-Free アクティベーションを使用するように変換する必要があります。
* 外部コンポーネントは、 [こちらのガイダンスに従って](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup)Visual Studio の場所を見つけることができます。
* 外部コンポーネントでは、Visual Studio レジストリキーを直接読み書きするのではなく、 [外部設定マネージャー](/dotnet/api/microsoft.visualstudio.settings.externalsettingsmanager) を使用することをお勧めします。
* 拡張機能が使用しているコンポーネントが、別の登録手法を実装していないかどうかを確認します。 たとえば、デバッガー拡張機能では、新しい [MSVSMON JSON ファイル COM 登録](migrate-debugger-COM-registration.md)を利用できます。