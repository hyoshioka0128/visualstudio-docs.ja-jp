---
title: '方法 : 機能拡張プロジェクトを Visual Studio 2017 に移行する |マイクロソフトドキュメント'
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 8ca07b00-a3ff-40ab-b647-c0a93b55e86a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: b0cae0261b185ee08400e5f3d25735634663f54a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710979"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2017"></a>方法: 拡張機能プロジェクトを Visual Studio 2017 に移行する

このドキュメントでは、拡張機能プロジェクトを Visual Studio 2017 にアップグレードする方法について説明します。 プロジェクト ファイルを更新する方法を説明するだけでなく、拡張機能マニフェスト バージョン 2 (VSIX v2) から新しいバージョン 3 VSIX マニフェスト形式 (VSIX v3) にアップグレードする方法についても説明します。

## <a name="install-visual-studio-2017-with-required-workloads"></a>必要なワークロードを含む Visual Studio 2017 のインストール

インストールに次のワークロードが含まれていることを確認します。

* .NET デスクトップ開発
* Visual Studio 拡張機能の開発

## <a name="open-vsix-solution-in-visual-studio-2017"></a>VSIX ソリューションを開く 2017

すべての VSIX プロジェクトでは、Visual Studio 2017 へのメジャー バージョンの一方向アップグレードが必要です。

プロジェクト ファイル (たとえば **.csproj)* が更新されます。

* 最小ビジュアルスタジオバージョン - 15.0 に設定されました
* 古いツールバージョン (以前に存在する場合) - 14.0 に設定されるようになりました

## <a name="update-the-microsoftvssdkbuildtools-nuget-package"></a>パッケージを更新します。

> [!Note]
> ソリューションが Microsoft.VSSDK.BuildTools NuGet パッケージを参照していない場合は、この手順をスキップできます。

新しい VSIX v3 (バージョン 3) 形式で拡張機能をビルドするには、ソリューションを新しい VSSDK ビルド ツールを使用してビルドする必要があります。 これは Visual Studio 2017 と共にインストールされますが、VSIX v2 拡張機能は NuGet を使用して古いバージョンへの参照を保持している可能性があります。 その場合は、ソリューションの Microsoft.VSSDK.BuildTools NuGet パッケージの更新プログラムを手動でインストールする必要があります。

への参照を更新するには、次の手順を実行します。

* ソリューションを右クリックし、[**ソリューションの NuGet パッケージの管理**] を選択します。
* [**更新]** タブに移動します。
* を選択**します**。
* **[更新]** をクリックします。

![VSSDK ビルド ツール](media/vssdk-build-tools.png)

## <a name="make-changes-to-the-vsix-extension-manifest"></a>VSIX 拡張機能マニフェストに変更を加える

拡張機能を実行するために必要なすべてのアセンブリがユーザーの Visual Studio のインストールに確実に含まれるようにするには、拡張機能マニフェスト ファイルですべての必須コンポーネントまたはパッケージを指定します。 ユーザーが拡張機能をインストールしようとすると、VSIXInstaller はすべての必須コンポーネントがインストールされているかどうかを確認します。 一部が見つからない場合は、拡張機能のインストール プロセスの一部として、不足しているコンポーネントをインストールするように求められます。

> [!Note]
> 少なくとも、すべての拡張機能は、前提条件として Visual Studio コア エディター コンポーネントを指定する必要があります。

* 拡張マニフェスト ファイル (通常は*ソース.拡張子.vsixmanifest*と呼ばれます) を編集します。
* 15.0 が含まれていることを確認します`InstallationTarget`。
* 必要なインストール前提条件を追加します (以下の例に示すように)。
  * インストールの前提条件としては、コンポーネント ID のみを指定することをお勧めします。
  * コンポーネント ID の識別方法については、このドキュメントの最後[のセクションを](#find-component-ids)参照してください。

例:

```xml
<PackageManifest>
 ...
    <Prerequisites>
        <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Component.DiagnosticTools" Version="[15.0.25814.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Shell.12.0" Version="[12.0]" />
    </Prerequisites>
 ...
</PackageManifest>
```

### <a name="option-use-the-designer-to-make-changes-to-the-vsix-extension-manifest"></a>オプション: デザイナーを使用して VSIX 拡張機能マニフェストを変更する

マニフェスト XML を直接編集する代わりに、マニフェスト デザイナーの新しい **[必須コンポーネント**] タブを使用して、必須コンポーネントを選択すると、XML が更新されます。

> [!Note]
> マニフェスト デザイナーでは、現在の Visual Studio インスタンスにインストールされているコンポーネント (ワークロードまたはパッケージではない) のみを選択できます。 現在インストールされていないワークロード、パッケージ、またはコンポーネントの前提条件を追加する必要がある場合は、マニフェスト XML を直接編集します。

* *ファイルを*開きます。
* [**前提条件]** タブを選択し、[**新規]** ボタンを押します。

   ![VSIX マニフェスト デザイナー](media/vsix-manifest-designer.png)

* [**新しい前提条件の追加]** ウィンドウが開きます。

   ![vsix の前提条件を追加する](media/add-vsix-prerequisite.png)

* **[名前**]のドロップダウンをクリックし、必要な前提条件を選択します。
* 必要に応じてバージョンを更新します。

   > [!Note]
   > version フィールドには、現在インストールされているコンポーネントのバージョンがあらかじめ入力され、コンポーネントの次のメジャー バージョンまでの範囲が設定されます (ただし、コンポーネントの次のメジャー バージョンは含まれません)。

   ![roslyn の前提条件を追加する](media/add-roslyn-prerequisite.png)

* **[OK]** をクリックします。

## <a name="update-debug-settings-for-the-project"></a>プロジェクトのデバッグ設定を更新します。

Visual Studio の実験用インスタンスで拡張機能をデバッグする場合は、**デバッグ** > **開始アクション**のプロジェクト設定に、Visual Studio 2017 インストールの*devenv.exe*ファイルに設定された **[開始] 外部プログラム:** 値が設定されていることを確認します。

次のようになります: *C:\プログラム ファイル (x86)\マイクロソフト ビジュアル スタジオ\2017\エンタープライズ\コモン7\IDE\devenv.exe*

![外部プログラムを起動する](media/start-external-program.png)

> [!Note]
> デバッグ開始アクションは、通常 *、.csproj.user*ファイルに格納されます。 このファイルは通常 *、.gitignore*ファイルに含まれているので、ソース管理にコミットすると、通常は他のプロジェクト ファイルと共に保存されません。 そのため、ソース管理からソリューションを最新の位置に引き出した場合、プロジェクトの開始アクションに値が設定されていない可能性があります。 Visual Studio 2017 で作成された新しい VSIX プロジェクトには、現在の Visual Studio インストール ディレクトリを指す既定値を使用して作成された *.csproj.user*ファイルが含まれます。 ただし、VSIX v2 拡張機能を移行する場合は *、.csproj.user*ファイルには、以前の Visual Studio バージョンのインストール ディレクトリへの参照が含まれている可能性があります。 **デバッグ** > **開始アクション**の値を設定すると、拡張機能をデバッグしようとすると、適切な Visual Studio の実験用インスタンスを起動できます。

## <a name="check-that-the-extension-builds-correctly-as-a-vsix-v3"></a>拡張機能が正しくビルドされることを確認します (VSIX v3 として)

* VSIX プロジェクトをビルドします。
* 生成された VSIX を解凍します。
  * 既定では、VSIX ファイルは *[YourCustomExtension] .vsix*として*ビン/デバッグ**またはビン/リリース*内に配置されます。
  * 内容を簡単に表示するには *、.vsix*の名前を *.zip*に変更します。
* 3 つのファイルが存在するかどうかを確認します。
  * *拡張.vsix マニフェスト*
  * *マニフェスト.json*
  * *カタログ.json*

## <a name="check-when-all-required-prerequisites-are-installed"></a>必要な前提条件がすべてインストールされている場合に確認する

必要なすべての必須コンポーネントがインストールされているコンピューターに VSIX が正常にインストールされることをテストします。

> [!Note]
> 拡張機能をインストールする前に、Visual Studio のすべてのインスタンスをシャットダウンしてください。

拡張機能のインストールを試みます。

* ビジュアルスタジオ2017について

![VSIX インストーラーの Visual Studio 2017](media/vsixinstaller-vs-2017.png)

* オプション: 以前のバージョンの Visual Studio を確認します。
  * 下位互換性を証明します。
  * Visual Studio 2012、ビジュアル スタジオ 2013、Visual Studio 2015 で動作する必要があります。
* オプション: VSIX インストーラーバージョン チェッカーがバージョンの選択肢を提供していることを確認します。
  * 以前のバージョンの Visual Studio がインストールされている場合に含まれます。
  * Visual Studio 2017 が含まれています。

Visual Studio が最近開いた場合、次のようなダイアログ ボックスが表示される場合があります。

![vs 実行中のプロセス](media/vs-running-processes.png)

プロセスがシャットダウンするまで待つか、タスクを手動で終了します。 プロセスは、リストされた名前で検索するか、または括弧内にリストされている PID を使用して見つけることができます。

> [!Note]
> これらのプロセスは、Visual Studio のインスタンスの実行中に自動的にシャットダウンされません。 コンピューター上のすべての Visual Studio インスタンス (他のユーザーのインスタンスを含む) をシャットダウンしたことを確認してから、再試行を続行します。

## <a name="check-when-missing-the-required-prerequisites"></a>必要な前提条件がない場合に確認する

* 上記の前提条件 (上記) で定義されているすべてのコンポーネントを含まない Visual Studio 2017 のコンピューターに拡張機能をインストールしようとします。
* インストールが不足しているコンポーネントを識別し、VSIXInstaller の前提条件として一覧表示することを確認します。
* 注: 拡張機能を使用してインストールする必要がある前提条件がある場合は、標高が必要になります。

![vsix インストーラーに前提条件がありません](media/vsixinstaller-missing-prerequisite.png)

## <a name="decide-on-components"></a>コンポーネントの決定

依存関係を検索すると、1 つの依存関係が複数のコンポーネントにマップされる場合があります。 どの依存関係を必須コンポーネントとして指定する必要があるかを判断するには、拡張機能と同様の機能を持つコンポーネントを選択し、ユーザーと、インストールした可能性が最も高いコンポーネントの種類やインストールを気にしないコンポーネントも検討することをお勧めします。 また、必要な前提条件が、拡張機能の実行を可能にする最低限の条件のみを満たし、追加機能の場合は特定のコンポーネントが検出されない場合は休止状態になる方法で拡張機能を構築することをお勧めします。

さらにガイダンスを提供するために、いくつかの一般的な拡張タイプと推奨される前提条件を特定しました。

拡張機能の種類 | 表示名 | id
--- | --- | ---
エディター | Visual Studio のコア エディター | Microsoft.VisualStudio.Component.CoreEditor
ロスリン | C# および Visual Basic | Microsoft.VisualStudio.Component.Roslyn.LanguageServices
WPF | Managed Desktop Workload コア | Microsoft.VisualStudio.Component.ManagedDesktop.Core
デバッガー | Just-In-Time デバッガー | Microsoft.VisualStudio.Component.Debugger.JustInTime

## <a name="find-component-ids"></a>コンポーネント ID の検索

Visual Studio 製品で並べ替えられたコンポーネントの一覧は[、Visual Studio 2017 のワークロードとコンポーネント ID](/visualstudio/install/workload-and-component-ids?view=vs-2019)にあります。 マニフェストの前提条件 ID にこれらのコンポーネント ID を使用します。

どのコンポーネントに特定のバイナリが含まれているかわからない場合は、[コンポーネント -> バイナリ マッピング スプレッドシート](https://aka.ms/vs2017componentid-binaries)をダウンロードします。

### <a name="vs2017-componentbinarymappingxlsx"></a>を 2017-コンポーネントバイナリマッピング.xlsx

Excel シートには、**コンポーネント名、コンポーネント** **ID**、**バージョン**、バイナリ **/ファイル名**の 4 つの列があります。  フィルタを使用して、特定のコンポーネントやバイナリを検索できます。

すべての参照について、まずコア エディター (Microsoft.VisualStudio.Component.CoreEditor) コンポーネントに含まれるものを確認します。  少なくとも、コア エディター コンポーネントをすべての拡張機能の前提条件として指定する必要があります。 コア エディターに含まれていない参照のうち、**バイナリ /ファイル名**セクションにフィルターを追加して、これらの参照のサブセットを持つコンポーネントを検索します。

例 :

* デバッガー拡張機能があり、プロジェクトに*VSDebugEng.dll*および*VSDebug.dll*への参照があることを知っている場合は、[**バイナリ/ ファイル名]** ヘッダーのフィルター ボタンをクリックします。  "VSDebugEng.dll" を検索し *、[OK]* を選択します。  次に **、バイナリ /ファイル名**ヘッダーのフィルタボタンをもう一度クリックして、「VSDebug.dll」を検索します。  [フィルタする**現在の選択を追加する**] チェック ボックスをオンにし **、[OK]** を選択します。  ここで **、コンポーネント名**を見て、拡張機能の種類に最も関連するコンポーネントを見つけます。 この例では、Just-In-Time デバッガーを選択し、それを vsixmanifest に追加します。
* プロジェクトでデバッガー要素が処理される場合は、フィルター検索ボックスで "debugger" を検索して、その名前にデバッガーが含まれているコンポーネントを確認できます。

## <a name="specify-a-visual-studio-2017-release"></a>Visual Studio 2017 リリースの指定

たとえば、拡張機能で Visual Studio 2017 の特定のバージョンが必要な場合は、15.3 でリリースされた機能に依存し、VSIX**インストール ターゲット**でビルド番号を指定する必要があります。 たとえば、リリース 15.3 のビルド番号は '15.0.26730.3' です。 番号を構築するためのリリースのマッピングは、[ここ を参照してください](../install/visual-studio-build-numbers-and-release-dates.md)。 リリース番号 '15.3' を使用すると、正しく動作しません。

拡張に 15.3 以上が必要な場合は **、InstallationTarget バージョン**を [15.0.26730.3, 16.0:

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```
