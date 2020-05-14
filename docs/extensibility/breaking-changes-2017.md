---
title: Visual Studio 2017 の拡張機能の変更を破る
titleSuffix: ''
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 54d5af60-0b44-4ae1-aa57-45aa03f89f3d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b3a04c925ef897171de51c73c90973a12c3b17d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739969"
---
# <a name="changes-in-visual-studio-2017-extensibility"></a>Visual Studio 2017 の機能拡張の変更点

Visual Studio 2017 は[、より高速で軽量な Visual Studio のインストール エクスペリエンス](https://devblogs.microsoft.com/visualstudio/faster-leaner-visual-studio-installer)を提供し、ユーザー システムに対する Visual Studio の影響を軽減し、インストールされているワークロードと機能に対する選択肢をユーザーに提供します。 これらの改善をサポートするために、拡張機能モデルに変更を加えました。 この記事では、これらの変更の技術的な詳細と、それらに対処するために何ができるかについて説明します。

> [!NOTE]
> 一部の情報は、ポイント・イン・タイムの実装の詳細であり、後で変更される可能性があります。

## <a name="changes-affecting-vsix-format-and-installation"></a>VSIX の形式とインストールに影響を与える変更

Visual Studio 2017 では、軽量インストール エクスペリエンスをサポートするために VSIX v3 (バージョン 3) 形式が導入されました。

VSIX 形式の変更点は次のとおりです。

* セットアップの前提条件の宣言。 Visual Studio の軽量で高速インストールを実現するために、インストーラーはユーザーに対して、より多くの構成オプションを提供するようになりました。 その結果、拡張機能に必要な機能とコンポーネントがインストールされるように、拡張機能は依存関係を宣言する必要があります。

  * Visual Studio 2017 インストーラーは、拡張機能のインストールの一部として、ユーザーに必要なコンポーネントを自動的に取得してインストールすることを提供します。
  * また、新しい VSIX v3 形式を使用して作成されていない拡張機能をインストールしようとしたときに、マニフェストでターゲット バージョン 15.0 としてマークされている場合でも、警告が表示されます。

* VSIX 形式の機能が強化されました。 並行インストールもサポートする Visual Studio の[影響を少ないインストール](https://devblogs.microsoft.com/visualstudio/anatomy-of-a-low-impact-visual-studio-install)で提供するために、ほとんどの構成データをシステム レジストリに保存し、Visual Studio 固有のアセンブリを GAC から移動しました。 また、VSIX 形式と VSIX インストール エンジンの機能も強化され、MSI や EXE ではなく、その機能を使用して、一部のインストールの種類に対して拡張機能をインストールできます。

新しい機能には次のものがあります。

* 指定した Visual Studio インスタンスへの登録。
* [拡張フォルダ](set-install-root.md)の外へのインストール
* プロセッサ アーキテクチャの検出。
* 言語で区切られた言語パックへの依存。
* [NGEN サポートを使用](ngen-support.md)したインストール :

## <a name="build-an-extension-for-visual-studio-2017"></a>Visual Studio 2017 の拡張機能をビルドします。

新しい VSIX v3 マニフェスト形式の作成のためのデザイナー ツールは、Visual Studio 2017 で利用できます。 デザイナー ツールの使用、または VSIX v3 拡張機能を開発するためのプロジェクトとマニフェストの手動更新の詳細については、付属のドキュメント「[方法: Visual Studio 2017 に機能拡張プロジェクトを移行](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)する」を参照してください。

## <a name="change-visual-studio-user-data-path"></a>変更: ビジュアル スタジオのユーザー データ パス

以前は、各コンピューターに存在できる Visual Studio の各メジャー リリースのインストールは 1 つだけでした。 Visual Studio 2017 のサイド バイ サイド インストールをサポートするために、ユーザーのコンピューターに Visual Studio の複数のユーザー データ パスが存在する場合があります。

Visual Studio のプロセス内で実行されているコードは、Visual Studio 設定マネージャーを使用するように更新する必要があります。 Visual Studio プロセスの外部で実行されるコードは、[ここでのガイダンスに従って](locating-visual-studio.md)、特定の Visual Studio インストールのユーザー パスを見つけることができます。

## <a name="change-global-assembly-cache-gac"></a>変更: グローバル アセンブリ キャッシュ (GAC)

ほとんどの Visual Studio コア アセンブリは、GAC にインストールされなくなりました。 Visual Studio プロセスで実行されているコードが、実行時に必要なアセンブリを見つけることができるように、次の変更が行われました。

> [!NOTE]
> [INSTALLDIR] は、Visual Studio のインストール ルート ディレクトリを参照してください。 *VSIXInstaller.exe*は自動的にこの値を設定しますが、カスタム配置コードを記述するには[、Visual Studio の検索](locating-visual-studio.md)を参照してください。

* GAC にのみインストールされたアセンブリ:

  これらのアセンブリは<em>、[インストールディレクトリ]\Common7\IDE、*[INSTALLDIR]\Common7\IDE\\*パブリックアセンブリ</em>、または *[INSTALLDIR]\Common7\IDE\プライベートアセンブリの*下にインストールされます。 これらのフォルダーは、Visual Studio プロセスのプローブ パスの一部です。

* 非プローブ パスと GAC にインストールされたアセンブリ:

  * GAC のコピーがセットアップから削除されました。
  * アセンブリのコード ベース エントリを指定するために *.pkgdef*ファイルが追加されました。

    次に例を示します。

    ```
    [$RootKey$\RuntimeConfiguration\dependentAssembly\codeBase\{UniqueGUID}]
    "name"="AssemblyName" "codeBase"="$PackageFolder$\AssemblyName.dll"
    "publicKeyToken"="Public Key Token"
    "culture"="neutral"
    "version"=15.0.0.0
    ```

    実行時に、Visual Studio pkgdef サブシステムは、これらのエントリを Visual Studio プロセスのランタイム構成ファイル *([VSAPPDATA]\devenv.exe.config)* に要素として[`<codeBase>`](/dotnet/framework/configure-apps/file-schema/runtime/codebase-element)マージします。 これは、プローブ パスを使用して検索を回避するため、Visual Studio プロセスでアセンブリを検索する場合に推奨される方法です。

### <a name="reacting-to-this-breaking-change"></a>この壊れた変化に反応する

* 拡張機能が Visual Studio プロセス内で実行されている場合は、次の手順を実行します。

  * コードは Visual Studio のコア アセンブリを見つけることができます。
  * 必要に応じて *、.pkgdef*ファイルを使用してアセンブリへのパスを指定することを検討してください。

* 拡張機能が Visual Studio プロセスの外部で実行されている場合は、次の手順を実行します。

  構成ファイルまたはアセンブリリゾルバーを使用して、Visual Studio コア アセンブリを探し、[<em>インストールディレクトリ]\Common7\IDE、*[\*インストールディレクトリ]\Common7\IDE\パブリック アセンブリ</em>、または *[INSTALLDIR]\Common7\Ide\PrivateAssembly*を探し出す方法を検討してください。

## <a name="change-reduce-registry-impact"></a>変更: レジストリへの影響を軽減する

### <a name="global-com-registration"></a>グローバル COM 登録

* 以前は、Visual Studio では、ネイティブ COM 登録をサポートするために、多くのレジストリ キーをHKEY_CLASSES_ROOTおよびHKEY_LOCAL_MACHINEハイブにインストールしました。 この影響を排除するために、Visual Studio では[COM コンポーネントの登録フリーアクティベーションを使用するようになりました](https://msdn.microsoft.com/library/ms973913.aspx)。
* その結果、%ProgramFiles(x86)%\共通ファイル\マイクロソフト共有\MSEnvの下のほとんどのTLB / OLB / DLLファイルは、Visual Studioによってデフォルトでインストールされなくなりました。 これらのファイルは[INSTALLDIR]の下にインストールされ、Visual Studio ホスト プロセスで使用される、対応する登録フリー COM マニフェストが使用されます。
* その結果、Visual Studio COM インターフェイスのグローバル COM 登録に依存する外部コードでは、これらの登録が見つかりません。 Visual Studio プロセス内で実行されるコードには違いは表示されません。

### <a name="visual-studio-registry"></a>ビジュアル スタジオ レジストリ

* 以前は、Visual Studio では、多くのレジストリ キーがシステムの**HKEY_LOCAL_MACHINE****にインストール**され、Visual Studio 固有のキーの下にハイブHKEY_CURRENT_USER。

  * **HKLM\ソフトウェア\マイクロソフト\VisualStudio\{バージョン}**: MSI インストーラーとコンピューターごとの拡張機能によって作成されたレジストリ キー。
  * **HKCU\ソフトウェア\マイクロソフト\VisualStudio\{バージョン}**: ユーザー固有の設定を格納するために Visual Studio によって作成されたレジストリ キー。
  * **HKCU\ソフトウェア\マイクロソフト\VisualStudio\{バージョン}_Config**: 上記の Visual Studio HKLM キーのコピーと、拡張子によって *.pkgdef*ファイルからマージされたレジストリ キー。

* レジストリへの影響を軽減するために、Visual Studio では[RegLoadAppKey](/windows/desktop/api/winreg/nf-winreg-regloadappkeya)関数を使用して *、[VSAPPDATA]\privateregistry.bin*の下のプライベート バイナリ ファイルにレジストリ キーを格納するようになりました。 システム レジストリに残っている Visual Studio 固有のキーの数はごく少数です。
* Visual Studio プロセス内で実行されている既存のコードには影響はありません。 Visual Studio は、HKCU Visual Studio 固有のキーの下のすべてのレジストリ操作をプライベート レジストリにリダイレクトします。 他のレジストリの場所への読み取りと書き込みは、引き続きシステム レジストリを使用します。
* 外部コードは、Visual Studio のレジストリ エントリのこのファイルから読み込む必要があります。

### <a name="react-to-this-breaking-change"></a>この画期的な変化に反応する

* 外部コードは、COM コンポーネントの登録フリーアクティベーションを使用するように変換する必要があります。
* 外部コンポーネントは[、ここでのガイダンスに従って](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup)Visual Studio の場所を見つけることができます。
* 外部コンポーネントは、Visual Studio のレジストリ キーを直接読み書きするのではなく[、外部設定マネージャー](/dotnet/api/microsoft.visualstudio.settings.externalsettingsmanager)を使用することをお勧めします。
* 拡張機能が使用しているコンポーネントが、登録のための別の手法を実装しているかどうかを確認します。 たとえば、デバッガー拡張機能は、新しい[msvsmon JSON ファイル COM 登録](migrate-debugger-COM-registration.md)を利用できる可能性があります。
