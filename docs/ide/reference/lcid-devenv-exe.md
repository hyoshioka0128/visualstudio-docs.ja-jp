---
title: -LCID (devenv.exe)
description: devenv の LCID コマンド ライン スイッチを使用して、IDE 内でテキスト、通貨、その他の値に使用する既定の言語を設定する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: eda3a4d9242655af1b018664273ceb693c7e775c
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96043986"
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

## <a name="remarks"></a>注釈

IDE を読み込み、環境用の既定の自然言語を設定します。 この変更はセッションが変わっても保持され、IDE の **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[国際対応の設定]**  >  **[言語]** ボックスにこの変更が表示されます。

指定した言語がシステムで利用できない場合、`/LCID` スイッチは無視されます。

Visual Studio でサポートされる言語の LCID の一覧を次の表に示します。

|言語|LCID|
|--------------|----------|
|簡体中国語|2052|
|繁体中国語|1028|
|チェコ語|1029|
|英語|1033|
|フランス語|1036|
|ドイツ語|1031|
|イタリア語|1040|
|日本語|1041|
|韓国語|1042|
|ポーランド語|1045|
|ポルトガル語 (ブラジル)|1046|
|ロシア語|1049|
|スペイン語|3082|
|トルコ語|1055

## <a name="example"></a>例

この例では、英語のリソース文字列を使用して IDE を読み込みます。

```shell
devenv /LCID 1033
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
- [[国際対応の設定] ([オプション] ダイアログ ボックス - [環境])](../../ide/reference/international-settings-environment-options-dialog-box.md)
- [ウィンドウ レイアウトをカスタマイズする](../../ide/customizing-window-layouts-in-visual-studio.md)
