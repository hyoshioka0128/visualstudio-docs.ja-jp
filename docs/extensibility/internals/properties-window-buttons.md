---
title: プロパティウィンドウのボタン |Microsoft Docs
description: プロパティウィンドウのツールバーに既定で表示されるボタンと、ボタンの実装について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 601e40762adc665f6241bb00a4b683b81e7fbd80
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99970024"
---
# <a name="properties-window-buttons"></a>プロパティ ウィンドウのボタン
開発言語と製品の種類によっては、[ **プロパティ** ] ウィンドウのツールバーに、既定で特定のボタンが表示されます。 どのような場合でも、[ **分類** 済み]、[ **アルファベット**]、[ **プロパティ**]、[ **プロパティページ** ] の各ボタンが表示されます。 Visual C# と Visual Basic では、[ **イベント** ] ボタンも表示されます。 特定の Visual C++ プロジェクトでは、[ **vc + + メッセージ** ] ボタンと [ **vc 上書き** ] ボタンが表示されます。 他のプロジェクトの種類では、追加のボタンが表示される場合があります。 [ **プロパティ** ] ウィンドウのボタンの詳細については、「 [プロパティウィンドウ](../../ide/reference/properties-window.md)」を参照してください。

## <a name="implementation-of-properties-window-buttons"></a>プロパティウィンドウボタンの実装
 [項目 **別** ] ボタンをクリックすると、Visual Studio は、 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> プロパティをカテゴリ別に並べ替えるためにフォーカスがあるオブジェクトのインターフェイスを呼び出します。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> は `IDispatch` 、[ **プロパティ** ] ウィンドウに表示されるオブジェクトに実装されます。

 11個の定義済みプロパティカテゴリがあり、これらには負の値が含まれています。 カスタムカテゴリを定義することもできますが、定義済みのカテゴリと区別するために、正の値を割り当てることをお勧めします。

 メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A> 指定されたプロパティの適切なプロパティカテゴリの値を返します。 メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A> カテゴリ名を含む文字列を返します。 Visual Studio では、標準のプロパティカテゴリの値が認識されるため、カスタムカテゴリ値のサポートのみを提供する必要があります。

 [ **アルファベット** 順] ボタンをクリックすると、プロパティは名前順にアルファベット順に表示されます。 名前は、ローカライズされた並べ替えアルゴリズムに従ってによって取得され `IDispatch` ます。

 [ **プロパティ** ] ウィンドウが開いている場合は、[ **プロパティ** ] ボタンが自動的に選択された状態で表示されます。 環境の他の部分では、同じボタンが表示され、クリックして [ **プロパティ** ] ウィンドウを表示できます。

 選択したオブジェクトにが実装されていない場合、[ **プロパティページ** ] ボタンは使用できません `ISpecifyPropertyPages` 。 プロパティページには、通常はソリューションとプロジェクトに関連付けられている構成に依存するプロパティが表示されますが、プロジェクト項目に関連付けることもできます (たとえば、Visual C++)。

> [!NOTE]
> アンマネージコードを使用して、[ **プロパティ** ] ウィンドウにツールバーボタンを追加することはできません。 ツールバーボタンを追加するには、から派生するマネージオブジェクトを作成する必要があり <xref:System.Windows.Forms.Design.PropertyTab> ます。

## <a name="see-also"></a>関連項目
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
