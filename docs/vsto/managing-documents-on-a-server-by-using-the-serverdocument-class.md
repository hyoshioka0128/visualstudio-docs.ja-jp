---
title: ServerDocument クラスを使用してサーバー上のドキュメントを管理する
description: Visual Studio Tools for Office ランタイムで ServerDocument クラスを使用して、ドキュメントレベルのカスタマイズのいくつかの側面を管理する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], managing on server
- Office documents [Office development in Visual Studio, managing on server
- ServerDocument class, managing documents on server
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 17a25ca382cfbbc762731afacaa628de616cfe1c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99879476"
---
# <a name="manage-documents-on-a-server-by-using-the-serverdocument-class"></a>ServerDocument クラスを使用してサーバー上のドキュメントを管理する
  でクラスを使用すると、 `ServerDocument` [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] Microsoft Office Word および Microsoft Office Excel がインストールされていない場合でも、ドキュメントレベルのカスタマイズのいくつかの側面を管理できます。 実行できる管理タスクは以下のとおりです。

- ドキュメントまたはブックのデータ キャッシュにあるデータへのアクセスおよびそのデータの変更。 詳細については、ドキュメントの「キャッシュされ [たデータの操作](#CachedData)」を参照してください。

- ドキュメントに関連付けられているカスタマイズ アセンブリの管理。 詳細については、「 [ドキュメントのカスタマイズの管理](#CustomizationInfo)」を参照してください。

  [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="understand-the-serverdocument-class"></a>ServerDocument クラスについて
 `ServerDocument` クラスは Office がインストールされていないコンピューターでの使用を目的としています。 したがって、このクラスは通常、Office プロジェクトではなく、コンソール プロジェクトや Windows フォーム プロジェクトなどの Office に統合されないアプリケーションで使用します。 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> *Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll* アセンブリのクラスを使用します。

 `ServerDocument` クラスは、[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] を使用して作成されたドキュメント レベルのカスタマイズの操作に使用できます。

 Visual Studio 2010 Tools for Office Runtime および .NET Framework 用の Office 拡張機能の詳細については、「 [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)」を参照してください。

> [!NOTE]
> システムのクラス (バージョン3.0 ランタイム) を使用するレガシアプリケーションがある場合は、 `ServerDocument` `Visual Studio Tools for Office` アプリケーションを `Visual Studio Tools for Office` 実行するコンピューターにシステム (バージョン3.0 ランタイム) をインストールする必要があります。 では、 `Visual Studio 2010 Tools for Office runtime` これらのアプリケーションを実行できません。

## <a name="work-with-cached-data-in-the-document"></a><a name="CachedData"></a> ドキュメント内のキャッシュされたデータを操作する
 `ServerDocument` クラスには、カスタマイズされたドキュメント内のデータ キャッシュの操作に使用できるメンバーが用意されています。 キャッシュされたデータの詳細については、「サーバー上のドキュメントの [データをキャッシュ](../vsto/caching-data.md) し、 [データにアクセス](../vsto/accessing-data-in-documents-on-the-server.md)する」を参照してください。

 次の表は、キャッシュされたデータの操作に使用できるメンバーを示しています。

|タスク|使用するメンバー|
|----------|-------------------|
|ドキュメントにデータ キャッシュがあるかどうかを確認する。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.IsCacheEnabled%2A> メソッド。|
|ドキュメント内のキャッシュされたデータにアクセスする。<br /><br /> 詳細については、「 [サーバー上のドキュメントのデータにアクセス](../vsto/accessing-data-in-documents-on-the-server.md)する」を参照してください。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> プロパティ。|

## <a name="manage-the-document-customization"></a><a name="CustomizationInfo"></a> ドキュメントのカスタマイズの管理
 `ServerDocument` クラスのメンバーを使用して、ドキュメントに関連付けられているカスタマイズ アセンブリを管理できます。 たとえば、ドキュメントのカスタマイズをプログラムによって削除し、そのドキュメントをカスタマイズから除外することもできます。

 次の表は、カスタマイズ アセンブリの管理に使用できるメンバーを示しています。

|タスク|使用するメンバー|
|----------|-------------------|
|ドキュメントがドキュメント レベルのカスタマイズの一部であるかどうかを確認する。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.GetCustomizationVersion%2A> メソッド。|
|プログラムによって実行時にカスタマイズをドキュメントにアタッチする。<br /><br /> 詳細については、「[方法: マネージコード拡張機能をドキュメントにアタッチ](../vsto/how-to-attach-managed-code-extensions-to-documents.md)する」を参照してください。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> メソッドの 1 つ。|
|プログラムによって実行時にドキュメントからカスタマイズを削除する。<br /><br /> 詳細については、「 [方法: ドキュメントからマネージコード拡張を削除する](../vsto/how-to-remove-managed-code-extensions-from-documents.md)」を参照してください。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> メソッド。|
|ドキュメントに関連付けられている配置マニフェストの URL を取得する。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.DeploymentManifestUrl%2A> プロパティ。|

## <a name="see-also"></a>関連項目
- [方法: マネージコード拡張機能をドキュメントにアタッチする](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
- [方法: マネージコード拡張をドキュメントから削除する](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [キャッシュ データ](../vsto/caching-data.md)
