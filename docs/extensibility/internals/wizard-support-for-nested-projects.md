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
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8b3c6dee712f79648eba203650cc70f76fcea657
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/17/2020
ms.locfileid: "97615617"
---
# <a name="wizard-support-for-nested-projects"></a>入れ子になったプロジェクト向けのウィザード サポート
IDE では、入れ子になったプロジェクトの親プロジェクトが実装できる2つのウィザードが実行されます。これは、 **新しいプロジェクト** ウィザードと **項目の追加** ウィザードです。

 [**プロジェクトの追加**] を選択し、[ファイル] メニューの **[新しいプロジェクト] をクリックする** か、[**追加**] を選択し、[ソリューションエクスプローラーで [新しいプロジェクト] を **右クリックし** て、**プロジェクトの新規** 作成ウィザードを開始した場合、IDE は **Addproject** コマンドを実行し、親プロジェクトの **addproject** の実装は、コンテキストパラメーターのセットを含むテンプレートプロジェクト

 同様に、親プロジェクトの **AddItem** ウィザードの実装では、異なるコンテキストパラメーターのセットを持つ .vsz ファイルが返されます。

 ウィザードの詳細については、「ウィザード (」を参照してください [。.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)、 [コンテキストパラメーター](../../extensibility/internals/context-parameters.md) 、および [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)を行います。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [入れ子になったプロジェクト](../../extensibility/internals/nesting-projects.md)
