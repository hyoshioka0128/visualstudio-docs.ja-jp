---
title: プロジェクトの入れ子 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0e3a0fae42dc7bf1497e3d0d4a9d23f9cab50675
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "68180420"
---
# <a name="nesting-projects"></a>入れ子になったプロジェクト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VS パッケージを使用するエンタープライズアプリケーション開発者は、*プロジェクトの入れ子*を使用して、類似した種類のプロジェクトを [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] で簡単にグループ化できます。 たとえば、エンタープライズテンプレートプロジェクトでは、入れ子になったプロジェクトを使用して、プロジェクトをカテゴリにグループ化します。 ビジネスファサードプロジェクト、Web UI プロジェクトなどは、1つのカテゴリにまとめられています。  
  
 このシナリオでは、開発者はプログラムを使用して制限を提供できますが、開発者が各親プロジェクトの下で入れ子にできるプロジェクトの数に制限はありません。 この種類のグループ化を再帰的に行うこともできます。この場合、子プロジェクトと同じ種類のプロジェクトを子の下に入れ子にして、親のサブプロジェクトである子のサブプロジェクトにすることができます。  
  
 プロジェクトの入れ子は、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]の組み込みの部分ではありません。 子プロジェクト内で入れ子およびサブプロジェクトの入れ子を有効にするには、コードを記述する必要があります。 親プロジェクトは、プロジェクトの入れ子を実装するために必要なコードを含む独自の GUID を使用して作成および登録された、特殊な VSPackage またはプロジェクトの種類です。  
  
 入れ子になったプロジェクトの例についてC#は、「入れ子になったプロジェクトのサンプル」を参照してください。  
  
## <a name="nested-projects-example"></a>入れ子になったプロジェクトの例  
 ![入れ子になったプロジェクトソリューション](../../extensibility/internals/media/vsnestedprojects.gif "vsnestedprojects")  
入れ子になったプロジェクトの例  
  
## <a name="see-also"></a>関連項目  
 [方法: 入れ子になったプロジェクトを実装する](../../extensibility/internals/how-to-implement-nested-projects.md)   
 [入れ子になったプロジェクトのアンロードと再読み込みに関する考慮事項](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)   
 [入れ子になったプロジェクトのウィザードサポート](../../extensibility/internals/wizard-support-for-nested-projects.md)   
 [プロジェクトテンプレートと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)   
 [入れ子になったプロジェクトのコマンド処理の実装](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)   
 [入れ子になったプロジェクトの [AddItem] ダイアログボックスのフィルター処理](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)   
 [チェックリスト: 新しいプロジェクトの種類の作成](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [コンテキストパラメーター](../../extensibility/internals/context-parameters.md)   
 [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
