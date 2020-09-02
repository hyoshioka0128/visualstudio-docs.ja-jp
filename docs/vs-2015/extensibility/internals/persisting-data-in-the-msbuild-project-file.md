---
title: MSBuild プロジェクトファイル内のデータの永続化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 39d2ab449c3623a90dd76729b46a9f353900fc88
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704112"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>MSBuild プロジェクト ファイルでのデータの保持
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクトのサブタイプは、後で使用するために、サブタイプ固有のデータをプロジェクトファイルに保存する必要がある場合があります。 プロジェクトのサブタイプは、次の要件を満たすためにプロジェクトファイルの永続化を使用します。  
  
1. プロジェクトのビルドの一部として使用されるデータを保持します。 (Microsoft Build Engine の詳細については、「 [MSBuild](https://msdn.microsoft.com/7c49aba1-ee6c-47d8-9de1-6f29a906e20b)」を参照してください)。ビルド関連の情報は、次のいずれかになります。  
  
    1. 構成に依存しないデータ。 つまり、条件が空白または不足している MSBuild 要素に格納されているデータです。  
  
    2. 構成に依存するデータ。 つまり、特定のプロジェクト構成に対して条件を設定した MSBuild 要素に格納されたデータ。 次に例を示します。  
  
        ```  
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">  
        ```  
  
2. ビルドに関連しないデータを保持します。 このデータは、XML スキーマに対して検証されない自由形式の XML で表現できます。  
  
    1. 構成に依存しないデータ。  
  
    2. 構成に依存するデータ。  
  
## <a name="persisting-build-related-information"></a>ビルド関連の情報の保持  
 プロジェクトのビルドに役立つデータの永続化は、MSBuild によって処理されます。 MSBuild システムは、ビルド関連の情報のマスターテーブルを保持します。 プロジェクトのサブタイプは、このデータにアクセスしてプロパティ値を取得および設定する役割を担います。 プロジェクトのサブタイプでは、永続化されるプロパティを追加し、永続化されないようにプロパティを削除することで、ビルド関連のデータテーブルを拡張することもできます。  
  
 MSBuild データを変更するために、プロジェクトのサブタイプは、を使用して基本プロジェクトシステムから MSBuild プロパティオブジェクトを取得し <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> は、コアプロジェクトシステムに実装されたインターフェイスであり、を実行して、プロジェクトのサブタイプを集計し `QueryInterface` ます。  
  
 次の手順では、を使用してプロパティを削除する手順について説明し <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> ます。  
  
#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>MSBuild プロジェクトファイルからプロパティを削除するには  
  
1. `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> プロジェクトのサブタイプのでを呼び出します。  
  
2. を <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A> `pszPropName` 、削除するプロパティに設定してを呼び出します。  
  
### <a name="persisting-non-build-related-information"></a>非ビルド関連情報の保持  
 ビルドに関係のないプロジェクトファイル内のデータの永続化は、によって処理され <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> ます。  
  
 は、 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> メインオブジェクト、オブジェクト、またはその両方に実装でき `project subtype aggregator` `project subtype project configuration` ます。  
  
 次の点は、非ビルド関連情報の永続化に関する主な概念の概要を示しています。  
  
- 基本プロジェクトは、メインプロジェクトのサブタイプ (つまり、最も外側のプロジェクトのサブタイプ) のアグリゲーターオブジェクトを呼び出して、構成に依存しないデータを読み込んで保存します。また、プロジェクトのサブタイププロジェクト構成オブジェクトでを呼び出して、構成依存データを読み込んだり保存したりします。  
  
- 基本プロジェクトは、 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> プロジェクトのサブタイプ集計の各レベルに対して複数回のメソッドを呼び出し、各レベルの GUID を渡します。  
  
- 基本プロジェクトは、特定のプロジェクトのサブタイプ専用の XML フラグメントを渡したり受け取り、集計レベル間で状態を保持する手段としてこの機構を使用します。  
  
- 基本プロジェクトは、GUID を渡す最も外側のプロジェクトサブタイプの実装を呼び出します <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 。 GUID が最も外側のプロジェクトのサブタイプに属している場合は、呼び出し自体を処理します。それ以外の場合は、内部プロジェクトのサブタイプへの呼び出しをデリゲートします。これは、GUID が対応するプロジェクトのサブタイプが検出されるまで続きます。  
  
- プロジェクトのサブタイプは、内部プロジェクトのサブタイプへの呼び出しをデリゲートする前または後に、XML フラグメントを変更することもできます。 次の例は、プロジェクトファイルからの抜粋を示しています。ここでは、プロジェクトのサブタイプに固有のプロパティを含むファイルの名前が、そのプロジェクトのサブタイプに渡されます。  
  
    ```  
    <ProjectExtensions>  
        <VisualStudio>  
          <FlavorProperties GUID="{<FlavorGUID>}">  
            <FlavorProject TestFileFolder="TestFile" />  
          </FlavorProperties>  
        </VisualStudio>  
      </ProjectExtensions>  
    ```  
  
## <a name="see-also"></a>参照  
 [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)
