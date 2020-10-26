---
title: C++ デバッグ構成のプロジェクト設定 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- VC.Project.VCDebugSettings.WebBrowser.DebuggerType
- VC.Project.IVCGPUDebugPageObject.EnvironmentMerge
- VC.Project.VCDebugSettings.SymbolPath
- VC.Project.IVCClusterDebugPageObject.ApplicationCommand
- VC.Project.IVCRemoteDebugPageObject.WorkingDirectory
- VC.Project.VCDebugSettings.DebuggerType
- VC.Project.IVCLocalDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCRemoteDebugPageObject.SQLDebugging
- VC.Project.IVCRemoteDebugPageObject.Remote
- VC.Project.IVCGPUDebugPageObject.CommandArguments
- VC.Project.VCDebugSettings.CommandArguments
- VC.Project.IVCClusterDebugPageObject.MPIRunWorkingDirectory
- VC.Project.IVCLocalDebugPageObject.SQLDebugging
- VC.Project.IVCWebSvcDebugPageObject.HttpUrl
- VC.Project.IVCLocalDebugPageObject.WorkingDirectory
- VC.Project.IVCLocalDebugPageObject.CommandArguments
- VC.Project.IVCClusterDebugPageObject.MPIRunCommand
- VC.Project.IVCGPUDebugPageObject.WorkingDirectory
- VC.Project.IVCWebSvcDebugPageObject.DebuggerType
- VC.Project.IVCRemoteDebugPageObject.CommandArguments
- VC.Project.IVCRemoteDebugPageObject.DebuggerType
- VC.Project.IVCLocalDebugPageObject.GPUBreakOnAllThreads
- VC.Project.IVCRemoteDebugPageObject.RemoteMachine
- VC.Project.IVCClusterDebugPageObject.MPIRunArguments
- VC.Project.IVCClusterDebugPageObject.MPIAcceptFilter
- VC.Project.IVCGPUDebugPageObject.RemoteConnection
- VC.Project.VCDebugSettings.PDBPath
- VC.Project.IVCRemoteDebugPageObject.DeploymentDirectory
- VC.Project.VCDebugSettings.SQLDebugging
- VC.Project.VCDebugSettings.RemoteCommand
- VC.Project.IVCClusterDebugPageObject.ShimCommand
- VC.Project.IVCLocalDebugPageObject.Command
- VC.Project.IVCRemoteDebugPageObject.GPUBreakOnAllThreads
- VC.Project.IVCLocalDebugPageObject.Attach
- VC.Project.VCDebugSettings.Command
- VC.Project.IVCRemoteDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCRemoteDebugPageObject.RemoteCommand
- VC.Project.IVCClusterDebugPageObject.ApplicationArguments
- VC.Project.IVCLocalDebugPageObject.Environment
- VC.Project.IVCGPUDebugPageObject.DeploymentDirectory
- VC.Project.IVCLocalDebugPageObject.EnvironmentMerge
- VC.Project.VCDebugSettings.Environment
- VC.Project.IVCGPUDebugPageObject.BreakpointBehavior
- VC.Project.IVCLocalDebugPageObject.DebuggerType
- VC.Project.VCDebugSettings.WebBrowser.WebBrowserDebuggerHttpUrl
- VC.Project.IVCWebSvcDebugPageObject.SQLDebugging
- VC.Project.IVCGPUDebugPageObject.AcceleratorType
- VC.Project.IVCGPUDebugPageObject.Environment
- VC.Project.VCDebugSettings.RemoteMachine
- VC.Project.IVCGPUDebugPageObject.AdditionalFilesToDeploy
- VC.Project.VCDebugSettings.WorkingDirectory
- vs.debug.builds
- VC.Project.VCDebugSettings.Attach
- VC.Project.VCDebugSettings.HttpUrl
- VC.Project.IVCClusterDebugPageObject.MPIAcceptMode
- VC.Project.IVCGPUDebugPageObject.Attach
- VC.Project.IVCRemoteDebugPageObject.AdditionalFiles
- VC.Project.IVCGPUDebugPageObject.Command
- VC.Project.VCDebugSettings.Remote
- VC.Project.IVCRemoteDebugPageObject.Attach
- VC.Project.VCDebugSettings.EnvironmentMerge
- VC.Project.IVCGPUDebugPageObject.MachineName
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- DEBUG linker option
- -PDB linker option
- -Zl compiler option [C++]
- /DEBUG linker option
- /PDBSTRIPPED linker option
- /MAPINFO linker option
- -Zd compiler option [C++]
- -DEBUG linker option
- MAPINFO linker option
- /ZI compiler option [C++]
- ZI compiler option [C++]
- Z7 compiler option [C++]
- debugging [C++], debugger settings
- project settings [Visual Studio], debug configurations
- mapfiles, project settings
- debug configurations, C++
- project settings [Visual Studio]
- /PDB linker option
- -PDBSTRIPPED linker option
- debug builds, project settings
- PDB linker option
- projects [Visual Studio], debug configurations
- project configurations, debug
- Zd compiler option [C++]
- MAP linker option
- /Z7 compiler option [C++]
- .pdb files, debug build project settings
- -MAP linker option
- -MAPINFO linker option
- /Zd compiler option [C++]
- PDBSTRIPPED linker option
- -Z7 compiler option [C++]
- pdb files, debug build project settings
- /MAP linker option
ms.assetid: 860c7f13-a108-4fe5-8fca-d235cd3ca1cb
caps.latest.revision: 52
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ca9ff0678ba2c7abafa0d988efa09437ccd27dca
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687557"
---
# <a name="project-settings-for-a-c-debug-configuration"></a>C++ デバッグ構成のプロジェクト設定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

「[方法: デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)」で説明されているように、[**プロパティページ**] ダイアログボックスで、C または Visual C++ のデバッグ構成のプロジェクト設定を変更できます。 次の表は、 **[プロパティ ページ]** ダイアログ ボックスのデバッガー関連の設定の場所を示しています。  
  
> [!WARNING]
> C++ で記述された Windows ストアアプリおよびコンポーネントの [ **構成プロパティ/デバッグ** ] カテゴリのデバッグプロジェクト設定は異なります。 Windows 開発センターの「 [デバッグセッションを開始する (VB、C#、C++、および XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md) 」を参照してください。  
  
 [ **起動するデバッガー** ] ボックスで、使用するデバッガーを指定します。 選択したデバッガーによって、表示されるプロパティが異なります。  
  
 各デバッグ プロパティ設定は自動的に作成され、ソリューションを保存するたびに、ソリューションの "ユーザー単位の" ファイル (.vcxproj.user) に保存されます。  
  
### <a name="configuration-properties-folder-debugging-category"></a>[構成プロパティ] フォルダー ([デバッグ] カテゴリ)  
  
|**設定**|**説明**|  
|-----------------|---------------------|  
|**[起動するデバッガー]**|実行するデバッガーを指定します。次の中から選択します。<br /><br /> -   **ローカル Windows デバッガー**<br />-   **リモート Windows デバッガー**<br />-   **Web ブラウザー デバッガー**<br />-   **Web Service デバッガー**|  
|**[コマンド]** (ローカル Windows デバッガー)|ローカル コンピューターでデバッグするプログラムを起動するコマンドを指定します。|  
|**[リモート コマンド]** (リモート Windows デバッガー)|リモート コンピューター上の .exe のパスを指定します。 リモート コンピューターでパスを入力するようにパスを入力します。|  
|**コマンド引数** (ローカル windows デバッガーとリモート windows デバッガー)|- 上で指定したコマンドの引数を指定します。<br /><br /> このボックスでは、次のリダイレクト演算子を使用できます。<br /><br /> < `file`<br /> 標準入力を file から読み取ります。<br /><br /> > `file`<br /> 標準出力を file に書き込みます。<br /><br /> >> `file`<br /> 標準出力を file に追加します。<br /><br /> 2> `file`<br /> 標準エラー出力を file に書き込みます。<br /><br /> 2>> `file`<br /> 標準エラー出力を file に追加します。<br /><br /> 2> &1<br /> 標準エラー出力 (2) を標準出力 (1) と同じ位置に出力します。<br /><br /> 1> &2<br /> 標準出力 (1) を標準エラー出力 (2) と同じ位置に出力します。<br /><br /> ほとんどの場合、これらの演算子はコンソール アプリケーションでのみ有効です。|  
|**作業ディレクトリ**|デバッグするプログラムの作業ディレクトリを、EXE ファイルがあるプロジェクト ディレクトリを基準とした相対パスで指定します。 この設定を空白のままにした場合、作業ディレクトリはプロジェクト ディレクトリになります。 リモート デバッグの場合、プロジェクト ディレクトリはリモート サーバーにあります。|  
|**[アタッチ]** (ローカル Windows デバッガーとリモート Windows デバッガー)|アプリケーションを起動するか、またはアプリケーションにアタッチするかを指定します。 既定の設定は [いいえ] です。|  
|**[リモート サーバー名]** (リモート Windows デバッガー)|アプリケーションをデバッグするコンピューター (自分のコンピューター以外) の名前を指定します。<br /><br /> RemoteMachine ビルドマクロは、このプロパティの値に設定されます。詳細については、「 [ビルドコマンドとプロパティのマクロ](https://msdn.microsoft.com/library/239bd708-2ea9-4687-b264-043f1febf98b)」を参照してください。|  
|**[接続]** (リモート Windows デバッガー)|リモート デバッグ用の接続の種類を、標準の接続と認証を使用しない接続の間で切り替えます。 **[リモート サーバー名]** ボックスでリモート コンピューター名を指定します。 接続の種類には、次のようなものがあります。<br /><br /> -   **Windows 認証でリモート接続する**<br />-   **認証なしのリモート (ネイティブのみ)**<br /><br /> **メモ** 認証を使用しないリモート デバッグを行うと、セキュリティ違反に対してリモート コンピューターが脆弱になる可能性があります。 Windows 認証モードの方がより安全です。<br /><br /> 詳細については、「 [リモートデバッグのセットアップ](../debugger/remote-debugging.md)」を参照してください。|  
|**[HTTP URL]** (Web Service デバッガーと Web ブラウザー デバッガー)|デバッグするプロジェクトが存在する URL を指定します。|  
|**[デバッガーのタイプ]**|使用するデバッガーの種類を指定します: **[ネイティブのみ]** 、 **[マネージドのみ]** 、 **[GPU のみ]** 、 **[混合]** 、 **[自動]** (既定)、 **[スクリプト]** 。<br /><br /> -    **[ネイティブのみ]** は、アンマネージ C++ コードに使用します。<br />-    **[マネージドのみ]** は、共通言語ランタイムで実行されるコード (マネージド コード) に使用します。<br />-    **[混合]** を選択すると、マネージド コードとアンマネージド コードのデバッガーが起動します。<br />-    **[自動]** を選択すると、コンパイラと EXE の情報に基づいてデバッガーの種類が決まります。<br />-    **[スクリプト]** を選択すると、スクリプトのデバッガーが起動します。<br />-    **[GPU のみ]** は、GPU デバイスまたは DirectX リファレンス ラスターライザーで実行される C++ AMP コードに使用します。 「 [GPU コードのデバッグ](../debugger/debugging-gpu-code.md)」を参照してください。|  
|**環境** (ローカル Windows デバッガー)|デバッグするプログラムの環境変数を指定します。 標準的な環境変数の構文を使用します (例: `PATH="%SystemRoot%\..."`)。 各変数は、 **[マージ環境]** の設定に応じて、システム環境をオーバーライドするか、システム環境にマージされます。 設定列内でクリックすると、"... の編集" が表示されます。 そのリンクをクリックして、環境変数を編集します。|  
|**[マージ環境]** (ローカル Windows デバッガー)|**[環境]** ボックスで指定した変数を、オペレーティング システムによって定義されている環境にマージするかどうかを決定します。 既定の設定は [はい] です。|  
|**[SQL デバッグ]** (MPI クラスター デバッガーを除くすべて)|SQL プロシージャのデバッグを [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] アプリケーションから有効にします。 既定の設定は [いいえ] です。|  
|**[デバッグ アクセラレータの種類]** (GPU デバッグのみ)|デバッグに使用する GPU デバイスを指定します。 互換性のある GPU デバイス用のデバイス ドライバーをインストールするとその他のオプションが追加されます。 既定の設定は [GPU - ソフトウェア エミュレーター] です。|  
|**[GPU 既定のブレークポイントの動作]** (GPU デバッグのみ)|ブレークポイント イベントを SIMD ワープの各スレッドごとに発生させるかどうかを指定します。 既定の設定では、1 ワープごとに 1 回、ブレークポイント イベントが発生します。|  
|**Amp の既定のアクセラレータ** (GPU デバッグのみ)|GPU コードをデバッグする際、既定の AMP のアクセラレータを指定します。 問題の原因がコードではなく、ハードウェアやドライバーにあるかどうかを調査するには、 **[WARP ソフトウェアのアクセラレータ]** を選択します。|  
|**[配置ディレクトリ]** (リモート Windows デバッガー)|起動前にプロジェクト出力がコピーされるリモート コンピューター上のパスを指定します。 このパスとして、リモート コンピューター上のネットワーク共有、またはリモート コンピューター上のフォルダーへのパスを指定できます。 既定の設定は空で、プロジェクト出力はネットワーク共有にコピーされます。 ファイルの配置を有効にするには、[構成マネージャー] ダイアログ ボックスで **[配置]** チェック ボックスをオンにする必要もあります。 詳細については、「 [方法: 構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)」を参照してください。|  
|**[配置する追加ファイル]** (リモート Windows デバッガー)|配置ディレクトリのプロパティを設定している場合、配置ディレクトリにコピーする追加ファイルのセミコロン区切りのリストを指定します。 既定の設定は空で、配置ディレクトリにコピーされる追加ファイルはありません。 ファイルの配置を有効にするには、[構成マネージャー] ダイアログ ボックスで **[配置]** チェック ボックスをオンにする必要もあります。 詳細については、「 [方法: 構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)」を参照してください。|  
|**[Visual C++ デバッグ ランタイム ライブラリの配置]** (リモート Windows デバッガー)|配置ディレクトリのプロパティを設定している場合、現在のプラットフォーム用の Visual C++ デバッグ ランタイム ライブラリをネットワーク共有にコピーする必要があるかどうかを指定します。 既定の設定は [はい] です。|  
  
### <a name="cc-folder-general-category"></a>C/C++ フォルダー ([全般] カテゴリ)  
  
|設定|説明|  
|-------------|-----------------|  
|**[デバッグ情報の形式]** ([/Z7、/Zd、Zi、/ZI](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8))|プロジェクトに作成するデバッグ情報の種類を指定します。<br /><br /> 既定のオプション (/ZI) では、プログラム データベース (PDB) がエディット コンティニュ互換形式で作成されます。 詳細については、「 [/Z7、/zd、/zi、/zi (デバッグ情報の形式)](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8)」を参照してください。|  
  
### <a name="cc-folder-optimization-category"></a>[C/C++] フォルダー ([最適化] カテゴリ)  
  
|設定|説明|  
|-------------|-----------------|  
|**Optimization**|コンパイラが生成したコードを最適化するかどうかを指定します。 最適化すると、実行されるコードが変更されます。 最適化したコードはソース コードと一致しなくなります。 したがって、デバッグは困難です。<br /><br /> 既定のオプション (**Disabled (/0d**) は、最適化を抑制します。 最適化を行わずにコードを開発し、実行環境用のコードを作成するときに最適化をオンにできます。|  
  
### <a name="linker-folder-debugging-category"></a>[リンカー] フォルダー ([デバッグ] カテゴリ)  
  
|設定|説明|  
|-------------|-----------------|  
|**[デバッグ情報を作成]** ([/DEBUG](https://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103))|デバッグ情報を含めるようにリンカーに指示します。デバッグ情報の形式は、/Z7、/Zd、Zi、または /ZI で指定されます。|  
|**[プログラム データベース ファイルの生成]** ([/PDB:name](https://msdn.microsoft.com/library/d23db0ce-10cb-427a-bc60-d6b2a852723d))|PDB ファイルの名前を指定します。 [デバッグ情報の形式] で ZI または /Zi を選択する必要があります。|  
|**[プライベート シンボルの削除]** ([/PDBSTRIPPED:filename](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55))|PDB ファイルのプライベート シンボルを含めない場合は、このボックスに PDB ファイルの名前を指定します。 PDB ファイルを生成するいずれかのコンパイラ オプションまたはリンカー オプションを使ってプログラム イメージをビルドするときにこのオプションを指定すると、2 番目のプログラム データベース (PDB) ファイルが作成されます (コンパイラ オプションまたはリンカー オプションの例: /DEBUG、/Z7、/Zd、 /Zi など)。 2 番目の PDB ファイルでは、顧客に提供しないシンボルが省かれています。 詳細については、「 [/PDBSTRIPPED (プライベートシンボルの削除)](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55)」を参照してください。|  
|**[マップ ファイルの作成]** ([/MAP](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63))|リンク中にマップ ファイルを生成するようにリンカーに指示します。 既定の設定は [いいえ] です。 詳細については、「[/MAP (マップ ファイルの生成)](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63)」を参照してください。|  
|**[マップ ファイル名]** ([/MAP:](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63)*name*)|[マップ ファイルの作成] を選択する場合は、このボックスにマップ ファイルを指定できます。 詳細については、「[/MAP (マップ ファイルの生成)](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63)」を参照してください。|  
|**[マップファイルのエクスポート]** ([/MAPINFO:EXPORTS](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b))|エクスポートされた関数をマップ ファイルに含めます。 既定の設定は [いいえ] です。 詳細については、「[/MAPINFO (マップ ファイルに含める情報)](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b)」を参照してください。|  
|**[デバッグできるアセンブリ]** ([/ASSEMBLYDEBUG](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b))|リンカーの /ASSEMBLYDEBUG オプションの設定を指定します。 使用できる値は次のとおりです。<br /><br /> -    **[デバッグできる属性が作成されませんでした]** 。<br />-    **[ランタイム トラッキングおよび最適化の無効 (/ASSEMBLYDEBUG)]** 。 これが既定の設定です。<br />-    **[ランタイム トラッキングおよび最適化の有効を無効にする (/ASSEMBLYDEBUG:DISABLE)]** 。<br />-   **\<inherit from parent or project defaults>**.<br />詳細については、「[/ASSEMBLYDEBUG (DebuggableAttribute の追加)](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982)」を参照してください。|  
  
 [構成プロパティ] フォルダー ([デバッグ] カテゴリ) 内のこれらの設定は、Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings インターフェイスを使用してプログラムで変更できます。 詳細については、「<xref:Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings>」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ネイティブコードのデバッグ](../debugger/debugging-native-code.md)   
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)   
 [Visual C++ プロジェクトの作成と管理](https://msdn.microsoft.com/library/11003cd8-9046-4630-a189-a32bf3b88047)   
 [/Assemblydebug (DebuggableAttribute の追加)](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982)   
 [ビルドのコマンドとプロパティの共通マクロ](https://msdn.microsoft.com/library/239bd708-2ea9-4687-b264-043f1febf98b)
