---
title: Visual Studio プロファイラー API リファレンス (ネイティブ)
description: Visual Studio プロファイラー API を使用して、収集データの量をプログラムで制御したり、タイムスタンプとプロファイルの両方のマークをプロファイル時に挿入したりする方法について学習します。
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- performance tools, API
- Profiler, API
ms.assetid: a0c3be92-c263-4678-9fb9-bafead3bd5f5
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: 9d8fe6f4f1f38277a8cf317fa55fbc883b85394a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890540"
---
# <a name="visual-studio-profiler-api-reference-native"></a>Visual Studio プロファイラー API リファレンス (ネイティブ)
Visual Studio プロファイラー API を使用すると、収集データの量をプログラムで制御したり、タイムスタンプとプロファイルの両方のマークをプロファイル時に挿入したりできます。 ネイティブ API を使用するには、*VSPerf.h* ヘッダー ファイルをインクルードし、*VSPerf.lib* をプロジェクトに追加する必要があります。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。

## <a name="in-this-section"></a>このセクションの内容
[CommentMarkAtProfile](../profiling/commentmarkatprofile.md)

[CommentMarkProfile](../profiling/commentmarkprofile.md)

[MarkProfile](../profiling/markprofile.md)

[NameProfile](../profiling/nameprofile.md)

[ResumeProfile](../profiling/resumeprofile.md)

[StartProfile](../profiling/startprofile.md)

[StopProfile](../profiling/stopprofile.md)

[SuspendProfile](../profiling/suspendprofile.md)

[PROFILE_CURRENTID](../profiling/profile-currentid.md)

## <a name="see-also"></a>関連項目

- [プロファイル ツールの API](../profiling/profiling-tools-apis.md)
- [チュートリアル: プロファイラー API の使用](../profiling/walkthrough-using-profiler-apis.md)
