---
title: '方法: ドキュメント データにビューを添付する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - attach views to document data
ms.assetid: f92c0838-45be-42b8-9c55-713e9bb8df07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d8bd586a9d67996389f3cb6a2b0f13f0afec3bd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711083"
---
# <a name="how-to-attach-views-to-document-data"></a>方法: ドキュメント データにビューを添付する
新しいドキュメント ビューを使用している場合は、既存のドキュメント データ オブジェクトに添付できる場合があります。

## <a name="to-determine-if-you-can-attach-a-view-to-an-existing-document-data-object"></a>既存のドキュメント データ オブジェクトにビューをアタッチできるかどうかを確認するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>を実装します。

2. `IVsEditorFactory::CreateEditorInstance`の実装で、IDE`QueryInterface`が実装を呼び出すときに、既存の`CreateEditorInstance`ドキュメント データ オブジェクトを呼び出します。

    呼`QueryInterface`び出しを使用すると、パラメーターで指定されている既存のドキュメント`punkDocDataExisting`データ オブジェクトを調べることができます。

    ただし、クエリを実行する必要があるインターフェイスは、手順 4 で説明したように、ドキュメントを開いているエディターによって異なります。

3. 既存のドキュメント データ オブジェクトに適切なインターフェイスが見つからない場合は、ドキュメント データ オブジェクトがエディターと互換性ないことを示すエラー コードをエディターに返します。

    IDE の実装では、ドキュメント<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>が別のエディタで開かっていることを示すメッセージ ボックスが表示され、ドキュメントを閉じるかどうかを確認するメッセージが表示されます。

4. このドキュメントを閉じると、Visual Studio によってエディター ファクトリが 2 回目に呼び出されます。 この呼び出し`DocDataExisting`では、パラメーターは NULL に等しくなります。 エディター ファクトリの実装は、ドキュメント データ オブジェクトを独自のエディターで開くことができます。

   > [!NOTE]
   > 既存のドキュメント データ オブジェクトを操作できるかどうかを判断するには、プライベート実装の実際[!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)]のクラスへのポインターをキャストすることで、インターフェイス実装のプライベートな知識を使用することもできます。 たとえば、すべての標準エディタは、`IVsPersistFileFormat`から<xref:Microsoft.VisualStudio.OLE.Interop.IPersist>継承する を実装します。 したがって、 を呼`QueryInterface`び<xref:Microsoft.VisualStudio.OLE.Interop.IPersist.GetClassID%2A>出し、既存のドキュメント データ オブジェクトのクラス ID が実装のクラス ID と一致する場合は、ドキュメント データ オブジェクトを操作できます。

## <a name="robust-programming"></a>信頼性の高いプログラミング
 Visual Studio は、メソッドの<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>実装を呼び出すときに、パラメーター内の既存のドキュメント データ`punkDocDataExisting`オブジェクトへのポインターを渡します (存在する場合)。 返されたドキュメント データ オブジェクト`punkDocDataExisting`を調べて、このトピックの手順 4 のメモに示すように、ドキュメント データ オブジェクトがエディターに適しているかどうかを確認します。 適切な場合は、「複数のドキュメント ビューをサポートする 」で説明したように、エディター ファクトリにデータの 2 番目の[ビューを提供する](../extensibility/supporting-multiple-document-views.md)必要があります。 表示されない場合は、適切なエラー メッセージが表示されます。

## <a name="see-also"></a>関連項目
- [複数のドキュメント ビューをサポート](../extensibility/supporting-multiple-document-views.md)
- [カスタム エディターでのドキュメント データとドキュメント ビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)
