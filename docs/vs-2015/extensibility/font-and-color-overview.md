---
title: フォントと色の概要 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], font and color
- font and color control [Visual Studio SDK], editors
ms.assetid: 2203e4e7-8b7f-44ec-8884-6ff718d4f278
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0a20cfa2372b1e55652ffcebe6d173cff86140a6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204349"
---
# <a name="font-and-color-overview"></a>フォントと色の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 統合開発環境 (IDE) でのテキストのフォントと色の設定について説明します。 また、カテゴリと表示項目の概念についても説明します。また、Vspackage とコアエディターがテキスト属性を使用する方法についても説明します。  
  
## <a name="the-fonts-and-colors-property-page"></a>[フォントおよび色] プロパティページ  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)][**フォントおよび色**] プロパティページを使用して、統合開発環境 (IDE) で表示されるテキストの属性を管理できます。 [ **フォントおよび色** ] プロパティページを検索するには、[ **ツール** ] メニューの [ **オプション**] をクリックします。 **[環境]** を展開し、 **[フォントおよび色]** をクリックします。  
  
## <a name="categories-and-display-items"></a>カテゴリと表示項目  
 フォントおよび色は、 **カテゴリ** と **表示項目**に分類されます。  
  
- **カテゴリ**は、さまざまな**表示項目**の論理または機能のコンテナーです。  
  
   **カテゴリ**の一覧は、[**フォントおよび色**] プロパティページの [**設定の表示**] ドロップダウンボックスに表示されます。  
  
- **表示項目**は、コメント、文字列、または表示時に色分けされるコントロール構造など、適切に定義されたテキストエンティティです。  
  
  各 **表示項目** は、それを含む **カテゴリ** 内で一意に定義されます。 その結果、複数の **カテゴリ** に同じ名前の **表示項目** を含めることができます。  
  
## <a name="vspackage-control-of-fonts-and-colors"></a>フォントと色の VSPackage コントロール  
 では、Vspackage が許可され [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] ます。  
  
- フォントと色の **カテゴリ**を定義します。  
  
- **表示項目の表示**に使用するフォントと色を指定します。  
  
- [ **フォントおよび色** ] プロパティページを操作します。  
  
- 複数の **カテゴリ** をグループにまとめる。  
  
- 既定の設定の変更を保持します。  
  
  内でフォントと色の選択を操作するには、2つの方法があり [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] ます。  
  
- 1つの方法は、 *構文の色分け*と呼ばれます。 これは、既存のエディターをカスタマイズして [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 言語サービスを実装し、ソースエディターを作成する VSPackage によって使用されます。  
  
   このメカニズムをサポートしている **カテゴリ** は1つだけです。つまり、 **テキストエディター**です。  
  
- より一般的な方法では、テキストを表示するときに、ソースエディター以外の他のすべての **カテゴリ** とユーザーインターフェイスコンポーネントがサポートされます。 詳細については、「<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>」を参照してください。  
  
## <a name="core-editor-text-settings"></a>コアエディターのテキスト設定  
 言語サービスオブジェクトのコアエディターのフォントと色の設定は、[**フォントおよび色**] プロパティページの [**設定の表示**] ボックスの一覧にある**テキスト editorcategory**によって管理されます。  
  
 エディターを使用する場合、 **テキストエディター** の設定を制御および拡張するために言語サービスで提供されている特殊なフォントおよび色の制御メカニズムを使用する必要があります。 このメカニズムを *構文の色分け* と呼び、次の機能を提供します。  
  
- 表示項目のフォントと色を管理するための簡略化された手法。  
  
   詳細については、次のトピックを参照してください。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> および <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>  
  
- 明確に定義され、最適化された色付け機構。  
  
   詳細については、「<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>」を参照してください。  
  
- **Text EditorCategory**の組み込みの表示項目を使用して、それらを拡張する機能です。  
  
   詳細については、「 [方法: 組み込みの装飾項目](../extensibility/internals/how-to-use-built-in-colorable-items.md) および [カスタム装飾項目](../extensibility/internals/custom-colorable-items.md)を使用する」を参照してください。  
  
- [ **テキストエディター** ] カテゴリでの組み込み表示項目とカスタム表示項目の両方の現在の状態の自動永続化。  
  
  構文の色分けの詳細について [は、「従来の言語サービスの構文の色分け](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)表示」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エディター内のレガシインターフェイス](../extensibility/legacy-interfaces-in-the-editor.md)   
 [従来の言語サービスでの構文の色分け表示](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
