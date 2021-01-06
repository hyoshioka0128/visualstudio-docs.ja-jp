---
title: Visual Studio でのワークスペースのインデックス作成 |Microsoft Docs
description: ワークスペースのインデックス作成について説明します。これは、開いているフォルダーワークスペースの豊富な IDE 機能をサポートするためのデータの収集と永続的なストレージです。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 6b5c069ce3ae993f2d2371bffae3ac58b286fa70
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877053"
---
# <a name="workspace-indexing"></a>ワークスペースのインデックス作成

ソリューションでは、プロジェクトシステムはビルド、デバッグ、 **GoTo** シンボル検索などの機能を提供する役割を担います。 プロジェクトシステムでは、プロジェクト内のファイルの関係と機能を理解しているため、この作業を行うことができます。 [[フォルダーを開く](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)] ワークスペースは、豊富な IDE 機能を提供するためにも同じ洞察を必要とします。 このデータの収集と永続的なストレージは、ワークスペースのインデックス作成と呼ばれるプロセスです。 このインデックス付きデータは、一連の非同期 Api を使用して照会できます。 エクステンダーは、 <xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScanner> 特定の種類のファイルの処理方法を認識するを指定することによって、インデックス作成プロセスに参加できます。

## <a name="types-of-indexed-data"></a>インデックス付きデータの種類

インデックスが作成されるデータには3種類あります。 メモファイルスキャナーからの型は、インデックスから逆シリアル化された型とは異なることに注意してください。

|Data|ファイルスキャナーの種類|インデックスクエリの結果の種類|関連する型|
|--|--|--|--|
|リファレンス|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfo>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceResult>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfoType>|
|シンボル|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinition>|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinitionSearchResult>|<xref:Microsoft.VisualStudio.Workspace.Indexing.ISymbolService>クエリではなくを使用する必要があります。 `IIndexWorkspaceService`|
|データ値|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataValue>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataResult`1>||

## <a name="querying-for-indexed-data"></a>インデックス付きデータのクエリ

永続化されたデータにアクセスするには、2つの非同期型を使用できます。 最初の方法は、を使用することです <xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceData> 。 1つのファイルとデータへの基本的なアクセスを提供 `FileReferenceResult` `FileDataResult` し、結果をキャッシュします。 2つ目は、 <xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceService> キャッシュを使用しないが、より多くのクエリ機能を使用できることです。

```csharp
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Indexing;

private static IIndexWorkspaceData GetCachedIndexedData(IWorkspace workspace)
{
    // Gets access to indexed data wrapped in a cache.
    return workspace?.GetIndexWorkspaceDataService()?.CreateIndexWorkspaceData();
}

private static IIndexWorkspaceService GetDirectIndexedData(IWorkspace workspace)
{
    // Gets direct access to indexed data.
    // Can also be casted to IIndexWorkspaceService2.
    return workspace?.GetIndexWorkspaceService();
}
```

## <a name="participating-in-indexing"></a>インデックス作成に参加する

ワークスペースのインデックス作成は、おおよそ次の順序に従っています。

1. ワークスペース内のファイルシステムエンティティの検出と永続化 (最初に開いているスキャンの場合のみ)。
1. ファイルごとに、優先順位が最も高い一致プロバイダーがをスキャンするように求められ `FileReferenceInfo` ます。
1. ファイルごとに、優先順位が最も高い一致プロバイダーがをスキャンするように求められ `SymbolDefinition` ます。
1. ファイルごとに、すべてのプロバイダーに s が要求され `FileDataValue` ます。

拡張機能 `IWorkspaceProviderFactory<IFileScanner>` では、を使用して型を実装およびエクスポートすることによって、スキャナーをエクスポートでき <xref:Microsoft.VisualStudio.Workspace.Indexing.ExportFileScannerAttribute> ます。 `SupportedTypes`属性引数は、の1つ以上の値である必要があり <xref:Microsoft.VisualStudio.Workspace.Indexing.FileScannerTypeConstants> ます。 スキャナーの例については、VS SDK [サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples/blob/master/Open_Folder_Extensibility/C%23/SymbolScannerSample/TxtFileSymbolScanner.cs)を参照してください。

> [!WARNING]
> 種類がサポートされているファイルスキャナーはエクスポートしないでください `FileScannerTypeConstants.FileScannerContentType` 。 Microsoft の内部的な目的でのみ使用されます。

高度な状況では、拡張機能がファイルの種類の任意のセットを動的にサポートする場合があります。 MEF エクスポートではなく `IWorkspaceProviderFactory<IFileScanner>` 、拡張機能でエクスポートでき `IWorkspaceProviderFactory<IFileScannerProvider>` ます。 インデックス作成が開始されると、このファクトリ型はインポートされ、インスタンス化され、その <xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScannerProvider.GetSymbolScannersAsync%2A> メソッドが呼び出されます。 `IFileScanner` の任意の値をサポート `FileScannerTpeConstants` するインスタンスは、記号だけでなく、有効になります。

## <a name="next-steps"></a>次のステップ

* [ワークスペースと言語サービス](workspace-language-services.md) -言語サービスを開いているフォルダーワークスペースに統合する方法について説明します。
* [ワークスペースビルド](workspace-build.md) -オープンフォルダーは、MSBuild やメイクファイルなどのビルドシステムをサポートします。