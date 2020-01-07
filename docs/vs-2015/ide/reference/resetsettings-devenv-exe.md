---
title: -ResetSettings (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /ResetSettings switch
- ResetSettings switch
- /ResetSettings Devenv switch
ms.assetid: 1d41021c-6f58-4bd5-b122-d1c995812192
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 41e402a9268acecb70c83e26bab0e682d4ec59f5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665591"
---
# <a name="resetsettings-devenvexe"></a>/ResetSettings (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の既定の設定を復元し、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE を自動的に開始します。 指定の .vssettings ファイルに準じた設定にリセットすることもできます。

 既定の設定は、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の初回起動時に選択したプロファイルによって決定されます。

## <a name="syntax"></a>構文

```
Devenv /ResetSettings SettingsFile
```

## <a name="arguments"></a>引数
 `SettingsFile` [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] に適用する .vssettings ファイルの完全パスとファイル名です。

 全般的な開発設定のプロファイルを復元するには、`General` を使用します。

## <a name="remarks"></a>解説
 `SettingsFile` が指定されていない場合、次回 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] を起動したときに、既定の設定のコレクションを選択するよう要求されます。

## <a name="example"></a>例
 `MySettings.vssettings` ファイルに保存された設定を適用するコマンド ラインを次に示します。

```
Devenv.exe /ResetSettings "C:\My Files\MySettings.vssettings"
```

## <a name="see-also"></a>関連項目
 Visual Studio [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md)[での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)
