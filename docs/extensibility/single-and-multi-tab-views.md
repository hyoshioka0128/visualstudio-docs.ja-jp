---
title: シングルタブビューとマルチタブビュー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - single and multi-tab views
ms.assetid: e3611704-349f-4323-b03c-f2b0a445d781
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c308b4d6c7b90456255019ef57c6b9d544aefc77
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699990"
---
# <a name="single-and-multi-tab-views"></a>単一タブと複数タブのビュー
エディターは、さまざまなタイプのビューを作成できます。 1 つの例はコード エディター ウィンドウ、もう 1 つはフォーム デザイナーです。

 マルチタブ ビューは、複数のタブを持つビューです。 たとえば、HTML エディタの下部には、**デザイン**と**ソース**という 2 つのタブがあり、それぞれ論理ビューがあります。 デザイン ビューにはレンダリングされた Web ページが表示され、もう一方には Web ページを構成する HTML が表示されます。

## <a name="accessing-physical-views"></a>物理ビューへのアクセス
 物理ビューは、コードやフォームなどのバッファー内のデータのビューを表す、ドキュメント ビュー オブジェクトをホストします。 したがって、各ドキュメント ビュー オブジェクトには物理ビュー (物理ビュー文字列と呼ばれるもので識別されます) があり、通常は 1 つの論理ビューがあります。

 ただし、物理ビューには複数の論理ビューを含めることができる場合があります。 たとえば、サイド バイ サイド ビューを持つ分割ウィンドウを持つエディターや、GUI/デザイン ビューとフォームビハインド ビューを持つフォーム デザイナーがあります。

 エディターで使用可能なすべての物理ビューにアクセスできるようにするには、エディター ファクトリで作成できるドキュメント ビュー オブジェクトの種類ごとに一意の物理ビュー文字列を作成する必要があります。 たとえば、エディター[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]ファクトリは、コード ウィンドウとフォーム デザイナー ウィンドウのドキュメント ビュー オブジェクトを作成できます。

## <a name="creating-multi-tabbed-views"></a>マルチタブ ビューの作成
 ドキュメント ビュー オブジェクトは、一意の物理ビュー文字列を通じて物理ビューに関連付けられている必要がありますが、物理ビュー内に複数のタブを配置して、さまざまな方法でデータを表示できます。 このマルチタブ構成では、すべてのタブが同じ物理ビュー文字列に関連付けられますが、各タブには異なる論理ビュー GUID が与えられます。

 エディターのマルチタブ ビューを作成するには、インターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView>実装し、作成する各タブに異なる論理ビュー<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID>GUID ( ) を関連付けます。

 Visual Studio HTML エディターは、マルチタブ ビューを使用したエディターの例です。 **[デザイン]** タブと **[ソース]** タブがあります。 これを有効にするには、各タブの **[デザイン**] タブと [**ソース**]`LOGICALVIEWID_Code`タブに対して、`LOGICALVIEWID_TextView`異なる論理ビューが関連付けられます。

 適切な論理ビューを指定することにより、VSPackage は、フォームのデザイン、コードの編集、コードのデバッグなど、特定の目的に対応するビューにアクセスできます。 ただし、ウィンドウの 1 つは NULL 文字列で識別する必要があり、これはプライマリ論理ビュー`LOGVIEWID_Primary`( ) に対応している必要があります。

 次の表に、使用可能な論理ビューの値とその使用方法を示します。

|LOGVIEWID GUID|推奨用途|
|--------------------|---------------------|
|`LOGVIEWID_Primary`|エディター ファクトリの既定/プライマリ ビュー。<br /><br /> すべてのエディター ファクトリがこの値をサポートする必要があります。 このビューは、物理ビュー文字列として NULL 文字列を使用する必要があります。 少なくとも 1 つの論理ビューがこの値に設定されている必要があります。|
|`LOGVIEWID_Debugging`|デバッグ ビュー。 通常、`LOGVIEWID_Debugging`と同じビューにマップ`LOGVIEWID_Code`します。|
|`LOGVIEWID_Code`|[**コードの表示**] コマンドによって起動されたビュー。|
|`LOGVIEWID_Designer`|[**フォームの表示**] コマンドによって起動されたビュー。|
|`LOGVIEWID_TextView`|テキスト エディタ ビュー。 これは、 を返<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>すビューで、 にアクセス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>できます。|
|`LOGVIEWID_UserChooseView`|使用するビューを選択するようユーザーに求めます。|
|`LOGVIEWID_ProjectSpecificEditor`|[ファイルを**開く**] ダイアログ ボックスによって渡された<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> ユーザーが 「(プロジェクトの既定のエディター)」エントリを選択するとします。|

 論理ビューの GUID は拡張可能ですが、VSPackage で定義されている論理ビューの GUID のみを使用できます。

 Visual Studio は、シャットダウン時にエディター ファクトリの GUID とドキュメント ウィンドウに関連付けられた物理ビュー文字列を保持し、ソリューションを再び開いたときにドキュメント ウィンドウを再び開くために使用できるようにします。 ソリューションが閉じられたときに開いているウィンドウだけが、ソリューション (.suo) ファイルに保存されます。 `VSFPROPID_guidEditorType`これらの値は`VSFPROPID_pszPhysicalView`、`propid`<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>メソッドのパラメーターで渡される 値と に対応します。

## <a name="example"></a>例
 このスニペットは、オブジェクトを<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView>使用して を実装するビューにアクセスする`IVsCodeWindow`方法を示しています。 この場合、<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>サービスは、ウィンドウ フレームへの<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A>ポインターを`LOGVIEWID_TextView`取得するを呼び出し、要求に使用されます。 ドキュメント ビュー オブジェクトへのポインターは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>`VSFPROPID_DocView`の値を呼び出して指定することによって取得されます。 ドキュメント ビュー オブジェクトから`QueryInterface`、 に`IVsCodeWindow`対して呼び出されます。 この場合、テキスト エディターが返されるため、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>メソッドで返されるドキュメント ビュー オブジェクトはコード ウィンドウです。

```cpp
HRESULT CFindTool::GotoFileLocation(const WCHAR * szFile, long iLine, long iStart, long iLen)
{
  HRESULT hr;
  if (NULL == szFile || !*szFile)
    return E_INVALIDARG;

  if (iLine == -1L)
    return S_FALSE;

  VSITEMID                  itemid;
  VARIANT                   var;
  RECT                      rc;
  IVsUIShellOpenDocument *  pOpenDoc    = NULL;
  IVsCodeWindow *           pCodeWin    = NULL;
  IVsTextView *             pTextView   = NULL;
  IVsUIHierarchy *          pHierarchy  = NULL;
  IVsWindowFrame *          pFrame      = NULL;
  IUnknown *                pUnk        = NULL;
  IVsHighlight *            pHighlight  = NULL;

  IfFailGo(CGlobalServiceProvider::HrQueryService(SID_SVsUIShellOpenDocument, IID_IVsUIShellOpenDocument, (void **)&pOpenDoc));
  IfFailGo(pOpenDoc->OpenDocumentViaProject(szFile, LOGVIEWID_TextView, NULL, &pHierarchy, &itemid, &pFrame));
  pFrame->Show();
  VariantInit(&var);
  IfFailGo(pFrame->GetProperty(VSFPROPID_DocView, &var));
  if (VT_UNKNOWN != var.vt) { hr = E_FAIL; goto Error; }
  pUnk = V_UNKNOWN(&var);
  if (NULL != pUnk)
  {
    IfFailGo(pUnk->QueryInterface(IID_IVsCodeWindow, (void **)&pCodeWin));
    if (SUCCEEDED(hr = pCodeWin->GetLastActiveView(&pTextView)) ||
        SUCCEEDED(hr = pCodeWin->GetPrimaryView(&pTextView)) )
    {
      pTextView->SetSelection(iLine, iStart, iLine, iStart + iLen);
      // uncover selection
      IfFailGo(pTextView->QueryInterface(IID_IVsHighlight, (void**)&pHighlight));
      IfFailGo(SUCCEEDED(pHighlight->GetHighlightRect(&rc)));
      UncoverSelectionRect(&rc);
    }
  }

Error:
  CLEARINTERFACE(pHighlight);
  CLEARINTERFACE(pTextView);
  CLEARINTERFACE(pCodeWin);
  CLEARINTERFACE(pUnk);
  CLEARINTERFACE(pFrame);
  CLEARINTERFACE(pOpenDoc);
  CLEARINTERFACE(pHierarchy);
  RedrawWindow(m_hwndResults, NULL, NULL, RDW_ERASE|RDW_FRAME|RDW_INVALIDATE|RDW_ALLCHILDREN);
  return hr;
}
```

## <a name="see-also"></a>関連項目
- [複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)
- [方法: ビューをドキュメントデータに添付する](../extensibility/how-to-attach-views-to-document-data.md)
- [カスタム エディターとデザイナーの作成](../extensibility/creating-custom-editors-and-designers.md)
