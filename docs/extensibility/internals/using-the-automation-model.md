---
title: オートメーションモデルの使用 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], automation model
ms.assetid: 0c7f7889-fbfb-4b19-804f-b742138baecd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2b9d7bd789a41f7a5e801552ca07f9f228921867
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704219"
---
# <a name="using-the-automation-model"></a>オートメーション モデルの使用
VSPackage をオートメーションに接続した後、<xref:EnvDTE.DTEClass.GetObject%2A><xref:EnvDTE._DTE>取得するオブジェクトを表す文字列を渡して、オブジェクトのメソッドを呼び出すことによって、プロパティとメソッドを取得できます。

## <a name="obtaining-project-objects"></a>プロジェクト オブジェクトの取得
 オートメーション コンシューマーがプロジェクトオートメーション オブジェクトを取得する方法を示す 2 つのコード例を次に示します。 DTE オブジェクトを取得する方法については、「方法[: DTE オブジェクトおよび DTE2 オブジェクトへの参照を取得する](https://msdn.microsoft.com/Library/c92e3c8e-82e6-4a67-85da-e43c50ffd8e4)」を参照してください。

```vb
Sub DoAutomation()
    Dim MyProjects As Projects
    MyProjects = DTE.GetObject("AcmeProject")
End Sub
```

```cpp
void DoAutomation(void)
{
  CComQIPtr<Projects> pMyPkg; // Use an IDispatch-derived object type.
    pMyPkg = pDTE->GetObject("AcmeProjects");

   // The '=' performs a Query Interface.
   // Assumes pDTE is already available as a global.
   // Use pMyPkg to access your projects object's properties and methods.
}

```

 この時点で、特定の VSPackage の一部である標準プロジェクト オブジェクトを使用して、階層モデルを下に移動できます。

 カスタム プロジェクトの種類のプロパティであるカスタム オブジェクトを取得する方法を次のコード例に示します。

```vb
Dim MyPrj As Project
Dim MyPrjItem As ProjectItem
Dim objMyObject as MyExtendedObject

MyPrj = MyProjects.Item(1) 'use the Projects collection to get a project
objMyObject = MyPrj.Object 'You call .Object to get to special Project
                           'implementation
objMyObject.MySpecialMethodOrProperty
```

 次のコードは、[[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**ツール]** メニューの [**全般**] オプションの環境のすべてのプロパティの名前を示しています。

```vb
dim objDTE
dim objEnv
set objDTE = CreateObject("VisualStudio.DTE")
set objEnv = objDTE.Properties("Environment", "General")
for each obj in ObjEnv
MsgBox obj.Name
Next

```

## <a name="see-also"></a>関連項目
- <xref:EnvDTE.DTEClass.GetObject%2A>
