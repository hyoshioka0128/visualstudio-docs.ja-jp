---
title: VSTU によって作成されるプロジェクト ファイルのカスタマイズ | Microsoft Docs
description: Visual Studio Tools for Unity (VSTU) によって作成されたプロジェクト ファイルをカスタマイズする方法について説明します。 C# コードの例を確認します。
ms.custom: ''
ms.date: 07/26/2018
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: 60b8cc1d-cacc-404d-b768-77e81bc354f8
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: a2e4abb707f07e0a781460e5efe6996325e5ca00
ms.sourcegitcommit: 01c1b040b12d9d43e3e8ccadee20d6282154faad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039426"
---
# <a name="customize-project-files-created-by-vstu"></a>VSTU によって作成されたプロジェクト ファイルのカスタマイズ
Visual Studio Tools for Unity は、プロジェクト ファイルの生成時に Unity スタイルのコールバックを提供します。 `VisualStudioIntegration.ProjectFileGeneration` イベントに登録し、プロジェクト ファイルが再生成されるたびに、それを変更します。

## <a name="demonstrates"></a>対象
 Visual Studio Tools for Unity によって生成された Visual Studio プロジェクト ファイルをカスタマイズする方法について示します。

## <a name="example"></a>例

```csharp
#if ENABLE_VSTU
using System;
using System.IO;
using System.Linq;
using System.Text;
using System.Xml.Linq;

using UnityEngine;
using UnityEditor;

using SyntaxTree.VisualStudio.Unity.Bridge;

[InitializeOnLoad]
public class ProjectFileHook
{
    // necessary for XLinq to save the xml project file in utf8
    class Utf8StringWriter : StringWriter
    {
        public override Encoding Encoding
        {
            get { return Encoding.UTF8; }
        }
    }

    static ProjectFileHook()
    {
        ProjectFilesGenerator.ProjectFileGeneration += (string name, string content) =>
        {
            // parse the document and make some changes
            var document = XDocument.Parse(content);
            document.Root.Add(new XComment("FIX ME"));

            // save the changes using the Utf8StringWriter
            var str = new Utf8StringWriter();
            document.Save(str);

            return str.ToString();
        };
    }
}
#endif
```

## <a name="see-also"></a>関連項目
 [例: ログのコールバック](../cross-platform/share-the-unity-log-callback-with-vstu.md)
