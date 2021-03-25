---
title: プロジェクトの入れ子 |Microsoft Docs
description: プロジェクトの入れ子について説明します。これにより、VSPackage を使用するアプリケーション開発者は、類似した種類のプロジェクトを Visual Studio でまとめてグループ化できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 30b562cac794b7ab960f055fe67a5d0cc4ec871f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063222"
---
# <a name="nesting-projects"></a>入れ子になったプロジェクト
VS パッケージを使用するエンタープライズアプリケーション開発者は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] *プロジェクトの入れ子* を使用して、類似した種類のプロジェクトをで簡単にグループ化できます。 たとえば、エンタープライズテンプレートプロジェクトでは、入れ子になったプロジェクトを使用して、プロジェクトをカテゴリにグループ化します。 ビジネスファサードプロジェクト、Web UI プロジェクトなどは、1つのカテゴリにまとめられています。

 このシナリオでは、開発者はプログラムを使用して制限を提供できますが、開発者が各親プロジェクトの下で入れ子にできるプロジェクトの数に制限はありません。 この種類のグループ化を再帰的に行うこともできます。この場合、子プロジェクトと同じ種類のプロジェクトを子の下に入れ子にして、親のサブプロジェクトである子のサブプロジェクトにすることができます。

 プロジェクトの入れ子は、の組み込みの部分ではありません [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 子プロジェクト内で入れ子およびサブプロジェクトの入れ子を有効にするには、コードを記述する必要があります。 親プロジェクトは、プロジェクトの入れ子を実装するために必要なコードを含む独自の GUID を使用して作成および登録された、特殊な VSPackage またはプロジェクトの種類です。

 プロジェクトを入れ子にする方法の例については、 [「方法: 入れ子になったプロジェクトを実装](../../extensibility/internals/how-to-implement-nested-projects.md)する」を参照してください。

## <a name="nested-projects-example"></a>入れ子になったプロジェクトの例
 ![入れ子になったプロジェクトソリューション](../../extensibility/internals/media/vsnestedprojects.gif "vsNestedProjects") 入れ子になったプロジェクトの例

## <a name="see-also"></a>こちらもご覧ください
- [入れ子になったプロジェクトのアンロードと再ロードに関する考慮事項](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [入れ子になったプロジェクト向けのウィザード サポート](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [入れ子になったプロジェクト向けのコマンド処理の実装](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [入れ子になったプロジェクトのための [AddItem] ダイアログ ボックスのフィルター処理](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [コンテキストパラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
