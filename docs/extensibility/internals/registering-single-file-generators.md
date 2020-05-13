---
title: 単一ファイル ジェネレータの登録 |マイクロソフトドキュメント
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
ms.openlocfilehash: 1cea2ebba4739695393447a36e9842ade1670954
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705812"
---
# <a name="registering-single-file-generators"></a>単一ファイル ジェネレーターの登録
でカスタム ツールを使用できるようにするには[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]カスタム ツールを登録してインスタンス化し、特定のプロジェクトの種類に関連付ける必要があります。

### <a name="to-register-a-custom-tool"></a>カスタム ツールを登録するには

1. ローカル レジストリまたはシステム レジストリの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)][HKEY_CLASSES_ROOT] でカスタム ツール DLL を登録します。

    たとえば、次の表に示すマネージ MSDataSetGenerator カスタム ツールの登録情報を[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]示します。

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]
   @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"
   "ThreadingModel"="Both"
   "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"
   ```

2. 特定の言語のプロジェクト システム[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]またはサービスによって定義\\された*GUID*であるジェネレーター*の GUID*の下で目的のハイブにレジストリ キーを作成します。 キーの名前は、カスタム ツールのプログラム名になります。 カスタム ツール キーには、次の値があります。

   - (既定値)。

        省略可能。 カスタム ツールのわかりやすい説明を提供します。 このパラメーターはオプションですが、推奨されます。

   - CLSID

        必須。 を実装する COM コンポーネントのクラス ライブラリの識別子を<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>指定します。

   - デザインタイムソースを生成します。

        必須。 このカスタム ツールによって生成されたファイルの型をビジュアル デザイナーで使用できるかどうかを示します。 ビジュアル デザイナーでは使用できない型の場合は、このパラメーターの値は 0 (ゼロ) にする必要があります。

   > [!NOTE]
   > カスタム ツールを使用できるようにする言語ごとに、カスタム ツールを個別に登録する必要があります。

    たとえば、MSDataSetGenerator は、言語ごとに 1 回登録します。

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
- [BuildManager オブジェクトの概要](https://msdn.microsoft.com/library/50080ec2-c1c9-412c-98ef-18d7f895e7fa)
