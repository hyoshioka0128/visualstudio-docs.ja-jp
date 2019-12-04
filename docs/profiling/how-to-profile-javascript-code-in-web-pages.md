---
title: '方法: Web ページ内の JavaScript コードをプロファイリングする | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- JavaScript performance profiling
- Profiling Tools,JavaScript
- web site performance profiling
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 07c628b3c1f0be1c7ecc615dcae44f7736aa884e
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74775307"
---
# <a name="how-to-profile-javascript-code-in-web-pages"></a>方法: Web ページ内の JavaScript コードをプロファイリングする

Visual Studio プロファイル ツールは、インストルメンテーション プロファイル メソッドを使用して、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーション、任意の Web ページ、または JavaScript アプリケーションで実行する JavaScript コードのパフォーマンス データを収集できます。 Internet Explorer 8 以降が必要です。

> [!WARNING]
> UWP アプリで JavaScript をプロファイリングするには、「[JavaScript メモリ](../profiling/javascript-memory.md)」をご覧ください

プロファイル ウィザードを使用して、パフォーマンス セッションを作成できます。 インストルメンテーション メソッドを指定し、パフォーマンス セッションの [プロパティ] ダイアログ ボックスの [インストルメンテーション] ページで、JavaScript のプロファイル オプションを指定します。

JavaScript のプロファイルを指定すると、ブラウザーで実行する JavaScript コードとサーバーで実行される [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] コードのどちらもプロファイリングされます。

- [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションの場合、ブラウザーで実行される JavaScript コードとサーバーで実行される [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] コードのどちらもプロファイリングされます。

- 任意の Web ページの場合、ブラウザーで実行される JavaScript コードがプロファイリングされます。

## <a name="to-profile-javascript-in-an-aspnet-web-application-project"></a>ASP.NET Web アプリケーション プロジェクトで、JavaScript をプロファイリングするには

1. Visual Studio で [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web プロジェクトを開きます。

2. **[分析]** メニューの **[パフォーマンス ウィザードの起動]** をクリックします。

3. パフォーマンス ウィザードの最初のページで、 **インストルメンテーション** プロファイリング メソッドを指定して、 **[次へ]** をクリックします。

4. ウィザードの 2 番目のページで、ターゲットの一覧で現在のプロジェクトが選ばれていることを確認し、 **[次へ]** をクリックします。

5. ウィザードの 3 番目のページで、 **[プロファイル JavaScript]** チェック ボックスを選び、 **[次へ]** をクリックします。

6. ウィザードの 4 番目のページで、 **[完了]** をクリックして、ブラウザーで Web アプリケーションを開始します。

7. プロファイリングする機能を実行します。

8. プロファイル セッションを終了するには、ブラウザーを閉じます。

### <a name="to-profile-javascript-in-individual-web-pages-or-a-javascript-applications"></a>個々の Web ページや JavaScript アプリケーションで JavaScript をプロファイリングするには

1. Visual Studio を開きます。

2. **[分析]** メニューの **[パフォーマンス ウィザードの起動]** をクリックします。

3. パフォーマンス ウィザードの最初のページで、 **インストルメンテーション** プロファイリング メソッドを指定して、 **[次へ]** をクリックします。

4. ウィザードの 2 番目のページで、An ASP.NET、または JavaScript のアプリケーションをクリックし、 **[次へ]** をクリックします。

5. ウィザードの 3 番目のページ:

    1. **[アプリケーションを実行する URL またはパス]** ボックスのページの URL を入力します。

    2. **[プロファイル JavaScript]** チェック ボックスを選び、 **[次へ]** をクリックします。

6. ウィザードの 4 番目のページで、 **[完了]** をクリックし、ブラウザーで Web ページを開始します。

7. プロファイリングする機能を実行します。

8. プロファイル セッションを終了するには、ブラウザーを閉じます。
