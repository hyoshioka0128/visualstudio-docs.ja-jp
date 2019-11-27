---
title: SDK のモデリング-ドメイン固有言語 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools
- Domain-Specific Language
ms.assetid: 17a531e2-1964-4a9d-84fd-6fb1b4aee662
caps.latest.revision: 79
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 505c17635c80a165a7a094d3ce2bec3c32bd7101
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297687"
---
# <a name="modeling-sdk-for-visual-studio---domain-specific-languages"></a>Modeling SDK for Visual Studio - ドメイン固有言語
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

モデリング SDK for [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (MSDK) を使用すると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]に統合できる強力なモデルベースの開発ツールを作成できます。 たとえば、UML ツールは MSDK を使用して作成されます。 同様に、1 つ以上のモデル定義を作成して、一連のツールと統合できます。

 MSDK の中核は、業務分野の概念を表すために作成するモデルの定義です。 図式ビュー、コードおよびその他の成果物の生成機能、モデルを変換するためのコマンド、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のコードやその他のオブジェクトとの対話機能などのさまざまなツールでモデルを囲むことができます。 モデルを開発するとき、他のモデルやツールと組み合わせて、開発の中央に配置される強力なツール セットを形成することができます。

 MSDK では、ドメイン固有言語 (DSL) の形式でモデルを迅速に開発できます。 グラフィカルな表記と共にスキーマまたは抽象構文を定義する専用のエディターを使用することから始めます。 この定義から、VMSDK は次を生成します。

- トランザクション ベースのストアで実行する厳密に型指定された API によるモデル実装。

- ツリー ベースのエクスプローラー。

- 定義するモデルまたは一部をユーザーが表示できるグラフィカル エディター。

- 読み取り可能な XML にモデルを保存するシリアル化メソッド。

- テキスト テンプレートを使用して、プログラム コードとその他の成果物を生成するための機能。

  これらのすべての機能をカスタマイズおよび拡張できます。 拡張した機能は、統合後も DSL 定義を更新でき、拡張した機能を失うことなく機能を再生成できるように統合されています。

## <a name="samples-and-the-latest-information"></a>サンプルおよび最新情報
 [モデリング SDK for Visual Studio 2015 のダウンロード](https://www.microsoft.com/download/details.aspx?id=48148)

 モデリング SDK for Visual Studio の[サンプル](https://go.microsoft.com/fwlink/?LinkId=186128)です。

 高度な手法とトラブルシューティングのガイダンスについては、「 [Visual STUDIO DSL & モデリングツールの機能拡張フォーラム](https://go.microsoft.com/fwlink/?LinkID=186074)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [ドメイン固有言語の概要](../modeling/getting-started-with-domain-specific-languages.md)

 [モデル、クラス、およびリレーションシップについて](../modeling/understanding-models-classes-and-relationships.md)

 [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)

 [ドメイン固有言語のカスタマイズおよび拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)

 [ドメイン固有言語における検証](../modeling/validation-in-a-domain-specific-language.md)

 [ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)

 [ドメイン固有言語からのコード生成](../modeling/generating-code-from-a-domain-specific-language.md)

 [DSL コードについて](../modeling/understanding-the-dsl-code.md)

 [ファイル格納処理および XML シリアル化処理のカスタマイズ](../modeling/customizing-file-storage-and-xml-serialization.md)

 [ドメイン固有言語ソリューションの配置](../modeling/deploying-domain-specific-language-solutions.md)

 [Windows フォームに基づくドメイン固有言語の作成](../modeling/creating-a-windows-forms-based-domain-specific-language.md)

 [WPF に基づくドメイン固有言語の作成](../modeling/creating-a-wpf-based-domain-specific-language.md)

 [方法: ドメイン固有言語デザイナーを拡張する](../modeling/how-to-extend-the-domain-specific-language-designer.md)

 [Visualization and Modeling SDK に対してサポートされている Visual Studio のエディション](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)

 [方法: ドメイン固有言語を新バージョンに移行する](../modeling/how-to-migrate-a-domain-specific-language-to-a-new-version.md)

 [Modeling SDK for Visual Studio の API リファレンス](../modeling/api-reference-for-modeling-sdk-for-visual-studio.md)
