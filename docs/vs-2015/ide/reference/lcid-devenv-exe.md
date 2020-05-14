---
title: -LCID (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- language default
- locale IDs, setting for IDE
- Devenv, /LCID switch
- locale IDs
- /l Devenv switch
- LCID devenv switch
- /lcid Devenv switch
ms.assetid: 3a3f4e70-ea66-4351-9d62-acb1dec30e8e
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: badb88abdf4b3ffd6140cb587b2b0add20630925
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672703"
---
# <a name="lcid-devenvexe"></a>/LCID (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

統合開発環境 (IDE) 内の文字列、通貨、およびその他の値に使用する既定の言語を設定します。

## <a name="syntax"></a>構文

```
devenv {/LCID|/l} LocaleID
```

## <a name="arguments"></a>引数
 `LocaleID` 必須。 指定する言語の LCID (ロケール ID)。

## <a name="remarks"></a>解説
 IDE を読み込み、環境用の既定の自然言語を設定します。 この変更はセッション間で保持され、IDE の **[オプション]** ダイアログ ボックスにある **[環境]** オプションの **[国際対応の設定]** ウィンドウに反映されます。

 指定した言語がユーザーのシステムで使用できない場合、/LCID スイッチは無視されます。

 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] でサポートされる言語の LCID の一覧を次の表に示します。

|言語|LCID|
|--------------|----------|
|簡体中国語|2052|
|繁体中国語|1028|
|英語|1033|
|フランス語|1036|
|ドイツ語|1031|
|イタリア語|1040|
|日本語|1041|
|韓国語|1042|
|スペイン語|3082|

## <a name="example"></a>例
 この例では、英語のリソース文字列を使用して IDE を読み込みます。

```
devenv /LCID 1033
```

## <a name="see-also"></a>関連項目
 [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md)[インターナショナル設定、環境、オプションダイアログボックス](../../ide/reference/international-settings-environment-options-dialog-box.md)[ウィンドウレイアウトのカスタマイズ](../../ide/customizing-window-layouts-in-visual-studio.md)
