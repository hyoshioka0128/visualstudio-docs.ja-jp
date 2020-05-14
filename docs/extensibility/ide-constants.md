---
title: IDE 定数 |マイクロソフトドキュメント
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- IDE, errors
- logical views
- errors [Visual Studio], IDE
- UI context constants
- constants, Visual Studio IDE
- IDE, constants
- physical views
ms.assetid: 5030e70a-241d-474a-ba8c-e3b1cf947ff0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc2eddac1cc7d7e616deb197752adf41a4d68d15
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710499"
---
# <a name="ide-constants"></a>IDE 定数

この<xref:Microsoft.VisualStudio.VSConstants>クラスは、統合開発環境 (IDE) に固有で、以前はヘッダー ファイルでのみ定義された定数を提供します。

## <a name="logical-and-physical-views"></a>論理ビューと物理ビュー

|[値]|説明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーは、この値を<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>メソッドに渡して、[**ファイルを開く**] ダイアログ ボックス (この場合は可能なコード ビュー) を取得する必要があります。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーはこの値を<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>メソッドに渡して [**ファイルを開く**] ダイアログ ボックスを取得<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid><xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>します。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Designer_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーはこの値を<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>メソッドに渡して、[**開く**] ダイアログ ボックスを取得**します**。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Primary_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーはこの値を<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>メソッドに渡して、[**ファイルを開く**] ダイアログ ボックス (この場合はエディター ファクトリの既定/プライマリ ビュー) を取得します。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.TextView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーは、この値を<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>メソッドに渡して、ドキュメントまたはデータ テキスト エディター ビューの [**ファイルの選択]** ダイアログ ボックスを取得します。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.UserChooseView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーは<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>、使用するユーザー定義ビューを選択するようにユーザーに求めるメソッドにこの値を渡します。|

## <a name="editor-factory-flags"></a>エディタファクトリフラグ

|[値]|説明|
|-----------|-----------------|
|[Cef。クローンファイル](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>メソッドの最初のパラメータとしてビットごとに結合された古いフラグ。|
|[Cef。オープンアスニュー](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenAsNew>)|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>メソッドの最初のパラメータとしてビットごとに組み合わせると、エディター ファクトリが必要な修正を実行する必要があることを示します。|
|[Cef。Openfile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenFile>)|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>メソッドの最初のパラメータとしてビットごとに組み合わされたこのフラグは、CEF の相互に排他的です[。クローンファイル](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>).|
|[Cef。サイレント](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_Silent>)|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>メソッドの最初のパラメーターとしてビットごとに組み合わせると、エディター ファクトリがユーザー インターフェイス (UI) を表示せずにエディターを作成する必要があることを示します。|

## <a name="visual-studio-errors"></a>ビジュアル スタジオ エラー

|[値]|説明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_BUSY>|問題のオブジェクトが既にビジー状態の場合に、インターフェイスから非同期動作に戻される定数|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>|"互換性のないドキュメント データ" に対して Visual Studio に固有のエラー HRESULT です。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PACKAGENOTLOADED>|Visual Studio に固有で、"パッケージが読み込まれていない" ことを示すエラー HRESULT です。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTALREADYEXISTS>|Visual Studio に固有のエラー HRESULT で、"プロジェクトは既に存在します" ことを示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTMIGRATIONFAILED>|Visual Studio に固有で、"プロジェクト構成に失敗しました" ことを示すエラー HRESULT です。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTNOTLOADED>|Visual Studio に固有で、"プロジェクトが読み込まれていない" ことを示すエラー HRESULT です。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONALREADYOPEN>|Visual Studio に固有のエラー HRESULT で、"ソリューションは既に開かれています" ことを示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONNOTOPEN>|Visual Studio に固有で、"ソリューションが開いていない" ことを示すエラー HRESULT です。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SPECIFYING_OUTPUT_UNSUPPORTED>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput>インターフェイスから配列を指定するためのパラメーターを持つビルド インターフェイスによって返されますが、実装ではすべての出力に対してのみメソッドを適用できます。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>|ドキュメント<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>の形式がエディターで開けない場合、この値を返します。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_WIZARDBACKBUTTONPRESS>|ユーザーが Visual Studio ウィザードで [戻る] ボタンを押したことを示す HRESULT 値。|

## <a name="visual-studio-constants"></a>ビジュアル スタジオ定数

|[値]|説明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_PROJECTFORWARDED>|Visual Studio に固有で、"プロジェクトが転送されました" ことを示すエラー HRESULT です。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_TBXMARKER>|"ツールボックス マーカー" の Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_ENTERMODAL>|モダリティの開始を示すメソッドを介して通知メッセージを<xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A>ブロードキャストするための Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_EXITMODAL>|モダリティの終了を示すメソッドを介して通知メッセージを<xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A>ブロードキャストするための Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_TOOLBARMETRICSCHANGE>|コマンド バーのメトリックが変更されたことを示すメソッドを介して通知<xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A>メッセージをブロードキャストする Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSCOOKIE_NIL>|Cookie が設定されていない場合を示す Visual Studio 固有の定数。|
|[Vsitemid。Nil](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Nil>)|プロジェクト項目の不在を表す Visual Studio 項目識別子。 この値は、現在の選択がない場合に使用されます。|
|[Vsitemid。ルート](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)|プロジェクト階層のルートを表し、1 つの項目ではなく階層全体を識別するために使用される Visual Studio 項目識別子。|
|[Vsitemid。選択](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Selection>)|現在選択されている項目を表す Visual Studio 項目識別子。|

## <a name="ivsselectionevents"></a>イヴスセレクションイベント
 IDE のコンポーネントが選択された状態を、たとえば呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A>しで説明します。

|定数|[値]|
|--------------|-----------|
|[選択要素.ドキュメントフレーム](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_DocumentFrame>)|0x2|
|[プロパティブラウザのSID](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_PropertyBrowserSID>)|0x4|
|[スタートアッププロジェクト](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_StartupProject>)|0x3|
|[ノードを元に戻す](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UndoManager>)|0x0|
|[ユーザー コンテキスト](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UserContext>)|0x5|
|[ウィンドウフレーム](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_WindowFrame>)|0x1|

## <a name="vsselelemid"></a>VSSELELEMID
 新しい選択状態を示すために使用される定数。

|定数|[値]|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|2|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|7|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|4|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|6|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|3|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|0|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|5|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|1|

## <a name="component-selector-dialog-constants"></a>コンポーネントセレクタダイアログ定数

|定数|[値]|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELCHANGED>|WM_USER + 1280|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELDBLCLICK>|WM_USER + 1281|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_CLEARSELECTION>|WM_USER + 1290|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_GETSELECTION>|WM_USER + 1287|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZELIST>|WM_USER + 1285|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZETAB>|WM_USER + 1288|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_QUERYCANSELECT>|WM_USER + 1286|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_SETMULTISELECT>|WM_USER + 1289|

## <a name="see-also"></a>関連項目

- [プロジェクトシステムを拡張するための IDE 定義コマンド](../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
