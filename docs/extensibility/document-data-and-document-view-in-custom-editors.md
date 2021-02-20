---
title: カスタムエディターでのドキュメントデータとドキュメントビュー |Microsoft Docs
description: ドキュメントデータオブジェクトとドキュメントビューオブジェクトであるカスタムエディターのコンポーネントについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 89f2903b2ec1308692f629c40af06f89706a427b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968295"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>カスタムエディターでのドキュメントデータとドキュメントビュー
カスタムエディターは、ドキュメントデータオブジェクトとドキュメントビューオブジェクトの2つの部分で構成されます。 名前が示すように、ドキュメントデータオブジェクトは表示されるテキストデータを表します。 同様に、ドキュメントビューオブジェクト (または "ビュー") は、ドキュメントデータオブジェクトを表示する1つまたは複数のウィンドウを表します。

## <a name="document-data-object"></a>ドキュメントデータオブジェクト
 ドキュメントデータオブジェクトは、テキストバッファー内のテキストのデータ表現です。 これは、ドキュメントのテキストやその他の情報を格納する COM オブジェクトです。 また、ドキュメントデータオブジェクトは、ドキュメントの永続化を処理し、データの複数のビューを有効にします。 詳細については、「

 <xref:EnvDTE80.Window2.DocumentData%2A> および [ドキュメントウィンドウ](../extensibility/internals/document-windows.md)。

 カスタムエディターとデザイナーでは、 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> オブジェクトまたは独自のカスタムバッファーを使用することを選択できます。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 標準エディターの簡略化された埋め込みモデルに従い、複数のビューをサポートし、複数のビューを管理するために使用されるイベントインターフェイスを提供します。

## <a name="document-view-object"></a>ドキュメントビューオブジェクト
 コードやその他のテキストを表示するウィンドウは、ドキュメントビューまたはビューと呼ばれます。 エディターを作成するときに、1つのビューを選択して、1つのウィンドウにテキストを表示することができます。 複数のビューを選択して、複数のウィンドウにテキストを表示することもできます。 選択は、アプリケーションによって異なります。 たとえば、サイドバイサイド編集が必要な場合は、複数のビューを選択します。 各ビューは、ドキュメントテーブル (RDT) を実行している統合開発環境の (IDE) のエントリに関連付けられています。 ビューウィンドウは、プロジェクトまたはオブジェクトに属して <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> います。

 エディターでドキュメントデータオブジェクトの複数のビューがサポートされている場合は、ドキュメントデータオブジェクトとドキュメントビューオブジェクトが別々である必要があります。 それ以外の場合は、グループ化することができます。 詳細については、「 [複数のドキュメントビューのサポート](../extensibility/supporting-multiple-document-views.md)」を参照してください。

 IDE は、実行中のドキュメントテーブル内の各エントリの項目識別子 (ItemID) を照合することによって、イベント (たとえば、ドキュメントを含むソリューションが閉じられたとき) をビューに通知します。 詳細については、「 [document table の実行](../extensibility/internals/running-document-table.md)」を参照してください。

 カスタムエディターのビューを作成するには、2つのオプションがあります。 1つは、埋め込み先アクティブ化モデルです。このモデルでは、ActiveX コントロールまたはドキュメントデータオブジェクトを使用して、ビューがウィンドウでホストされます。 2つ目は簡略化された埋め込みモデルで、ビューはでホストされ、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> ウィンドウコマンドを処理するために実装されます。 インプレースアクティブ化モデルの詳細については、「 [インプレースアクティブ化](/previous-versions/visualstudio/visual-studio-2015/misc/in-place-activation?preserve-view=true&view=vs-2015)」を参照してください。 簡略化された埋め込みモデルについては、「簡略化された [埋め込み](../extensibility/simplified-embedding.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [複数のドキュメントビューのサポート](../extensibility/supporting-multiple-document-views.md)
- [簡略化された埋め込み](../extensibility/simplified-embedding.md)
- [方法: ドキュメントデータにビューをアタッチする](../extensibility/how-to-attach-views-to-document-data.md)
- [ドキュメントロック所有者の管理](../extensibility/document-lock-holder-management.md)
- [単一および複数のタブのビュー](../extensibility/single-and-multi-tab-views.md)
- [標準ドキュメントを保存する](../extensibility/internals/saving-a-standard-document.md)
- [永続化と実行中のドキュメントテーブル](../extensibility/internals/persistence-and-the-running-document-table.md)
- [プロジェクト内のファイルを開くエディターを決定する](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)