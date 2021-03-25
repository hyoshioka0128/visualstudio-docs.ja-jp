---
title: 機能拡張プロジェクトを Visual Studio 2017 に移行する
titleSuffix: ''
description: 機能拡張プロジェクトを Visual Studio 2017 にアップグレードする方法と、拡張機能マニフェストバージョン2からバージョン3の VSIX マニフェストにアップグレードする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: how-to
ms.assetid: 8ca07b00-a3ff-40ab-b647-c0a93b55e86a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: d50624dc4c0d96c20323afb3c7d065121a4baacb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069973"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2017"></a>方法: 機能拡張プロジェクトを Visual Studio 2017 に移行する

このドキュメントでは、機能拡張プロジェクトを Visual Studio 2017 にアップグレードする方法について説明します。 プロジェクトファイルの更新方法について説明するだけでなく、拡張機能マニフェストバージョン 2 (VSIX v2) から新しいバージョン 3 VSIX マニフェスト形式 (VSIX v3) にアップグレードする方法についても説明します。

## <a name="install-visual-studio-2017-with-required-workloads"></a>必要なワークロードで Visual Studio 2017 をインストールする

インストールに次のワークロードが含まれていることを確認してください。

* .NET デスクトップ開発
* Visual Studio 拡張機能の開発

## <a name="open-vsix-solution-in-visual-studio-2017"></a>Visual Studio 2017 で VSIX ソリューションを開く

すべての VSIX プロジェクトで、Visual Studio 2017 への一方向のメジャーバージョンのアップグレードが必要になります。

プロジェクトファイル (たとえば、**.csproj*) が更新されます。

* MinimumVisualStudioVersion-15.0 に設定されるようになりました
* OldToolsVersion (既に存在する場合)-14.0 に設定されるようになりました

## <a name="update-the-microsoftvssdkbuildtools-nuget-package"></a>Microsoft の VSSDK NuGet パッケージを更新します

> [!Note]
> ソリューションが、Microsoft の VSSDK NuGet パッケージを参照していない場合は、この手順を省略できます。

新しい VSIX v3 (バージョン 3) 形式で拡張機能をビルドするには、新しい VSSDK ビルドツールを使用してソリューションをビルドする必要があります。 これは Visual Studio 2017 と共にインストールされますが、VSIX v2 拡張機能は NuGet 経由で古いバージョンへの参照を保持している可能性があります。 その場合は、ソリューションのために、Microsoft の VSSDK NuGet パッケージの更新プログラムを手動でインストールする必要があります。

NuGet の参照を更新するには、次のようにします。

* ソリューションを右クリックし、[ **ソリューションの NuGet パッケージの管理**] を選択します。
* [ **更新** ] タブに移動します。
* [ **Microsoft**] を選択します。
* **Update** を押します。

![VSSDK ビルドツール](media/vssdk-build-tools.png)

## <a name="make-changes-to-the-vsix-extension-manifest"></a>VSIX 拡張機能マニフェストに変更を加える

拡張機能を実行するために必要なすべてのアセンブリが Visual Studio のユーザーのインストールに確実に含まれるようにするには、拡張機能マニフェストファイルにすべての必須コンポーネントまたはパッケージを指定します。 ユーザーが拡張機能をインストールしようとすると、VSIXInstaller は、すべての前提条件がインストールされているかどうかを確認します。 一部が不足している場合は、拡張機能のインストールプロセスの一部として、不足しているコンポーネントをインストールするように求められます。

> [!Note]
> 少なくとも、すべての拡張機能で Visual Studio コアエディターコンポーネントを前提条件として指定する必要があります。

* 拡張機能マニフェストファイル (通常は *source.extension.vsixmanifest* と呼ばれます) を編集します。
* `InstallationTarget`15.0 が含まれていることを確認します。
* 次の例に示すように、必要なインストールの前提条件を追加します。
  * インストールの前提条件にはコンポーネント Id のみを指定することをお勧めします。
  * [コンポーネント id を識別する方法](#find-component-ids)については、このドキュメントの末尾にある「」を参照してください。

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

マニフェスト XML を直接編集するのではなく、マニフェストデザイナーの [新しい **必須コンポーネント** ] タブを使用して、前提条件を選択すると、XML が更新されます。

> [!Note]
> マニフェストデザイナーでは、現在の Visual Studio インスタンスにインストールされているコンポーネント (ワークロードまたはパッケージではない) のみを選択できます。 現在インストールされていないワークロード、パッケージ、またはコンポーネントの前提条件を追加する必要がある場合は、マニフェスト XML を直接編集します。

* *Source.extension.vsixmanifest [Design]* ファイルを開きます。
* [ **必須コンポーネント** ] タブを選択し、[ **新規** ] ボタンをクリックします。

   ![VSIX マニフェストデザイナー](media/vsix-manifest-designer.png)

* [ **新しい前提条件の追加** ] ウィンドウが開きます。

   ![vsix の前提条件の追加](media/add-vsix-prerequisite.png)

* [ **名前** ] のドロップダウンをクリックし、必要な前提条件を選択します。
* 必要に応じてバージョンを更新します。

   > [!Note]
   > [バージョン] フィールドには、現在インストールされているコンポーネントのバージョンがあらかじめ設定されています。範囲は、コンポーネントの次のメジャーバージョンまで (ただし、含まれません) になります。

   ![roslyn の前提条件の追加](media/add-roslyn-prerequisite.png)

* **[OK]** を押します。

## <a name="update-debug-settings-for-the-project"></a>プロジェクトのデバッグ設定を更新する

Visual studio の実験用インスタンスで拡張機能をデバッグする場合は、[**デバッグ** 開始] アクションのプロジェクト設定に、  >   visual studio 2017 のインストールの *devenv.exe* ファイルに設定された [**外部プログラムの開始**] の値が設定されていることを確認してください。

*C:\Program files (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\devenv.exe* のようになります。

![外部プログラムの開始](media/start-external-program.png)

> [!Note]
> デバッグの開始アクションは通常、 *.csproj* ファイルに格納されます。 通常、このファイルは、ファイルに含まれてい *ます。* そのため、ソース管理にコミットすると、通常は他のプロジェクトファイルと共に保存されません。 そのため、ソース管理からソリューションを新規にプルした場合、プロジェクトの開始アクションに値が設定されていない可能性があります。 Visual Studio 2017 で作成された新しい VSIX プロジェクトには、既定で現在の Visual Studio インストールディレクトリを指す *.csproj* ファイルが作成されます。 ただし、VSIX v2 拡張機能を移行する場合は、 *.csproj* ファイルに以前の Visual Studio バージョンのインストールディレクトリへの参照が含まれている可能性があります。 **デバッグ** 開始アクションの値を設定する  >  と、拡張機能をデバッグしようとしたときに、正しい Visual Studio の実験的なインスタンスを起動することができます。

## <a name="check-that-the-extension-builds-correctly-as-a-vsix-v3"></a>拡張機能が (VSIX v3 として) 正しくビルドされることを確認します。

* VSIX プロジェクトをビルドします。
* 生成された VSIX を解凍します。
  * 既定では、VSIX ファイルは *bin/Debug* または *bin/Release* の内部にあり、[お持ちの *customextension] .vsix* として存在します。
  * *.Vsix* の名前を *.zip* に変更して、内容を簡単に表示します。
* 次の3つのファイルが存在するかどうかを確認します。
  * *拡張子 source.extension.vsixmanifest*
  * *manifest.js*
  * *catalog.js*

## <a name="check-when-all-required-prerequisites-are-installed"></a>必要なすべての必須コンポーネントがインストールされていることを確認する

必要なすべての前提条件がインストールされているコンピューターに、VSIX が正常にインストールされていることをテストします。

> [!Note]
> 拡張機能をインストールする前に、Visual Studio のすべてのインスタンスをシャットダウンしてください。

拡張機能をインストールしようとしています:

* (Visual Studio 2017)

![Visual Studio 2017 の VSIX インストーラー](media/vsixinstaller-vs-2017.png)

* 省略可能: 以前のバージョンの Visual Studio について確認します。
  * 旧バージョンとの互換性を証明します。
  * Visual Studio 2012、Visual Studio 2013、Visual Studio 2015 で動作する必要があります。
* 省略可能: VSIX インストーラーバージョンチェッカーでバージョンを選択できることを確認します。
  * 以前のバージョンの Visual Studio が含まれています (インストールされている場合)。
  * Visual Studio 2017 が含まれています。

Visual Studio が最近開いた場合は、次のようなダイアログボックスが表示されることがあります。

![vs 実行プロセス](media/vs-running-processes.png)

プロセスがシャットダウンされるまで待つか、手動でタスクを終了します。 リストされた名前、またはかっこ内に列挙されている PID を使用して、プロセスを検索できます。

> [!Note]
> これらのプロセスは、Visual Studio のインスタンスの実行中は自動的にはシャットダウンされません。 コンピューター上の Visual Studio のすべてのインスタンス (他のユーザーからのものも含む) がシャットダウンされていることを確認してから、再試行を続けます。

## <a name="check-when-missing-the-required-prerequisites"></a>必要な前提条件が満たされていない場合にチェックします

* 前提条件で定義されているすべてのコンポーネント (上記を含む) が含まれていない Visual Studio 2017 を使用しているコンピューターに拡張機能をインストールしようとしています。
* インストールによって、不足しているコンポーネント/s が識別され、VSIXInstaller の前提条件として一覧表示されていることを確認します。
* 注: 拡張機能を使用して必須コンポーネントをインストールする必要がある場合は、昇格が必要です。

![vsixinstaller 不足の前提条件](media/vsixinstaller-missing-prerequisite.png)

## <a name="decide-on-components"></a>コンポーネントの決定

依存関係を検索するときに、1つの依存関係が複数のコンポーネントにマップされる可能性があることがわかります。 前提条件としてどのような依存関係を指定する必要があるかを判断するには、拡張機能と同様の機能を備えたコンポーネントを選択することをお勧めします。また、ユーザーと、インストールされている可能性のあるコンポーネントの種類やインストールが気になるコンポーネントの種類も考慮することをお勧めします。 また、拡張機能を構築することをお勧めします。必要な前提条件が満たされているのは、拡張機能の実行を許可する最小値のみであり、その他の機能については、特定のコンポーネントが検出されない場合に休止状態になります。

さらにガイダンスを提供するために、いくつかの一般的な拡張機能の種類と推奨される前提条件を確認しました。

拡張機能の種類 | 表示名 | id
--- | --- | ---
エディター | Visual Studio のコア エディター | Microsoft.VisualStudio.Component.CoreEditor
Roslyn | C# および Visual Basic | Microsoft.VisualStudio.Component.Roslyn.LanguageServices
WPF | Managed Desktop Workload コア | Microsoft.VisualStudio.Component.ManagedDesktop.Core
デバッガー | Just-In-Time デバッガー | Microsoft.VisualStudio.Component.Debugger.JustInTime

## <a name="find-component-ids"></a>コンポーネント Id の検索

Visual Studio 製品によって並べ替えられたコンポーネントの一覧は、 [Visual studio 2017 のワークロードとコンポーネント id](../install/workload-and-component-ids.md?view=vs-2019&preserve-view=true)にあります。 マニフェスト内の前提条件 Id には、これらのコンポーネント Id を使用します。

特定のバイナリが含まれているコンポーネントがわからない場合は、 [コンポーネント > バイナリマッピングスプレッドシート](https://aka.ms/vs2017componentid-binaries)をダウンロードしてください。

### <a name="vs2017-componentbinarymappingxlsx"></a>vs2017-ComponentBinaryMapping.xlsx

Excel シートには、 **コンポーネント名**、 **ComponentId**、 **バージョン**、 **バイナリ/ファイル名** の4つの列があります。  フィルターを使用して、特定のコンポーネントとバイナリを検索および検索することができます。

すべての参照について、まず、コアエディター (VisualStudio) コンポーネントに含まれているものを確認します。  少なくとも、すべての拡張機能の前提条件として、コアエディターコンポーネントを指定する必要があります。 コアエディターに含まれていない参照の場合は、[ **バイナリ/ファイル名** ] セクションにフィルターを追加して、これらの参照のいずれかのサブセットを持つコンポーネントを検索します。

例 :

* デバッガー拡張機能があり、プロジェクトに *VSDebugEng.dll* と *VSDebug.dll* への参照が含まれていることがわかっている場合は、[ **バイナリ/ファイル名** ] ヘッダーの [フィルター] ボタンをクリックします。  "VSDebugEng.dll" を検索し、[ *OK]* を選択します。  次に、[ **バイナリ/ファイル名** ] ヘッダーの [フィルター] ボタンをもう一度クリックし、"VSDebug.dll" を検索します。  [現在の **選択項目をフィルターに追加する** ] チェックボックスをオンにして、[ **OK]** を選択します。  ここで、 **コンポーネント名** を調べて、拡張機能の種類に最も関係のあるコンポーネントを見つけます。 この例では、Just-in-time デバッガーを選択して、source.extension.vsixmanifest に追加します。
* プロジェクトがデバッガー要素を扱うことがわかっている場合は、フィルター検索ボックスで "デバッガー" を検索して、名前にデバッガーが含まれているコンポーネントを確認できます。

## <a name="specify-a-visual-studio-2017-release"></a>Visual Studio 2017 リリースを指定する

拡張機能に特定のバージョンの Visual Studio 2017 が必要な場合、たとえば、15.3 でリリースされた機能に依存している場合は、VSIX **インストールターゲット** でビルド番号を指定する必要があります。 たとえば、リリース15.3 のビルド番号は ' 15.0.26730.3 ' です。 [ここで](../install/visual-studio-build-numbers-and-release-dates.md)は、リリースのマッピングを参照して番号を作成できます。 リリース番号 ' 15.3 ' の使用は正しく機能しません。

拡張機能に15.3 以上が必要な場合は、 **Installationtarget バージョン** を [15.0.26730.3, 16.0) として宣言します。

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```