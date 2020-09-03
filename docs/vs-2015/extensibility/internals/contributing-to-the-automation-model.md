---
title: オートメーションモデルへの貢献 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c84ea078f9b7c1268b765111cc400f6e51b783f1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197000"
---
# <a name="contributing-to-the-automation-model"></a>オートメーション モデルへの投稿
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio には、環境をカスタマイズするための一連のオートメーションインターフェイスが用意されています。 オートメーションモデルは、エンドユーザーが Visual Studio のアドインと拡張機能を作成できるようにするオブジェクトモデルです。  
  
 また、VSPackage の開発者がオートメーションモデルに貢献するのに適しています。これにより、VSPackage のエンドユーザーがアドインを作成できるようになります。また、で VSPackage を使用する場合は、通常、一貫したユーザーモデルエクスペリエンスが提供さ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] れます。  
  
 エンドユーザーエクスペリエンスの一貫性を確保するために、VSPackage の設計時に一連のガイドラインに従って、VSPackage のオートメーションモデルがのアイデアに従うようにすることができ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [オートメーション モデルの概要](../../extensibility/internals/automation-model-overview.md)  
 共通環境の主要なファセットを制御するオブジェクトの関連グループとしてオートメーションモデルを定義します。 この一連のオブジェクトは、オートメーションモデルの図に示されています。  
  
 [VSPackage でのオートメーションの提供](../../extensibility/internals/providing-automation-for-vspackages.md)  
 VSPackage の自動化を実現する2つの主な方法について説明します。  
  
 [プロジェクト オブジェクトの公開](../../extensibility/internals/exposing-project-objects.md)  
 VSPackage 固有のオブジェクトを作成する手順について説明します。  
  
 [プロジェクトのモデリング](../../extensibility/internals/project-modeling.md)  
 新しいプロジェクトの種類のオートメーションを作成するために必要な標準プロジェクトオブジェクトについて説明し、プロジェクトオートメーションが従うパスを示します。 このトピックでは、クラスの宣言と実装の一覧も示します。  
  
 [イベントの公開](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)  
 オートメーションモデルのイベントを作成する手順について説明します。  
  
 [オプション ページのオートメーションのサポート](../../extensibility/internals/automation-support-for-options-pages.md)  
 オブジェクトを拡張することによって、**ツール**メニューの VSPackage の [カスタム**オプション**] ダイアログボックスのサポートプロパティのオートメーションオブジェクトを返す方法について説明し `DTE.Properties` ます。  
  
 [コードのオートメーションの提供](../../extensibility/internals/providing-automation-for-code.md)  
 コードのオートメーションモデルを作成する必要がないことについて説明します。 ただし、このトピックでは、コードモデルに関する洞察が得られる情報を提供するリンクが提供されています。  
  
 [方法: Windows 向けのオートメーションの提供](../../extensibility/internals/how-to-provide-automation-for-windows.md)  
 オートメーションオブジェクトをウィンドウで使用できるようにし、環境が既製のオートメーションオブジェクトを提供していない場合は常に、オートメーションを提供することをお勧めします。 ツールウィンドウとドキュメントウィンドウの自動化について説明します。  
  
 [オートメーション モデルの使用](../../extensibility/internals/using-the-automation-model.md)  
 オートメーションコンシューマーが初期のプロジェクトオートメーションオブジェクトを取得する方法を示す2つのコード例を示します。  
  
 [構成および SelectedItem オブジェクトのためのオートメーション](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)  
 選択した項目の構成オプションと自動化の自動化に関する情報を提供します。  
  
## <a name="reference"></a>リファレンス  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>  
 VSPackage が DTE オートメーションオブジェクトモデルにどのように参加するかを示すコードサンプルを提供します。 パラメーター、戻り値、および選択された解説を一覧表示します。  
  
## <a name="related-sections"></a>関連項目
