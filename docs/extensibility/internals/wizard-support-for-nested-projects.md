---
title: 入れ子になったプロジェクトに対するウィザードのサポート |Microsoft Docs
description: Visual Studio SDK の VSPackage の入れ子になったプロジェクトに対して、親プロジェクトが実装できる2つのウィザードについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add Item wizard
- nested projects, wizard support
- New Project wizard
ms.assetid: 1b496acc-b326-4cdb-bb48-e3b5c6f12e05
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7f52b42462fdc4b7878f97c01bdc65322f32eb5b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074146"
---
# <a name="wizard-support-for-nested-projects"></a>入れ子になったプロジェクト向けのウィザード サポート
IDE では、入れ子になったプロジェクトの親プロジェクトが実装できる2つのウィザードが実行されます。これは、 **新しいプロジェクト** ウィザードと **項目の追加** ウィザードです。

 [**プロジェクトの追加**] を選択し、[ファイル] メニューの **[新しいプロジェクト] をクリックする** か、[**追加**] を選択し、[ソリューションエクスプローラーで [新しいプロジェクト] を **右クリックし** て、**プロジェクトの新規** 作成ウィザードを開始した場合、IDE は **Addproject** コマンドを実行し、親プロジェクトの **addproject** の実装は、コンテキストパラメーターのセットを含むテンプレートプロジェクト

 同様に、親プロジェクトの **AddItem** ウィザードの実装では、異なるコンテキストパラメーターのセットを持つ .vsz ファイルが返されます。

 ウィザードの詳細については、「ウィザード (」を参照してください [。.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)、 [コンテキストパラメーター](../../extensibility/internals/context-parameters.md) 、および [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)を行います。

## <a name="see-also"></a>こちらもご覧ください
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [入れ子になったプロジェクト](../../extensibility/internals/nesting-projects.md)
