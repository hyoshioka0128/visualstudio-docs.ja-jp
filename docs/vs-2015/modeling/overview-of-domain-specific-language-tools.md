---
title: ドメイン固有言語ツールの概要 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: overview
helpviewer_keywords:
- Domain-Specific Language
ms.assetid: 50d93ea2-8c88-4522-853b-40ab194953db
caps.latest.revision: 56
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d38aed17d7fdaa694c8c5753705b28b0390dedfc
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "72652147"
---
# <a name="overview-of-domain-specific-language-tools"></a>ドメイン固有言語ツールの概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でホストされるドメイン固有言語ツール (DSL ツール) を使用すると、ドメイン固有言語を設計し、その言語に基づくモデルを作成するためにユーザーに必要なすべてのものを生成できます。

 DSL ツールには次のツールが含まれています。

- さまざまなソリューション テンプレートを使用してドメイン固有言語の開発を始めるのに役立つ、プロジェクト ウィザード。

- ドメイン固有言語の定義を作成、編集するためのグラフィカル デザイナー。

- ドメイン固有言語の定義が適切な形式であることを確認し、問題がある場合はエラーや警告を表示する検証エンジン。

- ドメイン固有言語の定義を入力として受け取り、ソース コードを出力として生成するコード ジェネレーター。

## <a name="the-dsl-tools-solution"></a>DSL ツール ソリューション
 ドメイン固有デザイナー ウィザードには、次のソリューション テンプレートが用意されています。

- タスク フロー

- クラス ダイアグラム

- 最小言語

- コンポーネント モデル

- 最小限の WPF

- 最小 Windows.Forms

- DSL ライブラリ

  詳細については、「[ドメイン固有言語ソリューション テンプレートの選択](../modeling/choosing-a-domain-specific-language-solution-template.md)」を参照してください。

  ウィザードにより、次のプロジェクトを含む [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションが作成されます。

- Dsl

   Dsl プロジェクトでは、ドメイン固有言語と、その言語の編集および処理ツールを定義します。

- **DslPackage**

   DslPackage プロジェクトでは、言語ツールを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] と統合する方法を決定します。

## <a name="the-dsl-tools-graphical-interface"></a>DSL ツールのグラフィカル インターフェイス
 DSL ツールのグラフィカル インターフェイスを使用して、ドメイン固有言語に要素とリレーションシップを追加することができます。 要素を追加後、要素をシェイプにマッピングし、色をカスタマイズして、デコレーターを追加することによって、要素の外観を定義できます。 要素をツールボックスに追加することもできます。

## <a name="validation-in-dsl-tools"></a>DSL ツールでの検証
 DSL には、ドメイン モデルがコード生成のための基本的な要件を満たしていることを確認する、1 つの検証レベルが用意されています。 通常、ご自分のドメイン固有言語を作成するときは、ご自分のビジネス ロジック ルールを表す独自の検証を追加します。 カスタム検証の詳細については、「[ドメイン固有言語における検証](../modeling/validation-in-a-domain-specific-language.md)」を参照してください。

 ドメイン固有言語を設計する際は、頻繁に検証することをお勧めします。 ドメイン固有言語に検証エラーがあると、ソース コードを生成できません。 テンプレートからソース コードを生成するプロセスは、ソリューション エクスプローラーのツール バーで **[すべてのテンプレートの変換]** をクリックすることによって実行します。 言語の定義を変更したときは、必ず**すべてのテンプレートの変換**も実行してください。 詳細については、[ドメイン固有言語ソリューションを作成する](../modeling/how-to-create-a-domain-specific-language-solution.md)」を参照してください。

## <a name="customization-of-dsl-tools"></a>DSL ツールのカスタマイズ
 モデルの動作を改善するために、また使用する言語に制約を定義するために、追加のコードを記述できます。 必要な場合は、テキスト テンプレートを変更することによって、大幅な変更を行うことができます。

## <a name="distributing-your-dsl-solution"></a>DSL ソリューションの配布
 DSL ツールによって、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でホストされるパッケージが生成されます。 パッケージにはツールボックス、DSL エクスプローラー、およびその他の UI 要素が表示され、ユーザーは、ドメイン固有言語を使用してモデルを作成できます。

 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で DSL ツール ソリューションをビルドして実行すると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の 2 番目のインスタンスに、ドメイン固有言語のユーザーに対して言語がどのように表示されるかが示されます。 すべてが正常に動作することを確認した後、DslPackage プロジェクトのビルド フォルダーにある `.vsix` ファイルを配布できます。 このファイルは、他のコンピューター上に [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能として DSL をインストールするために使用できます。  詳細については、「[ドメイン固有言語ソリューションの配置](../modeling/deploying-domain-specific-language-solutions.md)」を参照してください。

## <a name="see-also"></a>関連項目
 [実験用インスタンス](../extensibility/the-experimental-instance.md) [ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
