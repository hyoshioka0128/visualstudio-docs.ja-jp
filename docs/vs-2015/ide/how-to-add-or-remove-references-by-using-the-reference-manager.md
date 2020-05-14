---
title: '方法: 参照マネージャーを使用して参照を追加または削除する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.ReferenceManager
helpviewer_keywords:
- Visual C# projects, references
- references [Visual Studio], adding
- assemblies [Visual Studio], references
- Visual Basic projects, references
- project references, adding
- referencing components, adding references
- project references, removing
- referencing assemblies
- referencing components, removing references
- references [Visual Studio], removing
- referencing components, assemblies not listed
ms.assetid: 1aabb520-99b0-46c6-9368-21b4d84793eb
caps.latest.revision: 48
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d0763f2cf86d94f96f6f9c907ee306c731994f22
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75852088"
---
# <a name="how-to-add-or-remove-references-by-using-the-reference-manager"></a>方法: 参照マネージャーを使用して参照を追加または削除する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[参照マネージャー]** ダイアログ ボックスを使って、Microsoft または別の企業が開発したコンポーネントへの参照を追加し、管理することができます。 ユニバーサル Windows アプリを開発している場合、プロジェクトはすべての正しい Windows SDK DLL を自動的に参照します。 .NET アプリケーションを開発している場合、プロジェクトは mscorlib.dll を自動的に参照します。 一部の .NET API は、手動で追加する必要があるコンポーネントで公開されます。 COM コンポーネントまたはカスタム コンポーネントへの参照は、手動で追加する必要があります。

## <a name="adding-and-removing-a-reference"></a>参照の追加と削除

#### <a name="to-add-a-reference"></a>参照を追加するには

1. **ソリューション エクスプローラー**で、[参照] ノードを右クリックし、 **[参照の追加]** を選びます。

2. 追加する参照を指定した後、 **[OK]** ボタンを選びます。

   **[参照マネージャー]** は、使用可能な参照を開いてグループごとに表示します。 プロジェクトの種類に基づいて、次のグループのうちどれが表示されるかが決まります。

- アセンブリ - Framework と拡張機能の各サブグループが含まれます。

- ソリューション - プロジェクト サブグループが含まれます。

- Windows - コアと拡張機能の各サブグループが含まれます。 **[オブジェクト ブラウザー]** を使って Windows SDK または拡張 SDK 内の参照を探索できます。

- 最近使用したサブグループを参照します。

## <a name="assemblies-tab"></a>[アセンブリ] タブ
 **[アセンブリ]** タブには、参照に使うことができるすべての .NET Framework アセンブリが一覧表示されます。 グローバル アセンブリ キャッシュ (GAC) 内のアセンブリは実行時環境の一部であるため、 **[アセンブリ]** タブでは GAC からのアセンブリはどれもリスト表示されません。 GAC に登録されているアセンブリへの参照を含むアプリケーションを配置またはコピーした場合は、[ローカル コピー] の設定とはかかわりなく、そのアセンブリがアプリケーションと共に配置またはコピーされることはありません。 詳しくは、「[プロジェクトの参照](https://msdn.microsoft.com/library/ez524kew.aspx)」をご覧ください。

 EnvDTE 名前空間 (EnvDTE、EnvDTE80、EnvDTE90、EnvDTE90a、または EnvDTE100) に手動で参照を追加するときは、[プロパティ] ウィンドウで参照の [相互運用型の埋め込み] プロパティを False に設定します。 このプロパティを True に設定すると、埋め込むことができない EnvDTE プロパティが原因でビルドの問題が発生する可能性があります。

 すべてのデスクトップ プロジェクトには、mscorlib への暗黙的な参照が含まれます。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] プロジェクトには、Microsoft.VisualBasic への暗黙的な参照が含まれます。 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] では、System.Core が参照のリストから削除された場合でも、すべてのプロジェクトに System.Core への暗黙的な参照が含まれます。

 プロジェクトの種類がアセンブリをサポートしていない場合は、 **[参照マネージャー]** ダイアログ ボックスの中に [アセンブリ] タブが表示されません。

 [アセンブリ] タブの中には、次の 2 つのサブタブがあります。

1. [Framework] には、対象の Framework を形成するすべてのアセンブリが一覧表示されます。

   - アドバタイズされたアセンブリは [Full Framework] の中にあり、対象とする Framework のプロファイルをプロジェクトが対象にしている場合は、それらのアセンブリは [Framework] 一覧で列挙されます。 アドバタイズされたアセンブリは淡色表示され、プロジェクトの対象である Framework プロファイルの中に存在するアセンブリとは区別されます。 たとえば、プロジェクトが .NET Framework 4 Client を対象としている場合は、[Framework] 一覧には .NET Framework 4 からアドバタイズされたアセンブリが表示されます。 アドバタイズされたアセンブリをユーザーが追加した場合は、 **[参照マネージャー]** ダイアログ ボックスを閉じた後、プロジェクトが .NET Framework 4 を対象として再指定し、アドバタイズされたアセンブリが追加されることがユーザーに対して通知されます。

   - [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリケーションを対象とするプロジェクトには、プロジェクトを作成した時点の既定として、対象の [!INCLUDE[net_win8_profile](../includes/net-win8-profile-md.md)] 内にあるすべてのアセンブリへの参照が含まれています。 マネージド プロジェクトでは、**ソリューション エクスプローラー**内の [参照設定] フォルダーの下にある 1 つの読み取り専用ノードが、Framework 全体に対する参照を示します。 したがって、[Framework] タブでは、Framework からのどのアセンブリも列挙されず、代わりに次のメッセージが表示されます。"すべての Framework アセンブリが既に参照されています。 オブジェクト ブラウザーを使用して Framework 内の参照を調べてください。" デスクトップ プロジェクトの場合は、対象とする Framework からのアセンブリが [Framework] タブで列挙され、アプリケーションが必要とする参照をユーザーが追加する必要があります。

2. [拡張機能] には、対象の Framework を拡張するためにコンポーネントおよびコントロールを扱う外部販売元が開発したすべてのアセンブリの一覧が表示されます。 ユーザー アプリケーションの目的によっては、これらのアセンブリが必要になることがあります。

   - 次の場所に登録されているアセンブリを列挙することによって、拡張機能が設定されます。

       ```
       32-bit machine:
       HKEY_CURRENT_USER\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]
       HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]
       64-bit machine:
       HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]
       HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]
       And older versions of the [Target Framework Identifier]
       ```

        たとえば、プロジェクトが 32 ビット コンピューター上の .NET Framework 4 を対象とする場合は、拡張機能は \Microsoft\\.NETFramework\v4.0\AssemblyFoldersEx\\、\Microsoft\\.NETFramework\v3.5\AssemblyFoldersEx\\、\Microsoft\\.NETFramework\v3.0\AssemblyFoldersEx\\、および \Microsoft\\.NETFramework\v2.0\AssemblyFoldersEx\\ の下に登録されているアセンブリを列挙します。

   プロジェクトの [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] バージョンによっては、一部のコンポーネントが一覧に表示されないことがあります。 これは、次のような条件で発生します。

- 最新バージョンの .NET Framework を使用するコンポーネントは、旧バージョンの .NET Framework を対象とするプロジェクトとは互換性がありません。

     プロジェクトの対象となる .NET Framework のバージョンを変更する方法については、「[方法: .NET Framework のバージョンをターゲットにする](../ide/how-to-target-a-version-of-the-dotnet-framework.md)」をご覧ください。

- [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] を使用するコンポーネントは、[!INCLUDE[net_v45](../includes/net-v45-md.md)] を対象とするプロジェクトと互換性がありません。

     新しいアプリケーションの作成時に、いくつかのプロジェクトが既定で [!INCLUDE[net_v45](../includes/net-v45-md.md)] を対象とするように設定されます。 詳細については、「[.NET Framework Client Profile](https://msdn.microsoft.com/library/f0219919-1f02-4588-8704-327a62fd91f1)」を参照してください。

- コンパイル エラーが発生する可能性があるため、同じソリューション内の他のプロジェクトの出力に対するファイル参照は追加しないでください。 代わりに、 **[参照の追加]** ダイアログ ボックスの **[プロジェクト]** タブを使ってプロジェクト間参照を作成します。 そうすることによってプロジェクトで作成するクラス ライブラリを管理する機能が向上し、チーム開発が簡単になります。 詳しくは、「[壊れた参照のトラブルシューティング](../ide/troubleshooting-broken-references.md)」をご覧ください。

- > [!NOTE]
    > Visual Studio 2015 では、一方のプロジェクトが対象とする .NET Framework のバージョンが Version 4.5 で、他方のプロジェクトが対象とするバージョンが Version 2、3、3.5、または 4.0 である場合、プロジェクト参照ではなくファイル参照が作成されます。

#### <a name="to-display-an-assembly-in-the-add-reference-dialog-box"></a>[参照の追加] ダイアログ ボックスにアセンブリを表示するには

- アセンブリを次の場所のいずれかに移動またはコピーします。

  - 現在のプロジェクト ディレクトリ。 ここにあるアセンブリは、 **[参照]** タブに表示されます。

  - 同じソリューション内のその他のプロジェクト ディレクトリ。 ここにあるアセンブリは、 **[プロジェクト]** タブに表示されます。

    \- または

- 表示するアセンブリの場所を指定するレジストリ キーを設定します。

   32 ビット オペレーティング システムでは、次のいずれかのレジストリ キーを追加します。

  - [HKEY_CURRENT_USER\SOFTWARE\Microsoft\\.NETFramework\\*VersionMinimum*\AssemblyFoldersEx\MyAssemblies]@="*AssemblyLocation*"

  - [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\\*VersionMinimum*\AssemblyFoldersEx\MyAssemblies]@="*AssemblyLocation*"

    64 ビット オペレーティング システムでは、32 ビットのレジストリ ハイブで次のいずれかのレジストリ キーを追加します。

  - [HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\\*VersionMinimum*\AssemblyFoldersEx\MyAssemblies]@="*AssemblyLocation*"

  - [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\\*VersionMinimum*\AssemblyFoldersEx\MyAssemblies]@="*AssemblyLocation*"

    *VersionMinimum* は、適用される .NET Framework の最小バージョンです。 *VersionMinimum* が v3.0 の場合、AssemblyFoldersEx で指定したフォルダーは、.NET Framework 3.0 以降を対象にしたプロジェクトに適用されます。

    *AssemblyLocation* は、C:\MyAssemblies\\ など、 **[参照の追加]** ダイアログ ボックスに表示されるアセンブリのディレクトリです。

    HKEY_LOCAL_MACHINE ノードにレジストリ キーを作成すると、すべてのユーザーが特定の場所にあるアセンブリを **[参照の追加]** ダイアログ ボックスに表示できるようになります。 HKEY_CURRENT_USER ノードにレジストリ キーを作成すると、現在のユーザーの設定にのみ影響します。

    **[参照の追加]** ダイアログ ボックスを再度開きます。 アセンブリが **[.net]** タブに表示されます。そうでない場合は、アセンブリが指定された*Assemblylocation*ディレクトリに配置されていることを確認し、Visual Studio を再起動して、もう一度やり直してください。

## <a name="com-tab"></a>[COM] タブ
 [COM] タブには、参照できるすべての COM コンポーネントの一覧が表示されます。 内部マニフェストを含む登録済みの COM DLL に参照を追加する場合は、その DLL の登録をまず解除してください。 そうしない場合は、Visual Studio は、アセンブリ参照をネイティブ DLL ではなく、ActiveX コントロールとして追加します。

 プロジェクトの種類が COM をサポートしていない場合は、 **[参照マネージャー]** ダイアログ ボックスの中に [COM] タブが表示されません。

## <a name="solution-tab"></a>[ソリューション] タブ
 [ソリューション] タブ内の [プロジェクト] サブタブには、現在のソリューション内に存在し互換性のあるすべてのプロジェクトが表示されます。

 プロジェクトは、異なるバージョンの .NET Framework を対象とする別のプロジェクトを参照できます。 たとえば、[!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] を対象とするプロジェクトを作成し、その中で、.NET Framework 2 を想定してビルドされたアセンブリを参照することができます。 ただし、.NET Framework 2 プロジェクトから、[!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] プロジェクトを参照することはできません。 詳細については、「[対象となる特定の .NET Framework のバージョンの指定](../ide/targeting-a-specific-dotnet-framework-version.md)」を参照してください。

 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] を対象とするプロジェクトは、[!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] を対象とするプロジェクトと互換性がありません。

 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]で、1 つのプロジェクトが .NET Framework 4 を対象とし、別のプロジェクトが旧バージョンを対象としている場合は、プロジェクト参照ではなくファイル参照が生成されます。

 [!INCLUDE[net_win8_profile](../includes/net-win8-profile-md.md)] を対象とするプロジェクトは、.NET Framework を対象とするプロジェクトに対するプロジェクト参照を追加できません。逆も同じです。

## <a name="windows-tab"></a>[Windows] タブ
 [Windows] タブには、Windows オペレーティング システムを実行しているプラットフォームに固有であるすべての SDK が一覧表示されます。

 Visual Studio 内で、次のような 2 とおりの方法で WinMD ファイルを生成できます。

- **[!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリケーションのマネージド プロジェクト**: [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリ プロジェクトは、[プロジェクトのプロパティ &#124; 出力の種類 = WinMD ファイル] に設定することにより、WinMD バイナリを出力できます。 WinMD のファイル名はその中に存在するすべての名前空間に対するスーパーセットの名前空間である必要があります。 たとえば、1 つのプロジェクトが名前空間 A.B と A.B.C で形成されている場合は、出力される WinMD で使用可能な名前は A.winmd と A.B.winmd です。 ユーザーが、[プロジェクトのプロパティ &#124; アセンブリ名] または [プロジェクトのプロパティ &#124; 名前空間] に、プロジェクト内の一連の名前空間から分離されている値を入力した場合や、プロジェクト内に存在する名前空間に対するスーパーセットの名前空間が存在しない場合は、次のようなビルドの警告が生成されます。'A.winmd' は、このアセンブリに有効な winmd ファイル名ではありません。 Windows メタデータ ファイル内のすべての型は、ファイル名で指定される名前空間のサブ名前空間に存在する必要があります。 このようなサブ名前空間に存在しない型は、ランタイムに見つかりません。 このアセンブリでは、ファイル名として使用できる最も小さい共通の名前空間は 'CSWSClassLibrary1' です。 デスクトップの Visual Basic プロジェクトまたは Visual C# プロジェクトでは、[!INCLUDE[win8](../includes/win8-md.md)] SDK を使用して生成される WinMD のみを使用できます。このような WinMD を、ファースト パーティ WinMD と呼びます。また、これらのプロジェクトでは WinMD を生成できません。

- **[!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリケーションのネイティブ プロジェクト**: ネイティブ WinMD ファイルは、メタデータのみで構成されます。 その実装は、別の DLL ファイル内に存在します。 **[新しいプロジェクト]** ダイアログ ボックス内で Windows ランタイム構成プロジェクト テンプレートを選ぶか、空のプロジェクトから作業を開始し、WinMD ファイルを生成するようにプロジェクトのプロパティを変更することによって、ネイティブ バイナリを生成できます。 プロジェクトが、分離された複数の名前空間で形成されている場合は、ユーザーがそれらの名前空間を結合するか、MSMerge ツールを実行することを求めるビルド エラーが表示されます。

  [Windows] タブの中には、次の 2 つのサブグループがあります。

### <a name="core-subgroup"></a>[コア] サブグループ
 [コア] サブグループには、対象となる Windows のバージョンに対応する SDK の中にある (Windows ランタイム要素に対応する) すべての WinMD が一覧表示されます。

 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリケーション プロジェクトには、プロジェクトを作成した時点の既定として、[!INCLUDE[win8](../includes/win8-md.md)] 内にあるすべての WinMD への参照が含まれています。 マネージド プロジェクトでは、**ソリューション エクスプローラー**の [参照] フォルダーの下にある 1 つの読み取り専用ノードが、[!INCLUDE[win8](../includes/win8-md.md)] SDK 全体に対する参照を示します。 したがって、[参照マネージャー] の [コア] サブグループでは、[!INCLUDE[win8](../includes/win8-md.md)] SDK からのアセンブリのいずれも列挙されず、代わりに次のメッセージが表示されます。"The Windows SDK is already referenced. (Windows SDK が既に参照されています。) Please use the Object Browser to explore the references in the Windows SDK. (オブジェクト ブラウザーを使用して Windows SDK 内の参照を調べてください。)"

 デスクトップ プロジェクトでは、[コア] サブグループは既定では表示されません。 Windows ランタイムを追加するために、プロジェクト ノードのショートカット メニューを開き、 **[プロジェクトのアンロード]** をクリックし、次のスニペットを追加してから、プロジェクトをもう一度開きます (プロジェクト ノードで、 **[プロジェクトの再読み込み]** をクリックします)。 **[参照マネージャー]** ダイアログ ボックスを開くと、[コア] サブグループが表示されます。

```
<PropertyGroup>
  <TargetPlatformVersion>8.0</TargetPlatformVersion>
</PropertyGroup>
```

 このサブグループの **[Windows]** チェック ボックスがオンになっていることを確認します。 その後は、Windows ランタイム要素を使用できます。 ただし、System.Runtime を追加する必要もあります。そこで、Windows ランタイム ライブラリ全体で使用される、IEnumerable などの標準のクラスおよびインターフェイスが Windows ランタイムによって定義されます。 System.Runtime を追加する方法については、「[マネージド デスクトップ アプリと Windows ランタイム](https://msdn.microsoft.com/library/windows/apps/jj856306.aspx#consuming_standard_windows_runtime_types)」をご覧ください。

### <a name="extensions-subgroup"></a>[拡張機能] サブグループ
 [拡張機能] で、対象の Windows プラットフォームを拡張するユーザー SDK が一覧表示されます。 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリケーション プロジェクトの場合のみ、このタブが表示されます。 デスクトップ プロジェクトで使用できるのは、ファースト パーティの .winmd ファイルのみであるため、このタブは表示されません。

 SDK は、Visual Studio が単一のコンポーネントとして取り扱うファイルのコレクションです。 [拡張機能] タブで、 **[参照マネージャー]** ダイアログ ボックスを開いたプロジェクトに対して適用される複数の SDK は単一エントリとして表示されます。 プロジェクトに追加した場合は、SDK のすべての内容が Visual Studio によって使用されます。その結果、IntelliSense、ツールボックス、デザイナー、オブジェクト ブラウザー、ビルド、配置、デバッグ、およびパッケージ化で SDK の内容を活用するために、ユーザーが追加のアクションを実行する必要がなくなります。 [拡張機能] タブに SDK を表示する方法については、「[Creating a Software Development Kit](../extensibility/creating-a-software-development-kit.md)」(ソフトウェア開発キットの作成) を参照してください。

> [!NOTE]
> 別の SDK に依存する SDK をプロジェクトが参照する場合は、ユーザーが 2 番目の SDK への参照を手動で追加しない限り、Visual Studio は 2 番目の SDK を使用しません。 ユーザーが **[拡張機能]** タブでいずれかの SDK を選ぶと、 **[参照マネージャー]** ダイアログ ボックスで SDK の名前とバージョンが一覧表示されることに加えて、詳細ペインであらゆる依存先 SDK の名前も一覧表示され、SDK の依存関係を識別できるようになります。 ユーザーが依存関係に気付かず、SDK のみを追加した場合は、依存関係を追加することを要求するメッセージが MSBuild によって表示されます。

 プロジェクトの種類が **[拡張機能]** をサポートしていない場合は、 **[参照マネージャー]** ダイアログ ボックスの中に [拡張機能] タブが表示されません。

## <a name="browse-button"></a>[参照] ボタン
 **[参照]** ボタンを使って、ファイル システム内のコンポーネントを参照できます。

 プロジェクトは、異なるバージョンの .NET Framework を対象とするコンポーネントを参照できます。 たとえば、.NET Framework 4 Client Profile を対象とするアプリケーションを作成し、その中で、.NET Framework 2 を対象とするコンポーネントを参照することもできます。 詳細については、「[対象となる特定の .NET Framework のバージョンの指定](../ide/targeting-a-specific-dotnet-framework-version.md)」を参照してください。

 同じソリューション内にある別のプロジェクトの出力に対するファイル参照を追加しないでください。この方針を使用すると、コンパイル エラーが発生する可能性があります。 代わりに、 **[参照マネージャー]** ダイアログ ボックスの **[ソリューション]** タブを使ってプロジェクト間参照を作成します。 この方針を使用すると、プロジェクト内で作成するクラス ライブラリをより適切に管理でき、チーム開発が簡単になります。 詳しくは、「[壊れた参照のトラブルシューティング](../ide/troubleshooting-broken-references.md)」をご覧ください。

 SDK を参照してプロジェクトに追加することはできません。 ファイル (たとえば、アセンブリまたは .winmd) のみを参照してプロジェクトに追加することができます。

 WinMD に対してファイル参照を行う場合に予期されるレイアウトは、*FileName*.winmd、*FileName*.dll、および *FileName*.pri というすべてのファイルが並行して配置された状態です。 次のシナリオで WinMD を参照する場合は、不完全なファイル セットがプロジェクトの出力ディレクトリにコピーされるため、ビルド エラーとランタイム エラーが発生します。

- **ネイティブ コンポーネント**: ネイティブ プロジェクトは、分離された名前空間ごとに 1 つの WinMD を作成し、実装全体を含む 1 つの DLL を作成します。 各 WinMD は、共通点のない名前になります。 このネイティブ コンポーネント ファイルを参照するときに、MSBuild は、共通点のない名前を付けられた複数の WinMD が 1 つのコンポーネントを形成することを認識しません。 その結果、同じ名前を付けられた *FileName*.dll と *FileName*.winmd のみがコピーされ、ランタイム エラーが発生します。 この問題を回避するには、拡張機能 SDK を作成します。 詳しくは、「[Creating a Software Development Kit](../extensibility/creating-a-software-development-kit.md)」(ソフトウェア開発キットの作成) をご覧ください。

- **コントロールの使用**: XAML コントロールは、少なくとも *FileName*.winmd、*FileName*.dll、*FileName*.pri、*XamlName*.xaml、および *ImageName*.jpg で構成されます。 プロジェクトをビルドするときに、ファイル参照に関連付けられたリソース ファイルはプロジェクトの出力ディレクトリにコピーされず、*FileName*.winmd、*FileName*.dll、および *FileName*.pri のみがコピーされます。 リソースの *XamlName*.xaml と *ImageName*.jpg が見つからないことをユーザーに通知するために、ビルド エラーが記録されます。 ビルド、デバッグ、および実行時の動作を成功させるには、ユーザーはプロジェクトの出力ディレクトリにこれらのリソース ファイルを手動でコピーする必要があります。 この問題を回避するには、「[Creating a Software Development Kit](../extensibility/creating-a-software-development-kit.md)」(ソフトウェア開発キットの作成) の手順に従って拡張機能 SDK を作成するか、プロジェクト ファイルを編集して次のプロパティを追加します。

    ```
    <PropertyGroup>
    <GenerateLibraryOutput>True</GenerateLibraryOutput>
    </PropertyGroup>
    ```

    > [!NOTE]
    > プロパティを追加した場合は、ビルド速度が遅くなる可能性があります。

## <a name="recent"></a>最近使った項目
 [アセンブリ]、[COM]、[Windows]、[参照] はいずれも [最近使用したファイル] タブをサポートし、このタブではプロジェクトに最近追加されたコンポーネントのリストが列挙されます。

## <a name="search"></a>[検索]
 **[参照マネージャー]** ダイアログ ボックス内の検索バーは、現在フォーカスが置かれているタブを対象として動作します。 たとえば、 **[ソリューション]** タブにフォーカスがあるときにユーザーが検索バーに「System」と入力した場合は、"System" という文字列を含むプロジェクト名がソリューションを形成している状況以外では、検索結果が返されません。

## <a name="see-also"></a>参照
 [NIB 方法: [参照の追加] ダイアログボックスを使用して参照を追加または削除し、](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9) [プロジェクト内の参照を管理](../ide/managing-references-in-a-project.md)する
