---
title: ネストされたプロジェクトのウィザードサポート |マイクロソフトドキュメント
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
ms.openlocfilehash: f7f37700d908167ebef8c071021558822bdce173
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703195"
---
# <a name="wizard-support-for-nested-projects"></a>入れ子になったプロジェクト向けのウィザード サポート
IDE では、入れ子になったプロジェクトの親プロジェクトが実装できる 2 つのウィザード (**新規プロジェクト**ウィザードと**項目の追加**ウィザード) が実行されます。

 ユーザーが [**プロジェクト**の追加] をクリックして [新しい**プロジェクト**] をクリックするか、[ファイル] メニューの [**新しいプロジェクト**] をクリックするか、または [**追加**] を選択して右クリックした場合、IDE は AddProject コマンドを実行し、親プロジェクトの**New Project****AddProject**コマンドの実装は、テンプレート プロジェクト ファイルまたはコンテキスト パラメータのセットを含むウィザード (.vsz) ファイルを返します。 **AddProject**

 同様に、親プロジェクトの**AddItem**ウィザードの実装では、コンテキスト パラメーターの異なるセットを持つ .vsz ファイルが返されます。

 ウィザードの詳細については、「[ウィザード」を参照してください。Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)、[コンテキスト パラメータ](../../extensibility/internals/context-parameters.md)、および[プロジェクトテンプレートと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [入れ子になったプロジェクト](../../extensibility/internals/nesting-projects.md)
