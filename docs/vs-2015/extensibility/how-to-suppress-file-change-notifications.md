---
title: '方法: ファイル変更通知を抑制する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - suppress file change notification
ms.assetid: 891c1eb4-f6d0-4073-8df0-2859dbd417ca
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3f045175eae165b75a887ada2716b19f34fc228b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204076"
---
# <a name="how-to-suppress-file-change-notifications"></a>方法: ファイル変更通知を抑制する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストバッファーを表す物理ファイルが変更されると、ダイアログボックスに、**次の項目への変更を保存するかどうかを確認**するメッセージが表示されます。 これはファイル変更通知と呼ばれます。 ただし、ファイルに多くの変更が加えられる場合、このダイアログボックスは何度も表示されます。  
  
 次の手順を使用して、このダイアログボックスをプログラムによって非表示にすることができます。 これにより、ユーザーに毎回変更を保存するように求めるメッセージが表示されることなく、すぐにファイルを再度読み込むことができます。  
  
### <a name="to-suppress-file-change-notification"></a>ファイル変更通知を抑制するには  
  
1. メソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> 開いているファイルに関連付けられているテキストバッファーオブジェクトを確認します。  
  
2. <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl> <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> (ドキュメントデータ) オブジェクトからインターフェイスを取得し、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl.IgnoreFileChanges%2A> `fIgnore` パラメーターをに設定してメソッドを実装することにより、メモリ内のオブジェクトをダイレクトして監視ファイルの変更を無視し `true` ます。  
  
3. およびインターフェイスのメソッドを呼び出して、ファイルの変更を使用して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> メモリ内のオブジェクトを更新し <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> ます (フィールドがコンポーネントに追加されたときなど)。  
  
4. ユーザーが処理している保留中の編集を考慮せずに、ディスク上のファイルを更新します。  
  
     このようにして、 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> ファイル変更通知の監視を再開するようにオブジェクトに指示すると、メモリ内のテキストバッファーには、生成した変更と他のすべての保留中の編集が反映されます。 ディスク上のファイルには、ユーザーが生成した最新のコードと、ユーザーが編集したコードで以前に保存した変更が反映されます。  
  
5. メソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl.IgnoreFileChanges%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> て、パラメーターをに設定して、ファイル変更通知の監視を再開するようにオブジェクトに通知し `fIgnore` `false` ます。  
  
6. ソースコード管理 (SCC) の場合と同様に、ファイルにいくつかの変更を加える場合は、ファイル変更通知を一時的に中断するようにグローバルファイル変更サービスに指示する必要があります。  
  
     たとえば、ファイルを書き換えてタイムスタンプを変更した場合は、書き換え操作と timestample な操作がそれぞれ個別のファイル変更イベントとしてカウントされるので、ファイル変更通知を中断する必要があります。 グローバルファイル変更通知を有効にするには、代わりにメソッドを呼び出す必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx.IgnoreFile%2A> ます。  
  
## <a name="example"></a>例  
 次に、ファイル変更の通知を抑制する方法を示します。  
  
```cpp#  
//Misc. helper classes  
  
CSuspendFileChanges::CSuspendFileChanges(  
    /* [in] */ const CString& strMkDocument,   
    /* [in] */ BOOL fSuspendNow /* = TRUE */)   
:  
    m_strMkDocument(strMkDocument),  
    m_fFileChangeSuspended(FALSE)  
{  
    if(fSuspendNow)  
        Suspend();  
}  
CSuspendFileChanges::~CSuspendFileChanges()  
{  
    Resume();  
}  
void CSuspendFileChanges::Suspend()  
{  
    USES_CONVERSION;  
  
    // Prevent suspend from suspending more than once.  
    if(m_fFileChangeSuspended)  
        return;  
  
    IVsRunningDocumentTable* pRDT =   
      _VxModule.GetIVsRunningDocumentTable();  
    ASSERT(pRDT);  
    if (!pRDT)  
        return;  
  
    CComPtr<IUnknown> srpDocData;  
    VSCOOKIE vscookie = VSCOOKIE_NIL;  
    pRDT->FindAndLockDocument(RDT_NoLock, T2COLE(m_strMkDocument),    
      NULL, NULL, &srpDocData, &vscookie);  
    if ( (vscookie == VSCOOKIE_NIL) || !srpDocData)  
        return;  
    CComPtr<IVsFileChangeEx> srpIVsFileChangeEx;  
    HRESULT hr = _VxModule.QueryService(SID_SVsFileChangeEx,   
      IID_IVsFileChangeEx, (void **)&srpIVsFileChangeEx);  
    if (SUCCEEDED(hr) && srpIVsFileChangeEx)  
    {  
        m_fFileChangeSuspended = TRUE;  
        srpIVsFileChangeEx->IgnoreFile(NULL, m_strMkDocument, TRUE);   
        srpDocData->QueryInterface(IID_IVsDocDataFileChangeControl,   
          (void**)&m_srpIVsDocDataFileChangeControl);  
        if(m_srpIVsDocDataFileChangeControl)  
            m_srpIVsDocDataFileChangeControl->IgnoreFileChanges(TRUE);  
    }  
}  
void CSuspendFileChanges::Resume()  
{  
    if(!m_fFileChangeSuspended)  
        return;  
  
    CComPtr<IVsFileChangeEx> srpIVsFileChangeEx;  
    HRESULT hr = _VxModule.QueryService(SID_SVsFileChangeEx,   
      IID_IVsFileChangeEx, (void **)&srpIVsFileChangeEx);  
    if (SUCCEEDED(hr) && srpIVsFileChangeEx)  
  
    srpIVsFileChangeEx->IgnoreFile(NULL, m_strMkDocument, FALSE);   
    if(m_srpIVsDocDataFileChangeControl)  
        m_srpIVsDocDataFileChangeControl->IgnoreFileChanges(FALSE);  
    m_fFileChangeSuspended = FALSE;  
    m_srpIVsDocDataFileChangeControl.Release();  
}  
// Misc. helper classes  
```  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 SCC の場合のように、ファイルに複数の変更が含まれている場合は、ファイルの変更の監視を再開するために、グローバルファイル変更通知を再開してからドキュメントデータにアラートを生成することが重要です。
