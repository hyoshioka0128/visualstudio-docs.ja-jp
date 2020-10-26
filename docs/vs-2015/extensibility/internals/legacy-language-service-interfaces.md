---
title: 従来の言語サービスインターフェイス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 02f63cd5e3f0599723aee12f7aed2c56b74c3249
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196098"
---
# <a name="legacy-language-service-interfaces"></a>従来の言語サービスのインターフェイス
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

特定のプログラミング言語では、言語サービスのインスタンスは一度に1つしか存在できません。 ただし、1つの言語サービスで複数のエディターを使用できます。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] では、言語サービスが特定のエディターに関連付けられません。 そのため、言語サービス操作を要求する場合は、適切なエディターをパラメーターとして指定する必要があります。  
  
## <a name="common-interfaces-associated-with-language-services"></a>言語サービスに関連付けられている共通のインターフェイス  
 エディターは、適切な VSPackage でを呼び出すことによって、言語サービスを取得し <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> ます。 この呼び出しで渡されるサービス ID (SID) は、要求されている言語サービスを識別します。  
  
 コア言語サービスインターフェイスは、任意の数の独立したクラスに実装できます。 ただし、一般的な方法は、1つのクラスに次のインターフェイスを実装することです。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock> (省略可)  
  
  インターフェイスは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> すべての言語サービスに実装する必要があります。 言語のローカライズされた名前、言語サービスに関連付けられているファイル名拡張子、色計を取得する方法など、言語サービスに関する情報を提供します。  
  
## <a name="additional-language-service-interfaces"></a>追加の言語サービスインターフェイス  
 その他のインターフェイスは、言語サービスで提供できます。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] テキストバッファーのインスタンスごとに、これらのインターフェイスの個別のインスタンスを要求します。 そのため、これらの各インターフェイスを独自のオブジェクトに実装する必要があります。 次の表は、テキストバッファーインスタンスごとに1つのインスタンスを必要とするインターフェイスを示しています。  
  
|インターフェイス|説明|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|ドロップダウンバーなどのコードウィンドウの表示要素を管理します。 このインターフェイスは、メソッドを使用して取得でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> ます。 コードウィンドウごとに1つずつ存在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|色づけ言語のキーワードと区切り記号。 このインターフェイスは、メソッドを使用して取得でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> ます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> は、描画時に呼び出されます。 計算集中型の作業を避けて <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> ください。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|IntelliSense パラメーターのヒントを提供します。 言語サービスが、メソッドのデータを表示する必要があることを示す文字 (始めかっこなど) を認識すると、メソッドを呼び出して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> 言語サービスがパラメーターヒントを表示する準備ができていることをテキストビューに通知します。 次に、テキストビューは、インターフェイスのメソッドを使用して言語サービスにコールバックし、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> ツールヒントを表示するために必要な情報を取得します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|IntelliSense ステートメント入力候補を提供します。 言語サービスがコンプリートリストを表示する準備ができたら、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> テキストビューでメソッドを呼び出します。 その後、テキストビューは、オブジェクトのメソッドを使用して、言語サービスにコールバックし <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> ます。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|コマンドハンドラーを使用してテキストビューを変更できるようにします。 インターフェイスを実装するクラスは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> インターフェイスも実装する必要があり <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。 テキストビューでは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> メソッドに渡されたオブジェクトをクエリすることによって、オブジェクトを取得し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> ます。 ビューごとに1つのオブジェクトが存在する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> ます。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|ユーザーがコードウィンドウに入力するコマンドをインターセプトします。 実装からの出力を監視して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> カスタムの完了情報とビューの変更を提供する<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>オブジェクトをテキストビューに渡すには、を呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> ます。|  
  
## <a name="see-also"></a>参照  
 [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)   
 [チェックリスト: 従来の言語サービスの作成](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)
