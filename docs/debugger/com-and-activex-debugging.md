---
title: COM および ActiveX のデバッグ | Microsoft Docs
description: Visual Studio での、COM アプリケーションと ActiveX コントロールのデバッグに関するヒントを紹介します。 COM サーバーと COM コンテナーのデバッグについて説明します。 COM 用のデバッグ ツールをまとめています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.com
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- COM, debugging
- debugging ActiveX applications
- debugging [Visual Studio], COM
- debugging COM containers
- ActiveX controls, debugging
ms.assetid: 3260b2a7-3239-493d-9271-aedf705c13c7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f86f072a32bf9d7ff4af3c77564236fe2997f70a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99865866"
---
# <a name="com-and-activex-debugging"></a>COM および ActiveX のデバッグ
ここでは、COM アプリケーションと ActiveX コントロールのデバッグに関するヒントを紹介します。

## <a name="in-this-section"></a>このセクションの内容
 [COM サーバーとコンテナーのデバッグ](../debugger/com-server-and-container-debugging.md) COM アプリケーションをデバッグするときに特に考慮が必要な事項を説明します。 同じソリューション内の 2 つのプロジェクトを使った COM サーバーおよびコンテナーのデバッグ、プロセス間をまたぐ呼び出しのトレース、コールバック関数でのブレークポイントの設定、コンテナーとサーバー間のステップ実行などの問題を扱います。

 [方法: ActiveX コントロールのデバッグ](../debugger/how-to-debug-an-activex-control.md) ActiveX コントロールのデバッグについて説明します。 デバッグ セッションでコンテナーを指定して ActiveX コントロール内のコードの実行状況を見る方法、データ連結 ActiveX コントロールのデバッグ、特定のコンテナーのシミュレート、コンテナーのコードのステップ実行などを扱います。

 [COM デバッグ ツール](../debugger/com-debugging-tools.md) COM アプリケーションのデバッグに使用できるビューアーおよびサンプル アプリケーションを紹介します。

## <a name="related-sections"></a>関連項目
 [デバッガーでのはじめに](../debugger/debugger-feature-tour.md): デバッグ ドキュメントの重要なセクションへのリンクを提供します。 デバッガーの新機能、設定と準備、ブレークポイント、例外の処理、エディット コンティニュ、マネージド コードのデバッグ、C++ プロジェクトのデバッグ、COM および ActiveX のデバッグ、DLL のデバッグ、SQL のデバッグ、ユーザー インターフェイス リファレンスなどの情報へのリンクを提供します。

## <a name="see-also"></a>関連項目

- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [COM の概要](/cpp/atl/introduction-to-com)
- [ActiveX コントロール](/cpp/mfc/activex-controls)
- [SDI サーバー アプリケーション](com-server-and-container-debugging.md)