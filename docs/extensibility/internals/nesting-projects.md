---
title: プロジェクトのネスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 814780fa8e7e57a022a75b2e09115cfa55a1b8be
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707027"
---
# <a name="nesting-projects"></a>入れ子になったプロジェクト
VS Package を使用するエンタープライズ アプリケーション開発者は、 でプロジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]*の入れ子*を使用して、類似した種類のプロジェクトをまとめて簡単にグループ化できます。 たとえば、エンタープライズ テンプレート プロジェクトでは、入れ子になったプロジェクトを使用してプロジェクトをカテゴリにグループ化します。 ビジネス ファサード プロジェクト、Web UI プロジェクトなどは、1 つのカテゴリにグループ化されます。

 このシナリオでは、開発者がプログラムで制限を提供できますが、各親プロジェクトの下に入れ子にできるプロジェクトの数に制限はありません。 このタイプのグループ化は再帰的に行うこともできますが、子プロジェクトと同じタイプのプロジェクトを子プロジェクトの下にネストして、親のサブプロジェクトである子プロジェクトのサブプロジェクトにできます。

 プロジェクトの入れ子は. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 子プロジェクト内で入れ子とサブプロジェクトの入れ子を有効にするコードを記述する必要があります。 親プロジェクトは特別な VSPackage、つまりプロジェクトの種類で、プロジェクトの入れ子を実装するために必要なコードを含む独自の GUID で作成および登録されます。

 プロジェクトを入れ子にする方法の例は、「[方法 : 入れ子になったプロジェクトを実装する](../../extensibility/internals/how-to-implement-nested-projects.md)」を参照してください。

## <a name="nested-projects-example"></a>ネストされたプロジェクトの例
 ![入れ子になったプロジェクト ソリューション](../../extensibility/internals/media/vsnestedprojects.gif "プロジェクトのネスト")ネストされたプロジェクトの例

## <a name="see-also"></a>関連項目
- [入れ子になったプロジェクトのアンロードと再ロードに関する考慮事項](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [入れ子になったプロジェクト向けのウィザード サポート](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [入れ子になったプロジェクト向けのコマンド処理の実装](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [入れ子になったプロジェクトのための [AddItem] ダイアログ ボックスのフィルター処理](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)
- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
