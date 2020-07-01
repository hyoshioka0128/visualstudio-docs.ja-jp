---
title: ShowWebBrowser コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- view.showwebbrowser
helpviewer_keywords:
- ShowWebBrowser command
- View.ShowWebBrowser command
ms.assetid: c6a4fbd6-8e9d-45cc-8b2f-93990d065e78
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8266a7c70544d8a320658fcd8b9f5ad249162fe
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769573"
---
# <a name="showwebbrowser-command"></a>ShowWebBrowser コマンド

指定した URL を統合開発環境 (IDE: Integrated Development Environment) の内部または外部の Web ブラウザーのウィンドウに表示します。

## <a name="syntax"></a>構文

```cmd
View.ShowWebBrowser URL [/new][/ext]
```

## <a name="arguments"></a>引数
`URL`

必須。 Web サイトの URL (Uniform Resource Locator)。

## <a name="switches"></a>スイッチ
/new

任意。 Web ブラウザーの新しいインスタンスにページが表示されるように指定します。

/ext

任意。 IDE の外部にある既定の Web ブラウザーにページが表示されるように指定します。

## <a name="remarks"></a>解説
**ShowWebBrowser** コマンドのエイリアスは **navigate** または **nav** です。

## <a name="example"></a>例
次の例では、IDE の外部にある Web ブラウザーに Microsoft Docs のホーム ページを表示します。 既に Web ブラウザーのページが開いている場合は、そのページを使用します。それ以外の場合は、新しいインスタンスが起動します。

```cmd
>View.ShowWebBrowser https://docs.microsoft.com /ext
```

## <a name="see-also"></a>参照

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [[コマンド] ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)