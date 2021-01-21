---
title: '方法: ドキュメントデータにビューをアタッチする |Microsoft Docs'
description: 既存のドキュメントデータオブジェクトに新しいドキュメントビューをアタッチすることもできます。 ビューをアタッチできるかどうかを判断するには、次の手順に従います。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - attach views to document data
ms.assetid: f92c0838-45be-42b8-9c55-713e9bb8df07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1e044ecbf2309d4d858c16afbdddc130b4661005
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994187"
---
# <a name="how-to-attach-views-to-document-data"></a>方法: ドキュメントデータにビューをアタッチする
新しいドキュメントビューがある場合は、それを既存のドキュメントデータオブジェクトにアタッチすることができます。

## <a name="to-determine-if-you-can-attach-a-view-to-an-existing-document-data-object"></a>既存のドキュメントデータオブジェクトにビューをアタッチできるかどうかを判断するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>を実装します。

2. の実装では `IVsEditorFactory::CreateEditorInstance` 、 `QueryInterface` IDE がの実装を呼び出すと、既存のドキュメントデータオブジェクトに対してを呼び出し `CreateEditorInstance` ます。

    を呼び出す `QueryInterface` と、パラメーターに指定されている既存のドキュメントデータオブジェクトを調べることができ `punkDocDataExisting` ます。

    ただし、クエリを実行する必要があるインターフェイスは、手順 4. で説明したように、ドキュメントを開いているエディターによって異なります。

3. 既存のドキュメントデータオブジェクトに適切なインターフェイスが見つからない場合は、ドキュメントデータオブジェクトがエディターと互換性がないことを示すエラーコードをエディターに返します。

    IDE のの実装では <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 、ドキュメントが別のエディターで開かれていることを通知するメッセージボックスが表示され、ドキュメントを閉じるかどうかを確認するメッセージが表示されます。

4. このドキュメントを閉じると、Visual Studio は2回目のエディターファクトリを呼び出します。 この呼び出しでは、 `DocDataExisting` パラメーターは NULL と等しくなります。 エディターファクトリを実装すると、独自のエディターでドキュメントデータオブジェクトを開くことができます。

   > [!NOTE]
   > 既存のドキュメントデータオブジェクトを使用できるかどうかを判断するために、プライベート実装の実際のクラスへのポインターをキャストすることによって、インターフェイスの実装に関するプライベートな知識を使用することもでき [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] ます。 たとえば、すべての標準エディターは `IVsPersistFileFormat` 、から継承するを実装し <xref:Microsoft.VisualStudio.OLE.Interop.IPersist> ます。 したがって、に対してを呼び出すことができます `QueryInterface` <xref:Microsoft.VisualStudio.OLE.Interop.IPersist.GetClassID%2A> 。また、既存のドキュメントデータオブジェクトのクラス id が実装のクラス id と一致する場合は、ドキュメントデータオブジェクトを操作できます。

## <a name="robust-programming"></a>信頼性の高いプログラミング
 Visual Studio がメソッドの実装を呼び出すと <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 、パラメーター内の既存のドキュメントデータオブジェクトへのポインターが渡さ `punkDocDataExisting` れます (存在する場合)。 で返されたドキュメントデータオブジェクトを調べ `punkDocDataExisting` て、ドキュメントデータオブジェクトがエディターに適しているかどうかを確認します。これについては、このトピックの手順 4. のメモを参照してください。 適切な場合は、「 [複数のドキュメントビューのサポート](../extensibility/supporting-multiple-document-views.md)」で説明されているように、エディターファクトリはデータの2番目のビューを提供する必要があります。 そうでない場合は、適切なエラーメッセージが表示されます。

## <a name="see-also"></a>こちらもご覧ください
- [複数のドキュメントビューのサポート](../extensibility/supporting-multiple-document-views.md)
- [カスタムエディターでのドキュメントデータとドキュメントビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)
