---
title: プロジェクトモデリング |Microsoft Docs
description: 新しいプロジェクトの種類のオートメーションを作成するために必要な標準プロジェクトオブジェクトと、プロジェクトオートメーションが従うパスについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 7a481e731f01230139ec4342231479606c49bd11
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877417"
---
# <a name="project-modeling"></a>プロジェクトのモデリング
プロジェクトの自動化を提供する次の手順では、標準のプロジェクトオブジェクトを実装します。これは、 <xref:EnvDTE.Projects> との `ProjectItems` コレクション、 `Project` オブジェクトとオブジェクト、および <xref:EnvDTE.ProjectItem> 実装に固有の残りのオブジェクトです。 これらの標準オブジェクトは、Dteinternal .h ファイルで定義されています。 標準オブジェクトの実装は、BscPrj サンプルに用意されています。 これらのクラスをモデルとして使用して、他のプロジェクトの種類のプロジェクトオブジェクトとサイドバイサイドで実行する独自の標準プロジェクトオブジェクトを作成できます。

 オートメーションコンシューマーは、("と () を呼び出すことができることを前提としてい <xref:EnvDTE.Solution> `<UniqueProjName>")` <xref:EnvDTE.ProjectItems> `n` ます。ここで、n は、ソリューション内の特定のプロジェクトを取得するためのインデックス番号です。 このオートメーション呼び出しを行うと、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.GetProperty%2A> 適切なプロジェクト階層で環境が呼び出され、ItemID パラメーターとして VSITEMID_ROOT が渡され、VSHPROPID パラメーターとして VSHPROPID_ExtObject されます。 `IVsHierarchy::GetProperty``IDispatch`実装したコアインターフェイスを提供するオートメーションオブジェクトへのポインターを返し `Project` ます。

 の構文を次に示し `IVsHierarchy::GetProperty` ます。

 `HRESULT GetProperty (`

 `VSITEMID` `itemid`,

 `VSHPROPID` `propid`,

 `VARIANT` `*pvar`

 `);`

 プロジェクトは、入れ子にすることができ、コレクションを使用してプロジェクト項目のグループを作成します。 階層は次のようになります。

```
Projects
  |- Project
      |- ProjectItems (a collection of ProjectItem)
          |- ProjectItem (single object) or ProjectItems (another collection)
```

 入れ子とは、 <xref:EnvDTE.ProjectItem> <xref:EnvDTE.ProjectItems> `ProjectItems` コレクションに入れ子になったオブジェクトを含めることができるため、オブジェクトを同時にコレクションにすることができることを意味します。 基本的なプロジェクトのサンプルでは、この入れ子については説明しません。 オブジェクトを実装することにより `Project` 、オートメーションモデル全体の設計を特徴とするツリーのような構造に関与します。

 プロジェクトオートメーションは、次の図のパスに従います。

 ![Visual Studio プロジェクトオブジェクト](../../extensibility/internals/media/projectobjects.gif "ProjectObjects") プロジェクトの自動化

 オブジェクトを実装しない場合 `Project` でも、プロジェクトの名前のみを含む汎用オブジェクトが環境によって返され `Project` ます。

## <a name="see-also"></a>関連項目
- <xref:EnvDTE.Projects>
- <xref:EnvDTE.ProjectItem>
- <xref:EnvDTE.ProjectItems>
