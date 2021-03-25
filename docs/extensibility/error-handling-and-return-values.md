---
title: エラー処理と戻り値 |Microsoft Docs
description: Visual Studio SDK が相互運用機能アセンブリを提供して、エラー通知を受信したときに豊富なエラー情報を記録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- errors [Visual Studio SDK], handling
- error handling
- return values
ms.assetid: b2d9079d-39a6-438a-8010-290056694b5c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ac9c027623b34afa532f62b4b4c9443f219343e9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075264"
---
# <a name="error-handling-and-return-values"></a>エラー処理と戻り値
Vspackage と COM は、同じアーキテクチャを使用してエラーを発生させることができます。 `SetErrorInfo`関数と `GetErrorInfo` 関数は、Win32 アプリケーションプログラミングインターフェイス (API) の一部です。 統合開発環境 (IDE: integrated development environment) のすべての VSPackage は、これらのグローバル Win32 Api を呼び出して、エラー通知を受け取ったときに豊富なエラー情報を記録できます。 は、 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] エラー情報を管理する相互運用機能アセンブリを提供します。

## <a name="interop-methods"></a>相互運用メソッド
 IDE には、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> Win32 api を呼び出す代わりに、を使用するためのメソッドが用意されています。 マネージコードでは、を使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> します。 エラーメッセージが表示されるレベルでエラーが発生した場合 `HRESULT` (これは、多くの場合、コマンドハンドラーを実装しているオブジェクトです <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> )、IDE は別のメソッドであるを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 適切なメッセージボックスを表示します。 マネージコードでは、メソッドを使用し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> ます。

 VSPackage の実装者は、通常、COM オブジェクトがを実装 `ISupportErrorInfo` します。 `ISupportErrorInfo`インターフェイスにより、豊富なエラー情報が呼び出しチェーンの上下に移動することができます。 プロセス間またはスレッド間で使用される可能性のあるオブジェクトは `ISupportErrorInfo` 、豊富なエラー情報が呼び出し元に正しくマーシャリングされるようにをサポートする必要があります。

 エディターファクトリ、エディター、階層、提供されているサービスなど、Vspackage に関連し、IDE の拡張に関係するすべてのオブジェクトは、豊富なエラー情報をサポートする必要があります。 IDE では、これらの VSPackage オブジェクトを実装する必要はありません `ISupportErrorInfo` が、常に推奨されます。

 Ide は、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] `HRESULT` が ide に反映されるたびに、エラー情報をレポートしてユーザーに表示する役割を担います。 IDE は、オブジェクトを作成するためのメカニズムでも `ErrorInfo` あります。

## <a name="general-guidelines"></a>一般的なガイドライン
 メソッドとメソッドを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> VSPackage 実装の内部にあるエラーを設定し、報告することができます。 ただし、一般的な規則として、次のガイドラインに従って、VSPackage でエラーメッセージを処理します。

- `ISupportErrorInfo`VSPACKAGE COM オブジェクトにを実装します。

- を実装するオブジェクトでメソッドを呼び出すエラー報告機構を作成 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> します。

- IDE で、メソッドを使用してユーザーにエラーを表示させ <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> ます。

## <a name="error-information-in-the-ide"></a>IDE のエラー情報
 次の規則は、IDE でのエラー情報の処理方法を示してい [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

- 古いエラー情報がユーザーに報告されないことを保証するための防御戦略として、メソッドを呼び出す関数は <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 最初にメソッドを呼び出す必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> ます。 `null`新しいエラー情報を設定する可能性のあるものを呼び出す前に、キャッシュされたエラーメッセージをクリアするためにを渡します。

- エラーメッセージを直接報告しない関数は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> エラーが返された場合にのみメソッドを呼び出すことができ `HRESULT` ます。 `ErrorInfo`関数またはを返すときに、エントリのをクリアすることが <xref:Microsoft.VisualStudio.VSConstants.S_OK> できます。 この規則の唯一の例外は、 `HRESULT` 受信側が明示的に回復または安全に無視できるエラーを呼び出しが返す場合です。

- エラーを明示的に無視するすべてのパーティ `HRESULT` は、を使用してメソッドを呼び出す必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> <xref:Microsoft.VisualStudio.VSConstants.S_OK> ます。 そうしない `ErrorInfo` と、別のパーティが単独でエラーを生成するときに、オブジェクトが誤って使用されることがあり `ErrorInfo` ます。

- エラーが発生したすべてのメソッド `HRESULT` は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 豊富なエラー情報を提供するためにメソッドを呼び出すことをお勧めします。 返された `HRESULT` が特殊なエラーである場合は、 `FACILITY_ITF` 適切なオブジェクトを提供するためにメソッドが必要です `ErrorInfo` 。 返されたエラーが標準のシステムエラー (、、、など) の場合は、 <xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY> <xref:Microsoft.VisualStudio.VSConstants.E_ABORT> <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG> メソッドを <xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED> 明示的に呼び出すことなく、エラーコードを返すことができます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 防御的なコーディング方法として、エラーを発生させる `HRESULT` (システムエラーを含む) 場合は、エラーを詳細に説明するか、またはを使用して、常に <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> メソッドを呼び出し `ErrorInfo` `null` ます。

- 別の呼び出しによって発生したエラーを返すすべての関数は、 `HRESULT` オブジェクトを変更せずに、内の失敗した呼び出しから受け取った情報を渡す必要があり `ErrorInfo` ます。

## <a name="see-also"></a>こちらもご覧ください
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [SetErrorInfo (コンポーネントオートメーション)](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-seterrorinfo)
- [GetErrorInfo](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-geterrorinfo)
- [ISupportErrorInfo インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-isupporterrorinfo)
