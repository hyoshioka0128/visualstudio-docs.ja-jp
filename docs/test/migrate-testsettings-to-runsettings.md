---
title: testsettings を runsettings に移行する
description: testsettings を runsettings に移行する方法について説明します
ms.custom: SEO-VS-2020
ms.date: 03/18/2021
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.Migrate
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ab1cfe921777fa75d4f69251668934e8d78d9bec
ms.sourcegitcommit: 155d5f0fd54ac1d20df2f5b0245365924faa3565
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2021
ms.locfileid: "106087196"
---
# <a name="upgrade-from--testsettings-to-runsettings"></a>*.testsettings* から *.runsettings* にアップグレードする

Visual Studio と共にインストールされる SettingsMigrator ツールを使用し、テスト構成ファイルを *.testsettings* から *.runsettings* にアップグレードできます。 Visual Studio のインストール場所によっては、パス `C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Extensions\TestPlatform\SettingsMigrator.exe` に設定移行ツールがあります。

正しいディレクトリの場所で、次の形式でツールを実行できます。

```console
SettingsMigrator.exe <Full path to testsettings file to be migrated>
SettingsMigrator.exe <Full path to testsettings file to be migrated> <Full path to runsettings file to be created>
```

## <a name="examples"></a>例
```console
SettingsMigrator.exe E:\MyTest\MyTestSettings.testsettings
SettingsMigrator.exe E:\MyTest\MyTestSettings.testsettings E:\MyTest\MyNewRunSettings.runsettings
```

*.testsettings* オプションが *.runsettings* に変換されるしくみについては、GitHub の[オープン ソース テスト プラットフォーム リポジトリ](https://github.com/microsoft/vstest-docs/blob/master/RFCs/0023-TestSettings-Deprecation.md#migration)に実装の詳細があります。

## <a name="see-also"></a>関連項目

- [`.runsettings` を使用してテストの実行を構成する](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
- [MSTestv1 から MSTestv2 へのアップグレード](../test/mstest-update-to-mstestv2.md)
- [コードの単体テスト](../test/unit-test-your-code.md)
- [テスト エクスプローラーを使用して単体テストをデバッグする](../test/debug-unit-tests-with-test-explorer.md)
