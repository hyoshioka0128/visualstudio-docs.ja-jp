---
title: 1つのファイルジェネレーターの登録 |Microsoft Docs
description: Visual Studio でカスタムツールを登録してインスタンス化し、特定のプロジェクトの種類に関連付ける方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7a0ce4afeddebdec8519467e1f4249095ce98f6b
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97875259"
---
# <a name="registering-single-file-generators"></a>単一ファイル ジェネレーターの登録
でカスタムツールを使用できるようにするには、そのツールを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] インスタンス化して特定のプロジェクトの種類に関連付けることができるように、登録する必要があります。

### <a name="to-register-a-custom-tool"></a>カスタムツールを登録するには

1. カスタムツール DLL は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ローカルレジストリまたはシステムレジストリの [HKEY_CLASSES_ROOT] の下に登録します。

    たとえば、次のようなマネージ MSDataSetGenerator カスタムツールの登録情報を次に示し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]
   @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"
   "ThreadingModel"="Both"
   "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"
   ```

2. [ジェネレーター guid] の下にある目的の hive でレジストリキーを作成し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] \\ ます。 *guid* は、特定の言語のプロジェクトシステムまたはサービスによって定義された guid です。 キーの名前は、カスタムツールのプログラム名になります。 カスタムツールキーの値は次のとおりです。

   - (既定値)。

        省略可能。 カスタムツールについてのわかりやすい説明を提供します。 このパラメーターは省略可能ですが、推奨されます。

   - CLSID

        必須。 を実装する COM コンポーネントのクラスライブラリの識別子を指定し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> ます。

   - GeneratesDesignTimeSource

        必須。 このカスタムツールによって生成されたファイルの型をビジュアルデザイナーで使用できるようにするかどうかを示します。 このパラメーターの値は、ビジュアルデザイナーで使用できない型の場合は (0) 0、ビジュアルデザイナーで使用できる型の場合は (1) 0 である必要があります。

   > [!NOTE]
   > カスタムツールを使用する言語ごとに、カスタムツールを個別に登録する必要があります。

    たとえば、MSDataSetGenerator は、言語ごとに1回登録します。

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{164b10b9-b200-11d0-8c61-00a0c91e29d5}\MSDataSetGenerator]
   @="Microsoft VB Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001

   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{fae04ec1-301f-11d3-bf4b-00c04f79efbc}\MSDataSetGenerator]
   @="Microsoft C# Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001
   ```

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>
- [単一ファイル ジェネレーターの実装](../../extensibility/internals/implementing-single-file-generators.md)
- [ビジュアル デザイナーへのタイプの公開](../../extensibility/internals/exposing-types-to-visual-designers.md)
- [BuildManager オブジェクトの概要](/previous-versions/8f9kffa8(v=vs.140))