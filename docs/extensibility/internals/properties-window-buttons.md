---
title: プロパティウィンドウのボタン |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f2a41917a58a6fc5780b62c2c9e3db8aa52d407
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725270"
---
# <a name="properties-window-buttons"></a>プロパティ ウィンドウのボタン
開発言語と製品の種類によっては、 **[プロパティ]** ウィンドウのツールバーに、既定で特定のボタンが表示されます。 どのような場合でも、 **[分類]** 済み、 **[アルファベット]** 、 **[プロパティ]** 、 **[プロパティページ]** の各ボタンが表示されます。 ビジュアルC#と Visual Basic では、 **[イベント]** ボタンも表示されます。 特定のビジュアルC++プロジェクトでは、 **[Vc + + メッセージ]** ボタンと **[vc 上書き]** ボタンが表示されます。 他のプロジェクトの種類では、追加のボタンが表示される場合があります。 **[プロパティ]** ウィンドウのボタンの詳細については、「[プロパティウィンドウ](../../ide/reference/properties-window.md)」を参照してください。

## <a name="implementation-of-properties-window-buttons"></a>プロパティウィンドウボタンの実装
 [項目**別**] ボタンをクリックすると、Visual Studio は、プロパティをカテゴリ別に並べ替えるためにフォーカスがあるオブジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> インターフェイスを呼び出します。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> は、 **[プロパティ]** ウィンドウに表示される `IDispatch` オブジェクトに実装されます。

 11個の定義済みプロパティカテゴリがあり、これらには負の値が含まれています。 カスタムカテゴリを定義することもできますが、定義済みのカテゴリと区別するために、正の値を割り当てることをお勧めします。

 @No__t_0 メソッドは、指定されたプロパティの適切なプロパティカテゴリの値を返します。 @No__t_0 メソッドは、カテゴリ名を含む文字列を返します。 Visual Studio では、標準のプロパティカテゴリの値が認識されるため、カスタムカテゴリ値のサポートのみを提供する必要があります。

 [**アルファベット**順] ボタンをクリックすると、プロパティは名前順にアルファベット順に表示されます。 名前は、ローカライズされた並べ替えアルゴリズムに従って `IDispatch` によって取得されます。

 **[プロパティ]** ウィンドウが開いている場合は、 **[プロパティ]** ボタンが自動的に選択された状態で表示されます。 環境の他の部分では、同じボタンが表示され、クリックして **[プロパティ]** ウィンドウを表示できます。

 選択したオブジェクトに `ISpecifyPropertyPages` が実装されていない場合、 **[プロパティページ]** ボタンは使用できません。 プロパティページには、通常、ソリューションやプロジェクトに関連付けられている構成に依存するプロパティが表示されますが、プロジェクトアイテム ( C++ビジュアルなど) に関連付けることもできます。

> [!NOTE]
> アンマネージコードを使用して、 **[プロパティ]** ウィンドウにツールバーボタンを追加することはできません。 ツールバーボタンを追加するには、<xref:System.Windows.Forms.Design.PropertyTab> から派生するマネージオブジェクトを作成する必要があります。

## <a name="see-also"></a>関連項目
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)