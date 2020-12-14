---
title: デバッグとホスティング プロセス | Microsoft Docs
description: 2017 より以前のバージョンの Visual Studio については、デバッガーのパフォーマンスを改善し、一部のデバッガー機能にアクセスする目的でホスティング プロセスを使用します。
ms.custom: SEO-VS-2020
ms.date: 08/01/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], hosting process
- hosting process
ms.assetid: d0f0b9a6-2a6e-463d-b6ea-9518ee727933
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3b6f2650da6a83d936869d01fdc661bc9ddf8fc0
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560695"
---
# <a name="debugging-and-the-hosting-process"></a>プロセスのデバッグとホスト
Visual Studio のホスティング プロセスでは、デバッガーのパフォーマンスを向上させ、部分信頼のデバッグやデザイン時の式の評価など、新しいデバッガー機能が使用できるようになりました。 必要に応じてホスティング プロセスを無効にすることもできます。 次のセクションでは、ホスティング プロセスがある場合とない場合のデバッグの違いについて説明します。

> [!NOTE]
> Visual Studio 2017 以降では、ホスティング プロセスを使用してデバッグするオプションは不要になり、削除されました。 詳細については、「[Debugging:Visual Studio 2017 Aims To Speed Up Your Least Favorite Job (デバッグ: 最小限のお気に入りのジョブを高速化することをねらう Visual Studio 2017)](https://vslive.com/Blogs/News-and-Tips/2017/02/Debugging-Visual-Studio-2017-aims-to-speed-up-your-least-favorite-job.aspx)」を参照してください。

## <a name="partial-trust-debugging-and-click-once-security"></a>部分信頼のデバッグと ClickOnce のセキュリティ
 部分信頼のデバッグにはホスティング プロセスが必要です。 ホスティング プロセスを無効にすると、 **[プロジェクトのプロパティ]** の **[セキュリティ]** ページで部分信頼が有効になっている場合でも、部分信頼のデバッグは機能しません。 詳細については、[部分的に信頼されたアプリケーションをデバッグする](debugger-security.md)。

## <a name="design-time-expression-evaluation"></a>デザイン時の式評価
 デザイン時の式では、常にホスティング プロセスが使用されます。 **[プロジェクトのプロパティ]** でホスティング プロセスを無効にすると、クラス ライブラリ プロジェクトでデザイン時の式の評価も無効になります。 他のプロジェクトの種類では、デザイン時の式の評価は無効になりません。 代わりに、Visual Studio で実際の実行可能ファイルが起動され、ホスティング プロセスを使用せずにデザイン時の評価に使用されます。 この違いがあるため、結果も異なる可能性があります。

## <a name="appdomaincurrentdomainfriendlyname-differences"></a>AppDomain.CurrentDomain.FriendlyName の違い
 `AppDomain.CurrentDomain.FriendlyName` は、ホスティング プロセスが有効かどうかによって異なる結果を返します。 ホスティング プロセスを有効にして `AppDomain.CurrentDomain.FriendlyName` を呼び出すと、 *app_name*`.vhost.exe`が返されます。 ホスティング プロセスを無効にして呼び出した場合は、 *app_name*`.exe`が返されます。

## <a name="assemblygetcallingassemblyfullname-differences"></a>Assembly.GetCallingAssembly().FullName の違い
 `Assembly.GetCallingAssembly().FullName` は、ホスティング プロセスが有効かどうかによって異なる結果を返します。 ホスティング プロセスを有効にして `Assembly.GetCallingAssembly().FullName` を呼び出すと、 `mscorlib`が返されます。 ホスティング プロセスを無効にして `Assembly.GetCallingAssembly().FullName` を呼び出すと、アプリケーション名が返されます。

## <a name="see-also"></a>関連項目

- [方法: 部分的に信頼されたアプリケーションをデバッグする](debugger-security.md)