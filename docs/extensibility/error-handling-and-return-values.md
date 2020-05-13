---
title: エラー処理と戻り値 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- errors [Visual Studio SDK], handling
- error handling
- return values
ms.assetid: b2d9079d-39a6-438a-8010-290056694b5c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 30b6b9bff9056360f9ea840f47b1488f05bee872
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711930"
---
# <a name="error-handling-and-return-values"></a>エラー処理と戻り値
VSPackage と COM は、エラーに対して同じアーキテクチャを使用します。 および`SetErrorInfo``GetErrorInfo`関数は、Win32 アプリケーション プログラミング インターフェイス (API) の一部です。 統合開発環境 (IDE) 内の VSPackage は、エラー通知を受信したときに、リッチ エラー情報を記録するこれらのグローバル Win32 API を呼び出すことができます。 には[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]、エラー情報を管理するための相互運用機能アセンブリが用意されています。

## <a name="interop-methods"></a>相互運用メソッド
 利便性のため、IDE には、Win32 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>API を呼び出す代わりに使用するメソッドが用意されています。 マネージ コードでは<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>、 を使用します。 エラー メッセージ`HRESULT`が表示されるレベル (コマンド ハンドラを実装<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>するオブジェクトの場合が多い) にエラーが発生した場合、IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>は別のメソッドを使用して適切なメッセージ ボックスを表示します。 マネージ コードでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>メソッドを使用します。

 VSPackage 実装者として、COM オブジェクトは通常を`ISupportErrorInfo`実装します。 インターフェイス`ISupportErrorInfo`は、リッチ エラー情報がコール チェーンの垂直方向に移動できることを保証します。 複数のプロセスまたはスレッド間で使用されるオブジェクトは、豊富`ISupportErrorInfo`なエラー情報が呼び出し元に正しくマーシャリングされるようにサポートする必要があります。

 VSPackage に関連し、エディター ファクトリ、エディター、階層、提供サービスなど、IDE の拡張に関係するすべてのオブジェクトは、豊富なエラー情報をサポートする必要があります。 IDE では、これらの VSPackage オブジェクトを実装`ISupportErrorInfo`する必要はありませんが、常に推奨されます。

 IDE は、エラー情報を報告し、 IDE に伝搬[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]するたびに、`HRESULT`のユーザーに表示します。 IDE は、オブジェクトを作成`ErrorInfo`するためのメカニズムでもあります。

## <a name="general-guidelines"></a>一般的なガイドライン
 メソッドとメソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>を<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>使用して、VSPackage 実装の内部エラーを設定および報告することもできます。 ただし、一般的な規則として、VSPackage でエラー メッセージを処理するための次のガイドラインに従います。

- VSPackage COM オブジェクトに実装`ISupportErrorInfo`します。

- を実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A><xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>するオブジェクトでメソッドを呼び出すエラー報告機構を作成します。

- IDE で、このメソッドを使用して<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>ユーザーにエラーを表示します。

## <a name="error-information-in-the-ide"></a>IDE のエラー情報
 以下の規則は、IDE でエラー情報を[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]処理する方法を示しています。

- 古いエラー情報がユーザーに報告されないことを保証する防御策として、メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>呼び出す関数はまずメソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>を呼び出す必要があります。 新しい`null`エラー情報を設定する可能性のあるものを呼び出す前に、キャッシュされたエラー メッセージをクリアするために渡します。

- エラー メッセージを直接報告しない関数は、エラー<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>`HRESULT`を返す場合にのみメソッドを呼び出すことができます。 関数へのエントリまたはを返すときに`ErrorInfo`、 をクリアすることは許されます<xref:Microsoft.VisualStudio.VSConstants.S_OK>。 このルールの唯一の例外は、呼び出し`HRESULT`が、受信側の側が明示的に回復するか、または安全に無視できるエラーを返す場合です。

- エラー`HRESULT`を明示的に無視する当事者は、 を使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>して<xref:Microsoft.VisualStudio.VSConstants.S_OK>メソッドを呼び出す必要があります。 そうしないと、他`ErrorInfo`のパーティが独自`ErrorInfo`のを提供せずにエラーが発生したときに、オブジェクトが誤って使用される可能性があります。

- エラー`HRESULT`を発生させたすべてのメソッドは、豊富なエラー情報<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>を提供するためにメソッドを呼び出すことをお勧めします。 返された`HRESULT`エラーが特殊な`FACILITY_ITF`場合は、メソッドが適切な`ErrorInfo`オブジェクトを提供する必要があります。 返されたエラーが標準システム エラー (たとえば、 <xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY>、 <xref:Microsoft.VisualStudio.VSConstants.E_ABORT> <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG>、、<xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED>など) の場合は、メソッドを明示的に呼び出さずにエラー<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>コードを返してもかまいません。 防御的なコーディング戦略として、エラー (`HRESULT`システム エラーを含む)<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>を発生させる場合`ErrorInfo`は、エラーをより詳細に記述するか、`null`または を常にメソッドを呼び出します。

- 別の呼び出しによって発生したエラーを返すすべての関数は、オブジェクトを変更`HRESULT`せずに、失敗した呼び出しから`ErrorInfo`受け取った情報を渡す必要があります。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [エラー情報を設定します ( コンポーネントオートメーション )](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-seterrorinfo)
- [GetErrorInfo](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-geterrorinfo)
- [インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-isupporterrorinfo)
