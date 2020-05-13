---
title: -LCID (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- language default
- locale IDs, setting for IDE
- Devenv, /L switch
- Devenv, /LCID switch
- locale IDs
- L Devenv switch
- /L Devenv switch
- LCID devenv switch
- /LCID Devenv switch
ms.assetid: 3a3f4e70-ea66-4351-9d62-acb1dec30e8e
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cabbf36adb5019543b3cfb72b0b0e56976517d2d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77557933"
---
# <a name="lcid-devenvexe"></a>/LCID (devenv.exe)

IDE 内の文字列、通貨、およびその他の値に使用する既定の言語を設定します。

## <a name="syntax"></a>構文

```shell
devenv {/LCID|/L} LocaleID
```

## <a name="arguments"></a>引数

- *LocaleID*

  必須。 指定する言語のロケール識別子 (LCID)。

## <a name="remarks"></a>解説

IDE を読み込み、環境用の既定の自然言語を設定します。 この変更はセッションが変わっても保持され、IDE の **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[国際対応の設定]**  >  **[言語]** ボックスにこの変更が表示されます。

指定した言語がシステムで利用できない場合、`/LCID` スイッチは無視されます。

Visual Studio でサポートされる言語の LCID の一覧を次の表に示します。

|言語|LCID|
|--------------|----------|
|簡体中国語|2052|
|繁体中国語|1028|
|Czech|1029|
|English|1033|
|French|1036|
|German|1031|
|Italian|1040|
|日本語|1041|
|Korean|1042|
|Polish|1045|
|ポルトガル語 (ブラジル)|1046|
|Russian|1049|
|Spanish|3082|
|Turkish|1055

## <a name="example"></a>例

この例では、英語のリソース文字列を使用して IDE を読み込みます。

```shell
devenv /LCID 1033
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
- [[国際対応の設定] ([オプション] ダイアログ ボックス - [環境])](../../ide/reference/international-settings-environment-options-dialog-box.md)
- [ウィンドウ レイアウトをカスタマイズする](../../ide/customizing-window-layouts-in-visual-studio.md)
