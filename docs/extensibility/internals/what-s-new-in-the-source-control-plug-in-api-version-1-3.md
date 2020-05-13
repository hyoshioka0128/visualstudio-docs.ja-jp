---
title: ソース管理プラグイン API バージョン 1.3 の新機能&#39;|マイクロソフトドキュメント
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
ms.openlocfilehash: 9654f1f3ae6d4a3d73ddc3afca2977a57a98297d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703363"
---
# <a name="what39s-new-in-the-source-control-plug-in-api-version-13"></a>ソース管理プラグイン API バージョン 1.3 の新機能&#39;
ソース管理プラグイン API バージョン 1.3 では、より高度な制御を提供するために、次の新しい機能が導入されています。

## <a name="changes"></a>[変更点]
 ソース管理プラグイン API バージョン 1.3 では、次の関数が新たに追加されました。

|関数|概要|
|--------------|--------------|
|[SccGetExtendedCapabilities](../../extensibility/sccgetextendedcapabilities-function.md)|追加の機能ビットを報告可能|
|[SccEnumChangedFiles](../../extensibility/sccenumchangedfiles-function.md)|ローカル ディスク上よりもバージョン管理データベースに新しいバージョンを持つファイルを調べることができる|
|[SccQueryChanges](../../extensibility/sccquerychanges-function.md)|指定されたファイルの名前の変更 (名前変更、追加、削除) の状態を確認できます。|
|[SccPopulateDirList](../../extensibility/sccpopulatedirlist-function.md)|バージョン管理データベース内のディレクトリとファイルの検査を許可します。|
|[SccAddFilesFromSCC](../../extensibility/sccaddfilesfromscc-function.md)|バージョン管理データベースから現在のプロジェクトに、指定したファイルの一覧を追加します。|
|[SccBackgroundGet](../../extensibility/sccbackgroundget-function.md)|指定されたファイルのサイレント"Get"を実行します(ユーザーインターフェイスは表示されません)。|
|[SccGetUserOption](../../extensibility/sccgetuseroption-function.md)|ユーザー固有のオプションへのアクセスを許可します。|

## <a name="see-also"></a>関連項目
- [作業の開始](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
