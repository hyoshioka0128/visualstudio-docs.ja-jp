---
title: プロパティ ウィンドウボタン |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aaa4db159ccb0ecf3d0e9c9243e23fcd0dacc455
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706174"
---
# <a name="properties-window-buttons"></a>プロパティ ウィンドウのボタン
開発言語と製品タイプに応じて、既定では **[プロパティ]** ウィンドウのツールバーに特定のボタンが表示されます。 いずれの場合も、[**分類済み**]、[**アルファベット順**]、[プロパティ]、および **[プロパティ****ページ]** の各ボタンが表示されます。 Visual C# および Visual Basic では、[**イベント**] ボタンも表示されます。 特定の Visual C++ プロジェクトでは **、VC++ メッセージ**と**VC オーバーライド**ボタンが表示されます。 他の種類のプロジェクトに対して、追加のボタンが表示される場合があります。 **[プロパティ]** ウィンドウのボタンの詳細については、「[プロパティ ウィンドウ](../../ide/reference/properties-window.md)」を参照してください。

## <a name="implementation-of-properties-window-buttons"></a>[プロパティ] ウィンドウ ボタンの実装
 **[分類済み**] ボタンをクリックすると、Visual <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> Studio は、カテゴリ別にプロパティを並べ替えるためにフォーカスを持つオブジェクトのインターフェイスを呼び出します。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>は、プロパティ ウィンドウ`IDispatch`に表示されるオブジェクトに実装**Properties**されます。

 11 の定義済みのプロパティ カテゴリがあり、負の値を持ちます。 カスタム カテゴリを定義できますが、定義済みのカテゴリと区別するために正の値を割り当てることをお勧めします。

 この<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A>メソッドは、指定されたプロパティに対して適切なプロパティ カテゴリ値を返します。 この<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A>メソッドは、カテゴリ名を含む文字列を返します。 Visual Studio は標準のプロパティ カテゴリ値を認識しているため、カスタム カテゴリ値のサポートを提供する必要があります。

 **[アルファベット順**] ボタンをクリックすると、プロパティが名前のアルファベット順に表示されます。 名前は、ローカライズされた並`IDispatch`べ替えアルゴリズムに従って取得されます。

 **[プロパティ]** ウィンドウが開いている場合は、[**プロパティ]** ボタンが選択された状態で自動的に表示されます。 環境の他の部分では、同じボタンが表示され、**クリックすると[プロパティ]** ウィンドウを表示できます。

 選択したオブジェクトに対して`ISpecifyPropertyPages`[**プロパティ ページ]** ボタンが実装されていない場合は、[プロパティ ページ] ボタンは使用できません。 プロパティ ページには、通常はソリューションやプロジェクトに関連付けられている構成依存のプロパティが表示されますが、Visual C++ など、プロジェクト項目に関連付けることもできます。

> [!NOTE]
> アンマネージ コードを使用して[**プロパティ]** ウィンドウにツール バー ボタンを追加することはできません。 ツール バー ボタンを追加するには、 から<xref:System.Windows.Forms.Design.PropertyTab>派生するマネージ オブジェクトを作成する必要があります。

## <a name="see-also"></a>関連項目
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
