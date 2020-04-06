---
title: ソース管理プラグインの使用開始 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting started
- getting started, source control plug-ins
ms.assetid: 46ac1f9f-4ecc-4a72-88d3-4c7e1647e1cb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: efc21e07830614d9d3041b2d2d231fd82c652114
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708344"
---
# <a name="get-started-with-source-control-plug-ins"></a>ソース管理プラグインの使用を開始する
ソース管理プラグインを作成するには、ソース管理プラグイン API で定義された関数を実装する DLL を作成し、DLL をに登録[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]してソース コード バージョン管理で使用できるようにする必要があります。

 ソース管理プラグインには、3 つのバージョンのソース管理プラグイン API (バージョン 1.1、1.2、および 1.3) が用意されています。ここで説明するソース管理プラグイン API はバージョン 1.3 です。 バージョン 1.1 および 1.2 をサポートするソース管理プラグインと完全に互換性があるように設計されています。 [ソース管理プラグイン API バージョン 1.3 セクションの新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)では、ソース管理プラグイン API の最新バージョンでサポートされる新機能について詳しく説明します。

## <a name="in-this-section"></a>このセクションの内容
- [方法: ソース管理プラグインをインストールする](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)

 ソース管理 DLL を接続するために必要なレジストリ エントリを作成する方法について説明します。

- [ソース管理プラグイン API バージョン 1.3 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)

 バージョン 1.3 でソース管理プラグイン API に加えられた変更の概要を示します。

- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

 バージョン 1.2 でソース管理プラグイン API に加えられた変更の概要を示します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)

 ソース管理プラグイン API のすべての要素の完全な一覧を提供します。

- [ソース管理プラグインを作成する](../../extensibility/internals/creating-a-source-control-plug-in.md)

 ソース管理プラグイン SDK を定義し、含まれているリソースについて説明します。
