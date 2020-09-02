---
title: フォントと色を使用する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- fonts, controlling in IDE
- IDE, controlling text color and fonts
- Fonts and Colors property page
- font and color control [Visual Studio SDK]
- text, IDE
ms.assetid: d1a9b99f-fbdc-45ed-920a-e08c3d931ac9
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42ebc9414e3e5bb10f2468ed7f5f4fb4900e4ec6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68177229"
---
# <a name="using-fonts-and-colors"></a>フォントと色の使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

では、 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] フォントと色を使用したテキストの表示がサポートされています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [フォントと色の概要](../extensibility/font-and-color-overview.md)  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]統合開発環境 (IDE: integrated development environment) でのテキストのフォントと色の設定について説明します。 また、には、カテゴリと表示項目の概念が導入されており、Vspackage とコアエディターでテキスト属性がどのように使用されるかが説明されています。  
  
 [テキストに色づけするためのフォントと色の情報の取得](../extensibility/getting-font-and-color-information-for-text-colorization.md)  
 **テキストエディター**以外の**カテゴリ**を管理するテキストの色付けを vspackage に実装するためのガイドラインを示します。  
  
 [格納されたフォントと色の設定へのアクセス](../extensibility/accessing-stored-font-and-color-settings.md)  
 現在のフォントと色の設定を格納、取得、および適用する方法について説明します。  
  
 [カスタム カテゴリと表示項目の実装](../extensibility/implementing-custom-categories-and-display-items.md)  
 ウィンドウで、テキストの表示をサポートするために独自の **表示項目** および **カテゴリ** を作成して使用する基本的な手順について説明します。  
  
 この方法では、インターフェイスとそれに関連するインターフェイスを実装するには VSPackage が必要です <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> 。  
  
 [方法: 組み込みのフォントおよび色のスキーマにアクセスする](../extensibility/how-to-access-the-built-in-fonts-and-color-scheme.md)  
 組み込みのフォントと色を使用してカテゴリを定義および登録する方法と、システムによって提供されるフォントと色の使用を開始する方法について説明します。  
  
## <a name="reference"></a>リファレンス  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>  
 [ `IVsFontAndColorDefaults` <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> **オプション**] ダイアログボックスの [**フォントおよび色**] ページの [**設定の表示**] ボックスの一覧に表示されている特定の項目に対応するまたはインターフェイスのインスタンスを提供します。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>  
 ウィンドウまたは UI コンポーネントの既定のフォントと色を定義して、VSPackage が IDE の **フォントおよび色** ページをサポートできるようにします。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>  
 フォントおよび色のサポートを提供する VSPackage が、表示項目グループ (2 つ以上のカテゴリの和集合を表すスーパーカテゴリ) を指定できるようにするためのメカニズムを提供します。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>  
 VSPackage がフォントと色のデータを取得したり、レジストリに保存したりできるようにします。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>  
 フォントおよび色の設定の変更に関するフォントおよび色の情報を使用していることを Vspackage に通知します。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities>  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**フォントおよびカラー**機構のメソッドで使用される入力データと出力データを操作するためのツールを提供します。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager>  
 フォントおよび色の設定のキャッシュを制御します。  
  
## <a name="related-sections"></a>関連項目  
 [従来の言語サービスの開発](../extensibility/internals/developing-a-legacy-language-service.md)  
 Vspackage が言語サービスを使用してエディターをカスタマイズする方法について説明し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
 [カスタム エディターでの構文の色分け表示](../extensibility/syntax-coloring-in-custom-editors.md)  
 Descries は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] エディターが言語サービスを使用して構文の色分けを実装する方法を説明します。  
  
 [Visual Studio の他の部分の拡張](../extensibility/extending-other-parts-of-visual-studio.md)  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] サービスを使用して、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の他の部分に相当する UI 要素を作成する方法について説明します。
