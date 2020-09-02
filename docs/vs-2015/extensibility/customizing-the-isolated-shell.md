---
title: 分離シェルのカスタマイズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode
ms.assetid: e0b7c3ae-210f-4f48-ac49-6a59e6034f5f
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 724d4d0c4b392a362e702f33ea996df3a6fc0ad6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62555969"
---
# <a name="customizing-the-isolated-shell"></a>分離シェルのカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual studio の分離シェルアプリケーションをカスタマイズするには、Visual Studio のユーザーインターフェイスのさまざまな側面を変更し、特殊なアプリケーションに含まれるコマンドと機能を制限します。  
  
## <a name="using-the-applicationpkgdef-file"></a>アプリケーションの pkgdef ファイルの使用  
 分離シェルテンプレートソリューションには、 *SolutionName*が含まれています。次の機能を変更できるようにするアプリケーションの pkgdef ファイル。  
  
##### <a name="the-application-title"></a>アプリケーションのタイトル  
 アプリケーションのタイトルをカスタマイズできます。これは、 *SolutionName*の "AppName" 行の値を変更することによって、アプリケーションのタイトルバーに表示される名前です。アプリケーションの pkgdef ファイル。 詳細については、「 [チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
 現在読み込まれているプロジェクトをアプリケーションのタイトルに表示させたくない場合は、 *SolutionName*の "ShowHierarchyRootInTitle" 行の値を変更します。アプリケーションの pkgdef ファイルを dword: 00000001 から dword: 00000000 にします。  
  
##### <a name="the-application-icon"></a>アプリケーションアイコン  
 アプリケーションのタイトルバーにアプリケーション名で表示されるアイコンであるアプリケーションアイコンをカスタマイズできます。 アイコンディレクトリに別のアイコンをコピーします。 **ソリューションエクスプローラー**で、[リソースファイル] フォルダーにアイコンを追加します。 次に、VSShellStub .rc ファイルを開き、IDI_STUBPROGRAM の値を新しいアイコンの名前に置き換えます。 詳細については、「 [チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
##### <a name="the-command-line-logo"></a>コマンドラインロゴ  
 コマンドラインロゴは、アプリケーションをコマンドラインから起動したときに表示されるテキストで、 *SolutionName*の "CommandLineLogo" 行の値を変更することによってカスタマイズできます。アプリケーションの pkgdef ファイル。 詳細については、「[チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
##### <a name="the-name-of-the-user-files-subfolder"></a>ユーザーファイルサブフォルダーの名前  
 *SolutionName*の "UserFilesSubFolderName" 行の値を変更することによって、アプリケーションがユーザーファイル用に保持するフォルダーの名前を変更できます。アプリケーションの pkgdef ファイル。  
  
##### <a name="the-title-of-the-solution-tree-node-in-the-new-project-dialog"></a>[新しいプロジェクト] ダイアログのソリューションツリーノードのタイトル  
 [新しいプロジェクト] ダイアログでソリューションノードのタイトルをカスタマイズするには、 *SolutionName*の "Newprojdlgslntreのタイトル" 行の値を変更します。アプリケーションの pkgdef ファイル。  
  
##### <a name="the-installed-templates-header-in-the-new-project-dialog"></a>[新しいプロジェクト] ダイアログの [インストールされたテンプレート] ヘッダー  
 [新しいプロジェクト] ダイアログボックスの [インストールされたテンプレート] ヘッダーは、 *SolutionName*の "Newprojdlgexistingtemplates" 行の値を変更することによって変更できます。アプリケーションの pkgdef ファイル。  
  
##### <a name="whether-or-not-to-hide-miscellaneous-files-by-default"></a>その他のファイルを既定で非表示にするかどうか  
 *SolutionName*の "HideMiscellaneousFilesByDefault" 行の値を変更することで、その他のファイルを既定で非表示にするかどうかを指定できます。アプリケーションの pkgdef ファイル。 その他のファイルを非表示にするには、値を設定し、ファイルを表示するには、 `dword:00000001` 値を設定し `dword:00000000` ます。  
  
##### <a name="whether-or-not-to-disable-the-output-window"></a>出力ウィンドウを無効にするかどうか  
 *SolutionName*の "DisableOutputWindow" 行の値を変更することによって、アプリケーションの出力ウィンドウを無効にするかどうかを指定できます。アプリケーションの pkgdef ファイル。 [出力] ウィンドウを無効にするには、値を設定し、[ `dword:00000001` 出力] ウィンドウを表示するには、値を設定し `dword:00000000` ます。  
  
##### <a name="whether-or-not-to-allow-dropped-files-on-the-main-window"></a>メインウィンドウでのファイルの削除を許可するかどうか  
 *SolutionName*の "AllowsDroppedFilesOnMainWindow" 行の値を変更することによって、アプリケーションのメインウィンドウでの削除されたファイルを許可するかどうかを指定できます。アプリケーションの pkgdef ファイル。 削除されたファイルを許可するには、値を設定し、削除されたファイルを許可しないように `dword:00000001` するには、値を設定し `dword:00000000` ます。  
  
##### <a name="the-default-search-page"></a>既定の検索ページ  
 Web ブラウザーのページをカスタマイズするには、 *SolutionName*の "DefaultSearchPage" 行の値を変更して、web ブラウザーウィンドウを開いたときに表示されるページをカスタマイズします。アプリケーションの pkgdef ファイル。  
  
##### <a name="the-default-home-page"></a>既定のホームページ  
 ホームページをカスタマイズするには、 *SolutionName*の "DefaultHomePage" 行の値を変更します。アプリケーションの pkgdef ファイル。 詳細については、「[チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
##### <a name="whether-or-not-to-hide-the-solution-concept"></a>ソリューションの概念を非表示にするかどうか  
 *SolutionName*の "HideSolutionConcept" 行の値を変更することによって、アプリケーションのソリューションを非表示にするかどうかを指定できます。アプリケーションの pkgdef ファイル。 ソリューションを非表示にするには、値を設定し、 `dword:00000001` ソリューションを表示するには値を設定し `dword:00000000` ます。  
  
##### <a name="the-default-debug-engine"></a>既定のデバッグエンジン  
 *SolutionName*の "DefaultDebugEngine" 行の値を変更することで、アプリケーションで使用するデバッグエンジンを変更できます。アプリケーションの pkgdef ファイルをデバッグエンジンの GUID に適用します。  
  
##### <a name="the-file-extension-of-the-user-options-file"></a>ユーザーオプションファイルのファイル拡張子  
 *SolutionName*の "UserOptsFileExt" 行の値を変更することによって、ユーザーファイルに対してアプリケーションで保持されるフォルダーの名前を変更できます。アプリケーションの pkgdef ファイル。  
  
##### <a name="the-solution-file-extension"></a>ソリューションファイルの拡張子  
 ソリューションファイルに使用する拡張機能を変更するには、 *SolutionName*の "SolutionFileExt" 行の値を変更します。アプリケーションの pkgdef ファイル。  
  
##### <a name="the-default-user-files-folder-root"></a>既定のユーザーファイルフォルダーのルート  
 *SolutionName*の "UserFilesSubFolderName" 行の値を変更することによって、アプリケーションのユーザーファイルのルートフォルダーの名前を変更できます。アプリケーションの pkgdef ファイル。  
  
##### <a name="the-solution-file-creator-identifier"></a>ソリューションファイル作成者識別子  
 ソリューションファイルに使用される識別子を変更するには、 *SolutionName*の "SolutionFileCreatorIdentifier" 行の値を変更します。アプリケーションの pkgdef ファイル。  
  
##### <a name="the-default-projects-location"></a>既定のプロジェクトの場所  
 既定のプロジェクトの場所の名前を変更するには、 *SolutionName*の "Defaultprojects location" 行の値を変更します。アプリケーションの pkgdef ファイル。  
  
##### <a name="the-application-localization-package"></a>アプリケーションローカライズパッケージ  
 *SolutionName*の "AppLocalizationPackage" 行の値を変更することで、アプリケーションで使用するローカライズパッケージを変更できます。アプリケーションの pkgdef ファイル。  
  
##### <a name="whether-or-not-to-show-the-hierarchy-root-in-the-title"></a>タイトルに階層のルートを表示するかどうか  
 *SolutionName*の "ShowHierarchyRootInTitle" 行の値を変更することによって、アプリケーションのタイトルバーに階層のルートを表示するかどうかを指定できます。アプリケーションの pkgdef ファイル。 階層のルートを表示するには、値 `dword:00000001` を設定し、階層のルートを非表示にするには、値を設定し `dword:00000000` ます。  
  
##### <a name="specifying-a-start-page"></a>スタートページの指定  
 カスタムアプリケーションのスタートページを指定するには、 *SolutionName*を使用します。アプリケーションの pkgdef ファイルを指定し、"DisableStartPage" の値をに設定 `dword:00000000` し、 `[$RootKey$\StartPage\Default]` URI を .xaml ファイルの場所に設定します。  
  
```  
DisableStartPage=dword:00000000  
[$RootKey$\StartPage\Default]  
"Uri"="$RootFolder$\<name of XAML file>"  
```  
  
 *SolutionName*UI プロジェクトの applicationcommands. vsct ファイルで、"No_ShellPkg_startPageCommand" エントリをコメントアウトします。  
  
```  
<!--<Define name="No_ShellPkg_StartPageCommand"/>-->  
```  
  
 *SolutionName*プロジェクトには、必要な .xaml ファイルとグラフィックスファイルを追加する必要があります。 これらのファイルは、実際には *SolutionName* プロジェクトディレクトリにコピーする必要があり、他のディレクトリからは追加されません。  
  
 ファイルが *$RootFolder $* ディレクトリにコピーされるようにするには、すべてのファイルで [**項目の種類**] プロパティを [**分離シェルファイル**] に設定します。 ( **項目の種類** のプロパティを設定するには、ファイルを右クリックし、[ **プロパティ**] を選択します。 このプロパティは、[ **構成プロパティ**]、[ **全般**] の下にあります)。  
  
 スタートページのカスタマイズの詳細については、「 [スタートページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)」を参照してください。  
  
## <a name="using-other-elements-of-the-isolated-shell"></a>分離シェルのその他の要素の使用  
 分離シェルソリューションテンプレートに含まれている他のファイルやプロジェクトを使用して、アプリケーションをさらにカスタマイズすることができます。  
  
##### <a name="enabledisable-visual-studio-packages"></a>Visual Studio パッケージを有効/無効にする  
 *SolutionName*を使用すると、特定のパッケージを除外することによって、特定の種類の Visual Studio 機能を無効にすることができます。 たとえば、次の行になります。  
  
```  
[$RootKey$\Projects\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3}\AddItemTemplates\TemplateDirs\{39c9c826-8ef8-4079-8c95-428f5b1c323f}]  
```  
  
 [ **新しいプロジェクト** ] ダイアログに表示される一連のプロジェクトテンプレートから、その他のファイルプロジェクトを削除します。 詳細については、「 [チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
##### <a name="enabledisable-menu-commands"></a>メニューコマンドを有効または無効にする  
 *SolutionName*ファイルには、分離シェルで使用できるすべてのメニューコマンドのコメントアウトされた一覧が含まれています。 特定のコマンドを無効にするには、対応する行のコメントを解除します。 たとえば、ウィンドウ/分割コメントを無効にするには、行のコメントを解除し `<Define name="No_SplitCommand"/>` ます。 詳細については、「 [チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
##### <a name="the-bitmap-used-on-the-splash-screen"></a>スプラッシュスクリーンで使用されるビットマップ  
 スプラッシュスクリーンで使用するビットマップ (アプリケーションの起動時に表示されるウィンドウ) は、 *SolutionName*の "SplashScreenBitmap" 行の値を変更することによってカスタマイズできます。アプリケーションの pkgdef ファイル。 詳細については、「 [チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
##### <a name="the-helpabout-window"></a>[ヘルプ/バージョン情報] ウィンドウ  
 分離シェルテンプレートには、アプリケーションの [ヘルプ]/[バージョン情報] ボックスをカスタマイズするために使用できる別のプロジェクトがあります。 詳細については、「 [チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。
