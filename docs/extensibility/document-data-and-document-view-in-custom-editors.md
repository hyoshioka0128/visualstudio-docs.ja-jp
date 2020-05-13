---
title: カスタム エディタでのドキュメント データとドキュメント ビュー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 04e89194ff09bc273294246cc25718c999daf70f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712143"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>カスタム エディターでのドキュメント データとドキュメント ビュー
カスタム エディターは、ドキュメント データ オブジェクトとドキュメント ビュー オブジェクトの 2 つの部分で構成されます。 名前が示すように、ドキュメント データ オブジェクトは表示されるテキスト データを表します。 同様に、ドキュメント ビュー オブジェクト (または "ビュー" ) は、ドキュメント データ オブジェクトを表示する 1 つまたは複数のウィンドウを表します。

## <a name="document-data-object"></a>ドキュメント データ オブジェクト
 ドキュメント データ オブジェクトは、テキスト バッファー内のテキストのデータ表現です。 ドキュメント テキストおよびその他の情報を格納する COM オブジェクトです。 ドキュメント データ オブジェクトは、ドキュメントの永続化も処理し、データの複数のビューを有効にします。 詳細については、「

 <xref:EnvDTE80.Window2.DocumentData%2A>[およびドキュメント ウィンドウ](../extensibility/internals/document-windows.md)。

 カスタム エディターおよびデザイナーは、オブジェクトまたは独自<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>のカスタム バッファーを使用できます。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>標準エディタの簡略化された埋め込みモデルに従い、複数のビューをサポートし、複数のビューを管理するために使用されるイベントインターフェイスを提供します。

## <a name="document-view-object"></a>ドキュメント ビュー オブジェクト
 コードやその他のテキストを表示するウィンドウは、ドキュメント ビューまたはビューと呼ばれます。 エディターを作成する場合、1 つのウィンドウにテキストを表示する単一のビューを選択できます。 または、複数のウィンドウにテキストを表示する複数のビューを選択できます。 選択はアプリケーションによって異なります。 たとえば、サイド バイ サイド編集が必要な場合は、複数のビューを選択します。 各ビューは、統合開発環境 (IDE) 実行中のドキュメントテーブル (RDT) のエントリに関連付けられます。 ビュー ウィンドウは、プロジェクトまたはオブジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>に属します。

 エディターがドキュメント データ オブジェクトの複数のビューをサポートしている場合は、ドキュメント データとドキュメント ビュー オブジェクトを個別に使用する必要があります。 それ以外の場合は、グループ化できます。 詳細については、「[複数のドキュメント ビューをサポート](../extensibility/supporting-multiple-document-views.md)する 」を参照してください。

 IDE は、実行中のドキュメント テーブルの各エントリの項目識別子 (ItemID) を照合することによって、イベント (たとえば、ドキュメントを含むソリューションが閉じられた場合) に関するビューに通知します。 詳細については、「ドキュメント テーブルの[実行](../extensibility/internals/running-document-table.md)」を参照してください。

 カスタム エディターのビューを作成するには、2 つのオプションがあります。 1 つは、ActiveX コントロールまたはドキュメント データ オブジェクトを使用してウィンドウでビューがホストされるインプレース アクティブ化モデルです。 2 つ目は、ビューがホストされ[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]、ウィンドウ コマンドを処理するために実装される<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>、簡略化された埋め込みモデルです。 インプレース アクティブ化モデルの詳細については、「インプレー[ス アクティブ化](/visualstudio/misc/in-place-activation?view=vs-2015)」を参照してください。 簡略化された埋め込みモデルの詳細については、「[簡易埋め込み」を](../extensibility/simplified-embedding.md)参照してください。

## <a name="see-also"></a>関連項目

- [複数のドキュメント ビューをサポート](../extensibility/supporting-multiple-document-views.md)
- [簡単な埋め込み](../extensibility/simplified-embedding.md)
- [方法: ドキュメント データにビューを添付する](../extensibility/how-to-attach-views-to-document-data.md)
- [ドキュメントロックホルダー管理](../extensibility/document-lock-holder-management.md)
- [単一および複数タブのビュー](../extensibility/single-and-multi-tab-views.md)
- [標準ドキュメントを保存する](../extensibility/internals/saving-a-standard-document.md)
- [永続性と実行中のドキュメントテーブル](../extensibility/internals/persistence-and-the-running-document-table.md)
- [プロジェクト内のファイルを開くエディタを決定する](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)
