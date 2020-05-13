---
title: レガシー言語サービスインタフェース |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89d80d6961f5eaf91721567ccb0efa73bbe31406
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707382"
---
# <a name="legacy-language-service-interfaces"></a>従来の言語サービスのインターフェイス
特定のプログラミング言語の場合、言語サービスのインスタンスは一度に 1 つしか存在できません。 ただし、1 つの言語サービスは複数のエディターを提供できます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]言語サービスを特定のエディターに関連付けりません。 そのため、言語サービス操作を要求する場合は、適切なエディターをパラメーターとして指定する必要があります。

## <a name="common-interfaces-associated-with-language-services"></a>言語サービスに関連付けられた共通インタフェース
 エディターは、適切な VSPackage<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>を呼び出すことによって、言語サービスを取得します。 この呼び出しで渡されるサービス ID (SID) は、要求されている言語サービスを識別します。

 コア言語サービス インターフェイスは、任意の数の独立したクラスに実装できます。 ただし、一般的なアプローチは、次のインターフェイスを 1 つのクラスに実装することです。

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock> (省略可)

  インターフェイス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>はすべての言語サービスに実装する必要があります。 ローカライズされた言語名、言語サービスに関連付けられたファイル名拡張子、カラー化器の取得方法など、言語サービスに関する情報を提供します。

## <a name="additional-language-service-interfaces"></a>その他の言語サービス インターフェイス
 他のインターフェイスは、言語サービスで提供できます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、テキスト バッファーの各インスタンスに対して、これらのインターフェイスの個別のインスタンスを要求します。 したがって、これらの各インターフェイスは、独自のオブジェクトに実装する必要があります。 次の表は、テキスト バッファー インスタンスごとに 1 つのインスタンスを必要とするインターフェイスを示しています。

|インターフェイス|説明|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|ドロップダウン バーなどのコード ウィンドウの表示要素を管理します。 このインターフェイスは、 メソッドを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>使用して取得できます。 コード ウィンドウ<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>ごとに 1 つがあります。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|言語キーワードと区切り文字を色分けします。 このインターフェイスは、 メソッドを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>使用して取得できます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>は塗装時に呼び出されます。 内部<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>での計算負荷の高い作業やパフォーマンスが低下する可能性を避けます。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|IntelliSense パラメーターのツールヒントを提供します。 言語サービスは、メソッド データを表示する必要があることを示す文字 (左かっこなど) を認識すると、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>メソッドを呼び出して、言語サービスがパラメーターヒントを表示する準備ができていることをテキスト ビューに通知します。 テキスト ビューは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>インターフェイスのメソッドを使用して言語サービスに呼び出し、ツールヒントを表示するために必要な情報を取得します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|ステートメント補完を提供します。 言語サービスは、入力候補リストを表示する準備が整ったら、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>テキスト ビューのメソッドを呼び出します。 テキスト ビューは、オブジェクトのメソッドを使用して言語サービスに<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>呼び出します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|コマンド ハンドラーを使用してテキスト ビューを変更できます。 インターフェイスを実装するクラスも、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>インターフェイスを実装する<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>必要があります。 テキスト ビューは、メソッド<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>に渡されたオブジェクトを<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>クエリすることによってオブジェクトを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>取得します。 各ビューに<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>1 つのオブジェクトが存在する必要があります。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|ユーザーがコード ウィンドウに入力したコマンドをインターセプトします。 実装からの出力を<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>監視して、カスタム完了情報を提供し、変更を表示する<br /><br /> オブジェクトをテキスト<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>ビューに渡す場合は<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>、 を呼び出します。|

## <a name="see-also"></a>関連項目
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
- [チェック リスト: 従来の言語サービスの作成](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)
