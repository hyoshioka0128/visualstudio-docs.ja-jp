---
title: 簡略化された埋め込み |Microsoft Docs
description: ドキュメントビューオブジェクトが Visual Studio の子である場合にエディターで有効にできる、簡略化された埋め込みについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - simple view embedding
ms.assetid: f1292478-a57d-48ec-8c9e-88a23f04ffe5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f62e3a4f33193f36e76b1286ae3d35d26706b3ac
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99928095"
---
# <a name="simplified-embedding"></a>簡略化された埋め込み
簡略化された埋め込みは、ドキュメントビューオブジェクトが親 (つまり、の子) であり、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> そのウィンドウコマンドを処理するためにインターフェイスが実装されている場合に、エディターで有効になります。 簡略化された埋め込みエディターは、アクティブなコントロールをホストできません。 簡略化された埋め込みを使用してエディターを作成するために使用するオブジェクトを次の図に示します。

 簡略化された![埋め込みエディターグラフィック](../extensibility/media/vssimplifiedembeddingeditor.gif "vsSimplifiedEmbeddingEditor")簡略化された埋め込みのエディター

> [!NOTE]
> この図のオブジェクトのうち、 `CYourEditorFactory` 標準的なファイルベースのエディターを作成するために必要なのはオブジェクトだけです。 カスタムエディターを作成する場合、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> エディターは独自のプライベート永続化メカニズムを持つ可能性があるため、を実装する必要はありません。 ただし、カスタムエディター以外の場合は、これを行う必要があります。

 簡略化された埋め込みを使用してエディターを作成するために実装されるすべてのインターフェイスは、オブジェクトに含まれてい `CYourEditorDocument` ます。 ただし、ドキュメントデータの複数のビューをサポートするには、次の表に示すように、インターフェイスを別のデータに分割し、オブジェクトを表示します。

|インターフェイス|インターフェイスの場所|用途|
|---------------|---------------------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|表示|親ウィンドウへの接続を提供します。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|表示|コマンドを処理します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|表示|ステータス バーを更新できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|表示|**ツールボックス** 項目を有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|データ|ファイルが変更されたときに通知を送信します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|データ|ファイルの種類に対して名前を付けて保存機能を有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>|データ|ドキュメントの永続性を有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|データ|再読み込みのトリガーなど、ファイル変更イベントの抑制を許可します。|
