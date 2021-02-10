---
title: 単一および複数のタブのビュー |Microsoft Docs
description: コードエディターウィンドウやフォームデザイナーなど、複数のタブから成るビューをエディターで実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - single and multi-tab views
ms.assetid: e3611704-349f-4323-b03c-f2b0a445d781
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6cea04557fb0bf3075461b22979cac2168af322
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942985"
---
# <a name="single-and-multi-tab-views"></a>単一タブと複数タブのビュー
エディターでは、さまざまな種類のビューを作成できます。 例として、コードエディターウィンドウがあり、もう1つはフォームデザイナーです。

 複数のタブからなるビューは、複数のタブを持つビューです。 たとえば、HTML エディターの下部には、[ **デザイン** ] タブと [ **ソース**] タブの2つのタブがあり、それぞれ論理ビューが表示されます。 デザインビューには、レンダリングされた web ページが表示されます。一方、web ページで構成されている HTML が表示されます。

## <a name="accessing-physical-views"></a>物理ビューへのアクセス
 物理ビューは、ドキュメントビューオブジェクトをホストします。各オブジェクトは、コードやフォームなど、バッファー内のデータのビューを表します。 これにより、各ドキュメントビューオブジェクトには物理ビュー (物理ビュー文字列と呼ばれます) があり、通常は1つの論理ビューが表示されます。

 ただし、場合によっては、物理ビューに2つ以上の論理ビューを含めることができます。 例としては、サイドバイサイドビューを備えた分割ウィンドウがあるエディターや、GUI/デザインビューとフォームビューのビューを持つフォームデザイナーがあります。

 エディターが使用可能なすべての物理ビューにアクセスできるようにするには、エディターファクトリで作成できるドキュメントビューオブジェクトの種類ごとに一意の物理ビュー文字列を作成する必要があります。 たとえば、 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] エディターファクトリは、コードウィンドウとフォームデザイナーウィンドウのドキュメントビューオブジェクトを作成できます。

## <a name="creating-multi-tabbed-views"></a>複数のタブ付きビューの作成
 ドキュメントビューオブジェクトは、一意の物理ビュー文字列を使用して物理ビューに関連付けられている必要がありますが、複数のタブを物理ビュー内に配置することで、さまざまな方法でデータを表示することができます。 この複数タブの構成では、すべてのタブが同じ物理ビュー文字列に関連付けられていますが、各タブには異なる論理ビュー GUID が割り当てられています。

 エディター用の複数のタブ付きビューを作成するには、インターフェイスを実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView> してから、作成し <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID> た各タブに別の論理ビュー GUID () を関連付けます。

 Visual Studio HTML エディターは、複数のタブが表示されたエディターの一例です。 これには、[ **デザイン** ] タブと [ **ソース** ] タブがあります。 これを有効にするには、[ `LOGICALVIEWID_TextView` **デザイン** ] タブと [ `LOGICALVIEWID_Code` **ソース** ] タブの各タブに、別の論理ビューが関連付けられています。

 適切な論理ビューを指定することにより、VSPackage は、フォームのデザイン、コードの編集、コードのデバッグなど、特定の目的に対応するビューにアクセスできます。 ただし、windows の1つは NULL 文字列によって識別される必要があり、これはプライマリ論理ビュー () に対応する必要があり `LOGVIEWID_Primary` ます。

 次の表に、使用可能な論理ビューの値とその使用方法を示します。

|LOGVIEWID GUID|推奨される使用方法|
|--------------------|---------------------|
|`LOGVIEWID_Primary`|エディターファクトリの既定/プライマリビュー。<br /><br /> すべてのエディターファクトリは、この値をサポートする必要があります。 このビューでは、物理ビュー文字列として NULL 文字列を使用する必要があります。 少なくとも1つの論理ビューをこの値に設定する必要があります。|
|`LOGVIEWID_Debugging`|デバッグビュー。 通常、は `LOGVIEWID_Debugging` と同じビューにマップさ `LOGVIEWID_Code` れます。|
|`LOGVIEWID_Code`|[ **コードの表示** ] コマンドによって起動されたビュー。|
|`LOGVIEWID_Designer`|**フォームの表示** コマンドによって起動されたビュー。|
|`LOGVIEWID_TextView`|テキストエディタービュー。 これは、にアクセスするためのを返すビューです <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。|
|`LOGVIEWID_UserChooseView`|使用するビューを選択するようにユーザーに求めます。|
|`LOGVIEWID_ProjectSpecificEditor`|[ファイルを **開くアプリケーション** の選択] ダイアログボックスで<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> ユーザーが "(プロジェクトの既定のエディター)" エントリを選択したとき。|

 論理ビュー Guid は拡張可能ですが、VSPackage で定義されている論理ビュー Guid のみを使用できます。

 シャットダウン時に、Visual Studio は、エディターファクトリの GUID とドキュメントウィンドウに関連付けられている物理ビュー文字列を保持します。これにより、ソリューションを再度開いたときにドキュメントウィンドウを再び開くために使用できるようになります。 ソリューションが閉じられたときに開いていたウィンドウだけが、ソリューション (.suo) ファイルに保存されます。 これらの値は、 `VSFPROPID_guidEditorType` メソッドのパラメーターで渡される値と値に対応し `VSFPROPID_pszPhysicalView` `propid` <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> ます。

## <a name="example"></a>例
 このスニペットは、を <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView> 実装するビューにオブジェクトを使用してアクセスする方法を示してい `IVsCodeWindow` ます。 この場合、サービスは、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> ウィンドウフレームへのポインターを取得するとを呼び出すために使用され <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> `LOGVIEWID_TextView` ます。 ドキュメントビューオブジェクトへのポインターは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> を呼び出し、の値を指定することによって取得され `VSFPROPID_DocView` ます。 ドキュメントビューオブジェクトから、 `QueryInterface` が呼び出され `IVsCodeWindow` ます。 この場合は、テキストエディターが返されるため、メソッドで返されるドキュメントビューオブジェクト <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> がコードウィンドウになります。

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
