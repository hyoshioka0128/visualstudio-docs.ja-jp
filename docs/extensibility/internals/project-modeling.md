---
title: プロジェクトモデリング |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], implementing project objects
- project models, automation
ms.assetid: c8db8fdb-88c1-4b12-86fe-f3c30a18f9ee
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c1ac89baf5bc7582d3430532938a5e5a0c35a4c0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706554"
---
# <a name="project-modeling"></a>プロジェクトのモデリング
プロジェクトのオートメーションを提供する次の手順は、標準プロジェクト オブジェクト<xref:EnvDTE.Projects>を`ProjectItems`実装することです。と`Project`<xref:EnvDTE.ProjectItem>オブジェクト。実装に固有の残りのオブジェクト。 これらの標準オブジェクトは、Dteinternal.h ファイルで定義されます。 標準オブジェクトの実装は、BscPrj サンプルで提供されています。 これらのクラスをモデルとして使用して、他のプロジェクト タイプのプロジェクト オブジェクトと並んで立つ独自の標準プロジェクト オブジェクトを作成できます。

 オートメーション コンシューマは<xref:EnvDTE.Solution>、(" と`<UniqueProjName>")`)<xref:EnvDTE.ProjectItems>`n`を呼び出すことができると推測されます。 このオートメーション呼び出しを行うと<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.GetProperty%2A>、環境は適切なプロジェクト階層を呼び出し、VSITEMID_ROOT ItemID パラメーターとして渡し、VSHPROPID パラメーターとしてVSHPROPID_ExtObjectします。 `IVsHierarchy::GetProperty`は、`IDispatch`実装したコア`Project`インターフェイスを提供するオートメーション オブジェクトへのポインタを返します。

 次に、 の構文`IVsHierarchy::GetProperty`を示します。

 `HRESULT GetProperty (`

 `VSITEMID` `itemid`,

 `VSHPROPID` `propid`,

 `VARIANT` `*pvar`

 `);`

 プロジェクトは入れ子に対応し、コレクションを使用してプロジェクト項目のグループを作成します。 階層は次のようになります。

```
Projects
  |- Project
      |- ProjectItems (a collection of ProjectItem)
          |- ProjectItem (single object) or ProjectItems (another collection)
```

 入れ子とは<xref:EnvDTE.ProjectItem>、入れ<xref:EnvDTE.ProjectItems>子になったオブジェクトをコレクションに含`ProjectItems`めることができるので、オブジェクトを同時にコレクションにできることを意味します。 基本プロジェクトのサンプルでは、この入れ子の例は示されていません。 オブジェクトを`Project`実装すると、オートメーション モデル全体の設計を特徴付けたツリーのような構造に参加できます。

 プロジェクトの自動化は、次の図のパスに従います。

 ![プロジェクト オブジェクト](../../extensibility/internals/media/projectobjects.gif "ProjectObjects")プロジェクトの自動化

 オブジェクトを`Project`実装しない場合でも、環境はプロジェクトの名前のみを含む`Project`ジェネリック オブジェクトを返します。

## <a name="see-also"></a>関連項目
- <xref:EnvDTE.Projects>
- <xref:EnvDTE.ProjectItem>
- <xref:EnvDTE.ProjectItems>
