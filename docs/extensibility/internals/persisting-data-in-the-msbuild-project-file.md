---
title: MSBuild プロジェクトファイル内のデータの永続化 |Microsoft Docs
description: プロジェクトファイルにデータを保存し、IPersistXMLFragment を使用してプロジェクトファイル内のデータをプロジェクトのサブタイプ集計レベル全体で維持する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5e2cf082e4ca6a45bf42bd66ce34111d5c056787
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095018"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>MSBuild プロジェクト ファイルでのデータの保持
プロジェクトのサブタイプは、後で使用するために、サブタイプ固有のデータをプロジェクトファイルに保存する必要がある場合があります。 プロジェクトのサブタイプは、次の要件を満たすためにプロジェクトファイルの永続化を使用します。

1. プロジェクトのビルドの一部として使用されるデータを保持します。 (Microsoft Build Engine の詳細については、「 [MSBuild](../../msbuild/msbuild.md)」を参照してください)。ビルド関連の情報は、次のいずれかになります。

    1. 構成に依存しないデータ。 つまり、条件が空白または不足している MSBuild 要素に格納されているデータです。

    2. 構成に依存するデータ。 つまり、特定のプロジェクト構成に対して条件を設定した MSBuild 要素に格納されたデータ。 次に例を示します。

        ```
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        ```

2. ビルドに関連しないデータを保持します。 このデータは、XML スキーマに対して検証されない自由形式の XML で表現できます。

    1. 構成に依存しないデータ。

    2. 構成に依存するデータ。

## <a name="persisting-build-related-information"></a>Build-Related 情報の保持
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

## <a name="see-also"></a>こちらもご覧ください
- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)
