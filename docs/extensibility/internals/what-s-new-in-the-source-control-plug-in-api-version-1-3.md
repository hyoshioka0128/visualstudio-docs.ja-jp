---
title: '&apos;ソース管理プラグイン API 1.3 の新機能'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, what's new in API v1.3
- what's new [Visual Studio SDK], source control plug-ins
ms.assetid: 7dfb2227-6e1d-4028-bce9-f8967456a993
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0eb580d018bbb858cd0214970bdba3d4ab4f391c
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89741536"
---
# <a name="what39s-new-in-the-source-control-plug-in-api-version-13"></a>ソース管理プラグイン API バージョン1.3 の新機能&#39;
ソース管理プラグイン API バージョン1.3 では、より高度なコントロールを提供するために次の新しい関数が導入されています。

## <a name="changes"></a>[変更点]
 ソース管理プラグイン API バージョン1.3 では、次の関数が新しく追加されています。

|機能|概要|
|--------------|--------------|
|[SccGetExtendedCapabilities](../../extensibility/sccgetextendedcapabilities-function.md)|追加の機能ビットを報告できるようにします|
|[SccEnumChangedFiles](../../extensibility/sccenumchangedfiles-function.md)|バージョン管理データベースにローカルディスクよりも新しいバージョンがあるファイルを調べることができます。|
|[SccQueryChanges](../../extensibility/sccquerychanges-function.md)|指定されたファイルの名前変更 (名前の変更、追加、削除) の状態を調べることができます。|
|[SccPopulateDirList](../../extensibility/sccpopulatedirlist-function.md)|バージョン管理データベース内のディレクトリとファイルを調べることができます。|
|[SccAddFilesFromSCC](../../extensibility/sccaddfilesfromscc-function.md)|バージョン管理データベースから現在のプロジェクトに、指定したファイルの一覧を追加します。|
|[SccBackgroundGet](../../extensibility/sccbackgroundget-function.md)|指定されたファイルのサイレントな "Get" を実行します (ユーザーインターフェイスは表示されません)|
|[SccGetUserOption](../../extensibility/sccgetuseroption-function.md)|ユーザー固有のオプションへのアクセスを許可します|

## <a name="see-also"></a>関連項目
- [はじめに](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
