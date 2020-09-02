---
title: 1つのファイルジェネレーターの登録 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6afcd708ac50a46ceb3359f0d2c0821e3b788f47
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696104"
---
# <a name="registering-single-file-generators"></a>単一ファイル ジェネレーターの登録
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

でカスタムツールを使用できるようにするには、そのツールを [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] インスタンス化して特定のプロジェクトの種類に関連付けることができるように、登録する必要があります。  
  
### <a name="to-register-a-custom-tool"></a>カスタムツールを登録するには  
  
1. カスタムツール DLL は、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ローカルレジストリまたはシステムレジストリの [HKEY_CLASSES_ROOT] の下に登録します。  
  
     たとえば、次のようなマネージ MSDataSetGenerator カスタムツールの登録情報を次に示し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
    ```  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]  
    @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"  
    "ThreadingModel"="Both"  
    "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"  
    ```  
  
2. [ジェネレーター guid] の下にある目的の hive でレジストリキーを作成し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] \\ *GUID*ます。 *guid*は、特定の言語のプロジェクトシステムまたはサービスによって定義された guid です。 キーの名前は、カスタムツールのプログラム名になります。 カスタムツールキーの値は次のとおりです。  
  
    - (既定)  
  
         省略可能。 カスタムツールについてのわかりやすい説明を提供します。 このパラメーターは省略可能ですが、推奨されます。  
  
    - CLSID  
  
         必須です。 を実装する COM コンポーネントのクラスライブラリの識別子を指定し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> ます。  
  
    - GeneratesDesignTimeSource  
  
         必須です。 このカスタムツールによって生成されたファイルの型をビジュアルデザイナーで使用できるようにするかどうかを示します。 このパラメーターの値は、ビジュアルデザイナーで使用できない型の場合は (0) 0、ビジュアルデザイナーで使用できる型の場合は (1) 0 である必要があります。  
  
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
  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{e6fdf8b0-f3d1-11d4-8576-0002a516ece8}\MSDataSetGenerator]  
    @="Microsoft J# Code Generator for XSD"  
    "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"  
    "GeneratesDesignTimeSource"=dword:00000001  
    ```  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>   
 [単一ファイルジェネレーターの実装](../../extensibility/internals/implementing-single-file-generators.md)   
 [プロジェクトの既定の名前空間の決定](../../misc/determining-the-default-namespace-of-a-project.md)   
 [ビジュアルデザイナーへの型の公開](../../extensibility/internals/exposing-types-to-visual-designers.md)   
 [BuildManager オブジェクトの概要](https://msdn.microsoft.com/50080ec2-c1c9-412c-98ef-18d7f895e7fa)
