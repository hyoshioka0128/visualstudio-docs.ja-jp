---
title: レガシー言語サービスのモデル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, model
ms.assetid: d8ae1c0c-ee3d-4937-a581-ee78d0499793
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7f024a02641902843f673ce3ff8583a4bce3b135
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707045"
---
# <a name="model-of-a-legacy-language-service"></a>従来の言語サービスのモデル
言語サービスは、特定の言語の要素と機能を定義し、その言語に固有の情報をエディターに提供するために使用されます。 たとえば、構文の色分けをサポートするためには、言語の要素とキーワードをエディタが知る必要があります。

 言語サービスは、エディターによって管理されるテキスト バッファーとエディターを含むビューと密接に連携します。 言語サービスによって提供される機能の一例は、Microsoft IntelliSense**クイック ヒント**オプションです。

## <a name="a-minimal-language-service"></a>最小限の言語サービス
 最も基本的な言語サービスには、次の 2 つのオブジェクトが含まれています。

- *言語サービス*は、インターフェイスを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>実装します。 言語サービスには、言語名、ファイル名拡張子、コード ウィンドウ マネージャ、およびカラー化プログラムなどの言語に関する情報が含まれています。

- *カラー化プログラム*はインターフェイスを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>実装します。

  次の概念図は、基本的な言語サービスのモデルを示しています。

  ![言語サービス モデル グラフィック](../../extensibility/media/vslanguageservicemodel.gif "を使用します。")基本言語サービスモデル

  ドキュメントウィンドウは、エディタの*ドキュメントビュー* (この場合はコアエディタ)[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]をホストします。 ドキュメント ビューとテキスト バッファーは、エディターによって所有されます。 これらのオブジェクトは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]*コード ウィンドウ*と呼ばれる専用のドキュメント ウィンドウを通じて動作します。 コード ウィンドウは、IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>によって作成および制御されるオブジェクトに含まれています。

  指定された拡張子を持つファイルが読み込まれると、エディターはその拡張機能に関連付けられている言語サービスを検索し、メソッドを呼び出<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>すことによってコード ウィンドウに渡します。 言語サービスは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>インターフェイスを実装するコード ウィンドウ*マネージャー*を返します。

  次の表に、モデル内のオブジェクトの概要を示します。

| コンポーネント | Object | 関数 |
|------------------| - | - |
| テキスト バッファー | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> | Unicode 読み取り/書き込みテキスト ストリーム。 テキストは他のエンコーディングを使用できます。 |
| [コード ウィンドウ] | <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> | 1 つ以上のテキスト ビューを含むドキュメント ウィンドウ。 マルチ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ドキュメント インターフェイス (MDI) モードの場合、コード ウィンドウは MDI 子です。 |
| テキストビュー | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> | キーボードとマウスを使用してテキストをナビゲートおよび表示できるウィンドウ。 テキスト ビューは、エディターとしてユーザーに表示されます。 テキスト ビューは、通常のエディター ウィンドウ、[出力] ウィンドウ、および [イミディエイト] ウィンドウで使用できます。 さらに、コード ウィンドウ内で 1 つまたは複数のテキスト ビューを構成できます。 |
| テキストマネージャー | <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>サービスによって管理され、そこからポインターを取得します<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager>。 | 前述したすべてのコンポーネントで共有される共通の情報を保持するコンポーネント。 |
| 言語サービス | 実装依存;実装<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> | 構文の強調表示、ステートメント入力候補、かっこの一致などの言語固有の情報をエディターに提供するオブジェクト。 |

## <a name="see-also"></a>関連項目
- [カスタム エディターでのドキュメント データとドキュメント ビュー](../../extensibility/document-data-and-document-view-in-custom-editors.md)
