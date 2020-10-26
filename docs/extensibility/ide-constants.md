---
title: IDE 定数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80710499"
---
# <a name="ide-constants"></a>IDE 定数

クラスは、 <xref:Microsoft.VisualStudio.VSConstants> 以前にヘッダーファイルでのみ定義されていた統合開発環境 (IDE) に固有の定数を提供します。

## <a name="logical-and-physical-views"></a>論理ビューと物理ビュー

|値|説明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーは、この値をメソッドに渡して <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 、[**ファイルを開くアプリケーション**の選択] ダイアログボックス (この場合は、可能なコードビュー) を取得する必要があります。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーは、この値をメソッドに渡して [ <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> **ファイルを開くアプリケーション**の選択] ダイアログボックスを取得します。この場合は、 <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid> と同じビューにマップされるデバッグビューが設定され <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid> ます。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Designer_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーは、この値をメソッドに渡して <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 、[**ファイルを開くアプリケーション**の選択] ダイアログボックス (この場合は**フォーム**デザイナービュー) を取得します。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Primary_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーは、この値をメソッドに渡して <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 、[**ファイルを開くアプリケーション**の選択] ダイアログボックス (この場合は、エディターファクトリの既定/プライマリビュー) を取得します。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.TextView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>ハンドラーは、この `cmdidOpenWith` 値をメソッドに渡して [ファイル <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> **を開くアプリケーション** の選択] ダイアログボックスを取得します。これは、ドキュメントエディターまたはデータテキストエディタービューに使用します。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.UserChooseView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`ハンドラーは、この値をメソッドに渡して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> ユーザーが使用するユーザー定義ビューを選択するように要求します。|

## <a name="editor-factory-flags"></a>エディターファクトリフラグ

|値|説明|
|-----------|-----------------|
|[CEF.CloneFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)|メソッドの最初のパラメーターとしてビットごとに結合された古いフラグ <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> 。|
|[CEF.OpenAsNew](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenAsNew>)|メソッドの最初のパラメーターとしてビットごとに結合され <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> ます。これは、エディターファクトリが必要な修正を実行することを示します。|
|[CEF.System.windows.forms.openfiledialog.openfile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenFile>)|メソッドの最初のパラメーターとしてビットごと <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> に結合されます。このフラグは、Cef と相互に排他的です [。CloneFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)。|
|[CEF.しない](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_Silent>)|メソッドの最初のパラメーターとしてビットごとに結合さ <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> れます。これは、エディターファクトリがユーザーインターフェイス (UI) を表示せずにエディターを作成することを示します。|

## <a name="visual-studio-errors"></a>Visual Studio のエラー

|値|説明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_BUSY>|内の問題のオブジェクトが既にビジー状態である場合に、インターフェイスによって非同期動作に返される定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>|"互換性のないドキュメントデータ" の Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PACKAGENOTLOADED>|"パッケージが読み込まれていません" ことを示す、Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTALREADYEXISTS>|Visual Studio に固有のエラー HRESULT。 "プロジェクトは既に存在します" ことを示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTMIGRATIONFAILED>|Visual Studio に固有のエラー HRESULT。 "プロジェクトの構成に失敗しました。" を示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTNOTLOADED>|Visual Studio に固有の、"プロジェクトが読み込まれていません" を示すエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONALREADYOPEN>|Visual Studio に固有のエラー HRESULT。 "ソリューションは既に開いています" を示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONNOTOPEN>|Visual Studio に固有のエラー HRESULT。 "ソリューションが開いていません" を示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SPECIFYING_OUTPUT_UNSUPPORTED>|インターフェイスから配列を指定するためのパラメーターを持つビルドインターフェイスによって返され <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput> ますが、実装では、メソッドのみをすべての出力に適用できます。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>ドキュメントの形式がエディターで開けない場合、メソッドはこの値を返します。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_WIZARDBACKBUTTONPRESS>|ユーザーが Visual Studio ウィザードの [戻る] ボタンにヒットしたことを示す HRESULT 値。|

## <a name="visual-studio-constants"></a>Visual Studio の定数

|値|説明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_PROJECTFORWARDED>|Visual Studio に固有のエラー HRESULT で、"プロジェクトが転送された" ことを示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_TBXMARKER>|"ツールボックスマーカー" の Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_ENTERMODAL>|モーダルの開始を示すメソッドを介して通知メッセージをブロードキャストするために Visual Studio に固有の定数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> 。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_EXITMODAL>|モーダルの終了を示すメソッドを介して通知メッセージをブロードキャストするために Visual Studio に固有の定数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> 。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_TOOLBARMETRICSCHANGE>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A>コマンドバーのメトリックが変更されたことを示すメソッドを介して通知メッセージをブロードキャストするために Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSCOOKIE_NIL>|Cookie が設定されていないことを示す Visual Studio 固有の定数。|
|[VSITEMID.しない](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Nil>)|プロジェクト項目が存在しないことを表す Visual Studio 項目識別子。 この値は、現在選択されていない場合に使用されます。|
|[VSITEMID.ルート](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)|プロジェクト階層のルートを表す Visual Studio 項目識別子。1つの項目ではなく、階層全体を識別するために使用されます。|
|[VSITEMID.項目](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Selection>)|現在選択されている項目 (階層のルートを含むことができる項目) を表す Visual Studio の項目識別子。|

## <a name="ivsselectionevents"></a>IVsSelectionEvents
 選択された IDE のコンポーネントについて、などの呼び出しで説明し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A> ます。

|定数|値|
|--------------|-----------|
|[SelectionElement.DocumentFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_DocumentFrame>)|0x2|
|[SelectionElement. PropertyBrowserSID](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_PropertyBrowserSID>)|0x4|
|[SelectionElement. StartupProject](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_StartupProject>)|0x3|
|[SelectionElement. UndoManager](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UndoManager>)|0x0|
|[SelectionElement. UserContext](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UserContext>)|0x5|
|[SelectionElement. WindowFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_WindowFrame>)|0x1|

## <a name="vsselelemid"></a>VSSELの ID
 新しい選択状態を示すために使用される定数。

|定数|値|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|2|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|7|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|4|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|6|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|3|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|0|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|5|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|1|

## <a name="component-selector-dialog-constants"></a>コンポーネントセレクターダイアログ定数

|定数|値|
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
