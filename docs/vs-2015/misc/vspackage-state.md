---
title: VSPackage State |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- state, VSPackages
- VSPackages, managing application state
- state persistence
ms.assetid: 6056a9ea-e7a8-481c-9fc8-340229fa12d9
caps.latest.revision: 25
manager: jillfra
ms.openlocfilehash: f3140b527673f87b1d7c552e99584232494aed7f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62979996"
---
# <a name="vspackage-state"></a>Visual Studio の状態
アプリケーションの永続化された値のセット (状態) は、多くの要因によって決まり [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
- プロジェクトには、プロジェクトと構成のプロパティがあります。  
  
- ソリューションにはプロパティがあります。  
  
- ユーザー設定は、ドキュメントウィンドウ、ツールウィンドウ、ドッキング状態、およびキーボードショートカットのサイズと位置を決定します。  
  
- アプリケーションには、ユーザーが設定するオプションを含めることができます。  
  
- アプリケーションによって作成されるオブジェクトは、独自のプロパティを持つことができます。  
  
  アプリケーションの状態を管理できるいくつかの方法を次に示し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
- プロジェクトおよびソリューションのプロパティページを使用します。  
  
- 設定の **インポートとエクスポートウィザード**を使用して、ユーザーが設定をコンピューター間で移動できるようにします。  
  
- [ **オプション** ] ダイアログボックスを使用します。このダイアログボックスには、アプリケーションに関連するオプションが表示されます。  
  
- [ **プロパティ** ] ウィンドウを使用します。このウィンドウでは、オブジェクトのプロパティを公開します。  
  
- オートメーションを使用します。 アプリケーションは、オートメーションに公開されている VSPackage およびオブジェクトのプロパティにアクセスできます。  
  
  アプリケーションの状態の基になるのは、アプリケーションの状態を保存および復元できるようにするさまざまな永続化メカニズムです。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [状態の永続性のサポート](../misc/support-for-state-persistence.md)  
 VSPackage の状態を保存、復元、リセットするための一般的な戦略を一覧表示します。  
  
 [オプションとオプション ページ](../extensibility/internals/options-and-options-pages.md)  
 全般およびカスタムオプションページの概要と、それらを実装する方法について説明します。  
  
 [オプション ページの作成](../extensibility/creating-an-options-page.md)  
 2つのオプションページ (単純なページとカスタムページ) を作成する方法について説明します。  
  
 [設定カテゴリのサポート](../misc/support-for-settings-categories.md)  
 ユーザー設定とその作成方法と保存方法について説明します。  
  
 [設定カテゴリの作成](../extensibility/creating-a-settings-category.md)  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]設定カテゴリを作成し、それを使用して設定ファイルに値を保存し、値を復元する方法について説明します。  
  
 [プロパティとプロパティ ウィンドウの拡張](../extensibility/extending-properties-and-the-property-window.md)  
 [ **プロパティ** ] ウィンドウでオブジェクトの値を表示および変更する方法について説明します。  
  
 [プロパティ ウィンドウへのプロパティの公開](../extensibility/exposing-properties-to-the-properties-window.md)  
 オブジェクトのパブリックプロパティを [ **プロパティ** ] ウィンドウに公開する方法について説明します。  
  
 [プロジェクトおよび構成プロパティのサポート](../extensibility/internals/support-for-project-and-configuration-properties.md)  
 プロジェクトと構成のプロパティを表示および変更する方法について説明します。  
  
 [プロジェクト プロパティの取得](../extensibility/getting-project-properties.md)  
 ツールウィンドウにプロジェクトのプロパティを表示するマネージ VSPackage を作成する手順について説明します。  
  
 [設定ストアの使用](../extensibility/using-the-settings-store.md)  
 設定ストアの永続化メカニズムとその使用方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [VSPackages](../extensibility/internals/vspackages.md)  
 Vspackage を作成して使用する方法を説明するトピックへの一般的な向きを示します。