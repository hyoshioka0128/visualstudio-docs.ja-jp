---
title: 従来の言語サービスの開発 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- vs.vsip.LangServWiz.langtoks
- vs.vsip.LangServWiz.welcome
- vs.vsip.LangServWiz.langSpec
- vs.vsip.LangServWiz.langInfo
- vs.vsip.LangServWiz.langServOpts
helpviewer_keywords:
- language services, developing
ms.assetid: 6151ba88-c1c3-41de-a1cc-668f494d48d1
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 36ff8335bfaf99b5826d217a48910bfd581321e9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841761"
---
# <a name="developing-a-legacy-language-service"></a>従来の言語サービスの開発
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このセクションでは、従来の言語サービスの作成に役立つトピックにリンクします。  
  
 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 言語サービスを実装する新しい方法の詳細については、「 [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。  
  
> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [従来の言語サービスのモデル](../../extensibility/internals/model-of-a-legacy-language-service.md)  
 コアエディターの最小言語サービスのモデルを提供 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] します。 このモデルは、独自の言語サービスを作成するためのガイドとして使用できます。  
  
 [従来の言語サービスのインターフェイス](../../extensibility/internals/legacy-language-service-interfaces.md)  
 言語サービスを実装するために必要なオブジェクトについて説明し、構文の強調表示、メソッドデータ、およびその他の機能を提供するために使用できる追加のオブジェクトの一覧を示します。  
  
 [従来の言語サービスのコマンドの受信](../../extensibility/internals/intercepting-legacy-language-service-commands.md)  
 言語サービスにコマンドフィルターを挿入して、テキストビューで処理されるコマンドをインターセプトする方法について説明します。  
  
 [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service2.md)  
 を使用して言語サービスを登録する方法について説明 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] します。  
  
 [デバッグのための言語サービスのサポート](../../extensibility/internals/language-service-support-for-debugging.md)  
 言語サービスがデバッガーをサポートする機能を提供する方法について説明します。  
  
 [チェックリスト: 従来の言語サービスの作成](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)  
 コアエディターの言語サービスを作成および統合するための詳細な手順について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [従来の言語サービスでの構文の色分け表示](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)  
 言語サービスで構文の強調表示を実装する方法について説明します。  
  
 [従来の言語サービスでのステートメント入力補完](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)  
 ステートメント入力候補について説明します。このプロセスでは、言語サービスは、ユーザーが入力を開始した言語キーワードまたは要素を完了するのに役立ちます。  
  
 [従来の言語サービスのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)  
 オーバーロードされた関数およびメソッドに対してメソッドのヒントを提供する方法について説明します。  
  
 [方法: 従来の言語サービスでの隠し文字サポートの提供](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)  
 非表示テキスト領域の目的について説明し、非表示のテキスト領域を実装する方法について説明します。  
  
 [方法: 従来の言語サービスでのアウトラインの拡張サポートの提供](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)  
 [ *定義に折りたたむ* ] コマンドをサポートすること以外に、言語のアウトラインサポートを拡張する2つのオプションについて説明します。
