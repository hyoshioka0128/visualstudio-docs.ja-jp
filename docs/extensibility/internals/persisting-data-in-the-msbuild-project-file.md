---
title: MSBuild プロジェクト ファイルにデータを保存する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e83526007f676ae94ddce57936b627bcb4308c2a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706694"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>MSBuild プロジェクト ファイルでのデータの保持
プロジェクトのサブタイプは、後で使用するために、サブタイプ固有のデータをプロジェクト ファイルに保存する必要があります。 プロジェクトサブタイプは、プロジェクト ファイルの永続性を使用して、次の要件を満たします。

1. プロジェクトの構築の一部として使用されるデータを永続化します。 (マイクロソフト ビルド エンジンの詳細については[、MSBuild](../../msbuild/msbuild.md)を参照してください。ビルド関連の情報は、次のいずれかです。

    1. 構成に依存しないデータ。 つまり、空白または不足している条件を持つ MSBuild 要素に格納されているデータです。

    2. 構成依存データ。 つまり、特定のプロジェクト構成に合わせて条件付けされている MSBuild 要素に格納されているデータです。 次に例を示します。

        ```
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        ```

2. ビルドに関係しないデータを永続化します。 このデータは、XML スキーマに対して検証されない自由形式の XML で表現できます。

    1. 構成に依存しないデータ。

    2. 構成依存データ。

## <a name="persisting-build-related-information"></a>ビルド関連情報の保存
 プロジェクトのビルドに役立つデータの永続化は、MSBuild を通じて処理されます。 MSBuild システムは、ビルド関連情報のマスター テーブルを保持します。 プロジェクトのサブタイプは、プロパティ値を取得および設定するために、このデータにアクセスする役割を担います。 プロジェクト のサブタイプは、永続化するプロパティを追加し、永続化しないようにプロパティを削除することで、ビルド関連のデータ テーブルを拡張することもできます。

 MSBuild データを変更するには、プロジェクト のサブタイプが、基本プロジェクト システムから MSBuild プロパティ オブジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>を取得する役割を持ちます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>は、コア プロジェクト システムに実装されたインターフェイスであり、それを実行`QueryInterface`してプロジェクト サブタイプクエリを集計します。

 次の手順では、 を使用して<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>プロパティを削除する手順について説明します。

#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>MSBuild プロジェクト ファイルからプロパティを削除するには

1. プロジェクト`QueryInterface`<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>のサブタイプを呼び出します。

2. 削除<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A>する`pszPropName`プロパティを設定して呼び出します。

### <a name="persisting-non-build-related-information"></a>ビルド以外の関連情報の保持
 ビルドに関係しないプロジェクト ファイルのデータの永続性は、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>を介して処理されます。

 メイン<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>`project subtype aggregator`オブジェクト、オブジェクト、またはその両方に`project subtype project configuration`実装できます。

 以下の点は、非ビルド関連情報の永続化に関する主な概念を概説しています。

- 基本プロジェクトは、構成に依存するデータを読み込んで保存するために、メイン プロジェクト サブタイプ (つまり、最も外側のプロジェクトのサブタイプ) アグリゲータ オブジェクトを呼び出し、プロジェクト サブタイプ プロジェクト構成オブジェクトを呼び出して、構成に依存するデータを読み込むか保存します。

- 基本プロジェクトは、プロジェクトのサブ<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>タイプ集計のレベルごとに複数回のメソッドを呼び出し、各レベルの GUID を渡します。

- 基本プロジェクトは、特定のプロジェクト サブタイプ専用の XML フラグメントを渡すか受け取り、このメカニズムを集計レベル間で状態を保持する方法として使用します。

- 基本プロジェクトは、GUID を渡す最も外側<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>のプロジェクト サブタイプの実装を呼び出します。 GUID が最も外側のプロジェクト サブタイプに属している場合は、呼び出し自体を処理します。それ以外の場合は、GUID に対応するプロジェクトのサブタイプが見つかるまで、内部のプロジェクトのサブタイプに呼び出しを委任します。

- プロジェクトのサブタイプは、内部プロジェクトのサブタイプへの呼び出しのデリゲートの前または後に XML フラグメントを変更することもできます。 次の例は、プロジェクト ファイルからの抜粋を示しています。

    ```
    <ProjectExtensions>
        <VisualStudio>
          <FlavorProperties GUID="{<FlavorGUID>}">
            <FlavorProject TestFileFolder="TestFile" />
          </FlavorProperties>
        </VisualStudio>
      </ProjectExtensions>
    ```

## <a name="see-also"></a>関連項目
- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)
