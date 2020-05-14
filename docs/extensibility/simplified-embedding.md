---
title: 簡易埋め込み |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - simple view embedding
ms.assetid: f1292478-a57d-48ec-8c9e-88a23f04ffe5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b9bc9619ae1ed75aed3656ff014296f7c7d88fa0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700074"
---
# <a name="simplified-embedding"></a>簡略化された埋め込み
簡易埋め込みは、ドキュメント ビュー オブジェクトが (つまり、 子にされた)[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]に親として配置され、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>ウィンドウ コマンドを処理するためにインターフェイスが実装されている場合に、エディターで有効になります。 簡略化された埋め込みエディターは、アクティブなコントロールをホストできません。 埋め込みを簡略化したエディターの作成に使用するオブジェクトを次の図に示します。

 ![簡易埋め込みエディタグラフィック](../extensibility/media/vssimplifiedembeddingeditor.gif "を簡略化する埋め込みエディター")シンプルな埋め込みエディター

> [!NOTE]
> この図のオブジェクトのうち、標準のファイル`CYourEditorFactory`ベースエディタを作成するために必要なのはオブジェクトだけです。 カスタム エディターを作成する場合、エディターには独自のプライベート永続<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>性メカニズムが用意されている可能性があるため、 を実装する必要はありません。 ただし、カスタムエディター以外の場合は、その操作を行う必要があります。

 簡略化された埋め込みエディターを作成するために実装されたすべてのインターフェイスは、オブジェクトに`CYourEditorDocument`含まれています。 ただし、ドキュメント データの複数のビューをサポートするには、次の表に示すように、インターフェイスを個別のデータに分割し、オブジェクトを表示します。

|インターフェイス|インターフェイスの場所|用途|
|---------------|---------------------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|View|親ウィンドウへの接続を提供します。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|View|コマンドを処理します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|View|ステータス バーを更新できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|View|**ツールボックス項目を**有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|Data|ファイルが変更されたときに通知を送信します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|Data|ファイルの種類に対して [名前を付けて保存] 機能を有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>|Data|ドキュメントの永続性を有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|Data|リロード・トリガーなどのファイル変更イベントを抑制できます。|
