---
title: ヘルプ コンテンツ マネージャーのオーバーライド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-help-viewer
ms.topic: conceptual
ms.assetid: 95fe6396-276b-4ee5-b03d-faacec42765f
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 70c0044a0436dcf27a3b087b3f11a5f759824735
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645561"
---
# <a name="help-content-manager-overrides"></a>ヘルプ コンテンツ マネージャーのオーバーライド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

レジストリを変更することで、Visual Studio IDE のヘルプ ビューアーとヘルプ関連の機能の既定の動作を変更できます。

|タスク|レジストリ キー|値と定義|
|----------|------------------|--------------------------|
|一意のサービス エンドポイントを定義する|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSWinExpress\14.0\Help|NewContentAndUpdateService: *HTTPValueForTheServiceEndpoint*。|
|オンラインまたはオフラインの既定を定義する|HKEY_LOCAL_MACHINE\Software\Microsoft\VSWinExpress\14.0\help|UseOnlineHelp: ローカル ヘルプを指定するには `0`、オンライン ヘルプを指定するには `1` を入力します。|
|一意の F1 エンドポイントを定義する|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSWinExpress\14.0\Help|OnlineBaseUrl: *HTTPValueForTheServiceEndpoint*|
|Override BITS ジョブの優先順位をオーバーライドする|HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node (64-bit コンピューターの場合)\Microsoft\Help\v2.2|BITSPriority: **foreground**、**high**、**normal**、**low** のいずれかの値を使います。|
|オンライン (および IDE オンライン オプション) を無効にする|HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node (64 ビット コンピューターの場合)\Microsoft\VisualStudio\14.0\Help|OnlineHelpPreferenceDisabled: オンライン ヘルプ コンテンツへのアクセスを無効にするには 1 を設定します。|
|コンテンツの管理を無効にする|HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node (64 ビット コンピューターの場合)\Microsoft\VisualStudio\14.0\Help|ContentManagementDisabled: ヘルプ ビューアーの **[コンテンツの管理]** タブを無効にするには 1 を設定します。|
|ネットワーク共有上のローカル コンテンツ ストアを指定する|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.2\Catalogs\VisualStudio11|LocationPath="*ContentStoreNetworkShare*"|
|Visual Studio 機能の最初の起動時にコンテンツのインストールを無効にする。|HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node (64 ビット コンピューターの場合)\Microsoft\VisualStudio\14.0\Help|DisableFirstRunHelpSelection: Visual Studio の最初の開始時に構成されるヘルプ機能を無効にするには 1 を設定します。|

## <a name="see-also"></a>関連項目
 [ヘルプ ビューアーの管理者ガイド](../ide/help-viewer-administrator-guide.md)
