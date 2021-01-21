---
title: 従来の言語サービスのモデル |Microsoft Docs
description: 独自の言語サービスを作成するためのガイドとして、Visual Studio コアエディター用の最小限の言語サービスのこのモデルを使用します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 2928d3c09a54ea8e9548f7751381279f153643e5
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97876741"
---
# <a name="model-of-a-legacy-language-service"></a>従来の言語サービスのモデル
言語サービスは、特定の言語の要素と機能を定義し、その言語に固有の情報をエディターに提供するために使用されます。 たとえば、構文の色分けをサポートするために、エディターは言語の要素とキーワードを認識している必要があります。

 言語サービスは、エディターによって管理されるテキストバッファーと、エディターを含むビューと密接に連携します。 Microsoft IntelliSense の **クイックヒント** オプションは、言語サービスによって提供される機能の一例です。

## <a name="a-minimal-language-service"></a>最小言語サービス
 最も基本的な言語サービスには、次の2つのオブジェクトが含まれています。

- *言語サービス* は、インターフェイスを実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> ます。 言語サービスには、その言語に関する情報 (名前、ファイル名拡張子、コードウィンドウマネージャー、colorizer など) が含まれています。

- *Colorizer* は、インターフェイスを実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> ます。

  次の概念図は、基本的な言語サービスのモデルを示しています。

  ![言語サービスモデルグラフィック](../../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel") 基本言語サービスモデル

  ドキュメントウィンドウは、エディターの *ドキュメントビュー* (この場合はコアエディター) をホストし [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 ドキュメントビューとテキストバッファーは、エディターによって所有されています。 これらのオブジェクト [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、 *コードウィンドウ* と呼ばれる特殊なドキュメントウィンドウを使用して操作します。 コードウィンドウは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> IDE によって作成および制御されるオブジェクトに含まれています。

  拡張子が指定されたファイルが読み込まれると、エディターはその拡張機能に関連付けられている言語サービスを検索し、メソッドを呼び出してコードウィンドウに渡し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> ます。 言語サービスは、インターフェイスを実装する *コードウィンドウマネージャー* を返し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> ます。

  次の表に、モデル内のオブジェクトの概要を示します。

| コンポーネント | Object | 機能 |
|------------------| - | - |
| テキストバッファー | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> | Unicode の読み取り/書き込みテキストストリーム。 テキストで他のエンコーディングを使用することもできます。 |
| [コード ウィンドウ] | <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> | 1つまたは複数のテキストビューを含むドキュメントウィンドウ。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]がマルチドキュメントインターフェイス (mdi) モードの場合、コードウィンドウは mdi 子になります。 |
| テキストビュー | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> | キーボードとマウスを使用して、ユーザーがテキストを移動および表示できるウィンドウ。 ユーザーには、エディターとしてテキストビューが表示されます。 テキストビューは、通常のエディターウィンドウ、出力ウィンドウ、および [イミディエイト] ウィンドウで使用できます。 また、コードウィンドウ内で1つ以上のテキストビューを構成することもできます。 |
| テキストマネージャー | <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>ポインターを取得するサービスによって管理されます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> | 前に説明したすべてのコンポーネントによって共有される共通情報を保持するコンポーネント。 |
| 言語サービス | 実装に依存します。実装 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> | エディターに、構文の強調表示、ステートメント入力候補、中かっこの照合などの言語固有の情報を提供するオブジェクト。 |

## <a name="see-also"></a>関連項目
- [カスタム エディターでのドキュメント データとドキュメント ビュー](../../extensibility/document-data-and-document-view-in-custom-editors.md)
