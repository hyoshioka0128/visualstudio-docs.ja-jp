---
title: Web サーバーでは要求されたリソースを見つけられませんでした | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 21b1a97f93909a06ea9a542f83d4a4349b6f3a20
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99871248"
---
# <a name="error-the-web-server-could-not-find-the-requested-resource"></a>エラー :Web サーバーでは要求されたリソースを見つけられませんでした
セキュリティ上の考慮から、IIS が汎用エラーを返しました。

考えられる原因の 1 つは、サーバーのセキュリティ構成です。 IIS 6.0 以前のバージョンでは、URLScan と呼ばれるアドオン プログラムを使用して、不適切で疑わしい要求を除外しました。 IIS 7.0 には、同じ目的の要求フィルターが組み込まれています。 いずれの場合も、要求フィルター処理の制限が厳しすぎると Visual Studio がサーバーをデバッグできないことがあります。

このエラーの別の原因として、IIS の W3SVC サービスが開始されていないことが考えられます。 [サービス] ウィンドウ (*services.msc*) で、このサービスが開始 (淡色表示) されていることを確認します。

このエラーには、さまざまな原因が考えられます。 最も一般的な原因には、IIS のインストールまたは構成の問題、Web サイトの構成の問題、ファイル システムのアクセス許可の問題などがあります。 ブラウザーを使用してリソースへのアクセスを試すことができます。 IIS の構成方法によっては、サーバー上でローカル ブラウザーを使用したり、IIS エラー ログを検査して詳細なエラー メッセージを確認したりする必要があります。

 IIS のトラブルシューティングの詳細については、「[IIS Management and Administration (IIS の管理)](/iis/manage/provisioning-and-managing-iis/iis-management-and-administration)」を参照してください。

## <a name="see-also"></a>関連項目
- [エラー: Web サーバーが制限され、デバッグの有効化に必要な DEBUG 動詞をブロックしています](../debugger/error-the-web-server-has-been-locked-down-and-is-blocking-the-debug-verb.md)