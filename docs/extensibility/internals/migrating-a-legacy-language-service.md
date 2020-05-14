---
title: レガシ言語サービスの移行 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, migrating
ms.assetid: e0f666a0-92a7-4f9c-ba79-d05b13fb7f11
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9e2eff3f3a27b7d8a276c8ed776c1e11d5ce332e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707108"
---
# <a name="migrating-a-legacy-language-service"></a>従来の言語サービスの移行
プロジェクトを更新し、プロジェクトに source.extension.vsixmanifest ファイルを追加することで、従来の言語サービスを新しいバージョンの Visual Studio に移行できます。 Visual Studio エディターは、それを適応させるので、言語サービス自体は、以前と同じ機能を継続します。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 言語サービスを実装する新しい方法の詳細については、「[エディターと言語サービス拡張](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="migrating-a-visual-studio-2008-language-service-solution-to-a-later-version"></a>Visual Studio 2008 言語サービス ソリューションを新しいバージョンに移行する
 次の手順では、RegExLanguageService という名前の Visual Studio 2008 サンプルを適応させる方法を示します。 このサンプルは、Visual Studio 2008 SDK のインストール先にある Visual Studio SDK の*インストール パス \VisualStudioIntegration\*サンプル\IDE\CSharp\例.RegExLanguageService\ フォルダーにあります。

> [!IMPORTANT]
> 言語サービスで色が定義されていない場合は、VSPackage で<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute.RequestStockColors%2A>明示的`true`ににに設定する必要があります。

```
[Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(YourLanguageService), YourLanguageServiceName, 0, RequestStockColors = true)]
```

#### <a name="to-migrate-a-visual-studio-2008-language-service-to-a-later-version"></a>Visual Studio 2008 言語サービスを新しいバージョンに移行するには

1. 新しいバージョンの Visual Studio と Visual Studio SDK をインストールします。 SDK をインストールする方法の詳細については、「 [Visual Studio SDK のインストール](../../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

2. ファイルを編集します (Visual Studio で読み込まずにします。

     Microsoft.VsSDK.targets ファイルを参照する`Import`ノードで、値を次のテキストに置き換えます。

    ```
    $(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\VSSDK\Microsoft.VsSDK.targets
    ```

3. ファイルを保存し、閉じます。

4. ソリューションを開きます。

5. **一方向アップグレード**ウィンドウが表示されます。 **[OK]** をクリックします。

6. プロジェクトのプロパティを更新します。 **ソリューション エクスプローラ**でプロジェクト ノードを選択し、右クリックして [プロパティ] を選択し、[**プロジェクトの****プロパティ]** ウィンドウを開きます。

    - [**アプリケーション**] タブで、[**ターゲット フレームワーク]** を **[4.6.1]** に変更します。

    - [**デバッグ**] タブの [**外部プログラムの開始**] ボックスに**\<、「Visual Studio のインストール パス>\Common7\IDE\devenv.exe」と入力します**。

         [**コマンド ライン引数**] ボックスに「 /**ルートサフィックス Exp**」と入力します。

7. 以下の参照を更新します。

    - への参照を削除し、参照を追加します。

    - への参照を削除し、への参照を追加します。

    - への参照を追加します。

8. VsPkg.csファイルを開き、属性の値を`DefaultRegistryRoot`

    ```
    "Software\\Microsoft\\VisualStudio\\14.0Exp"
    ```

9. 元のサンプルでは、その言語サービスが登録されないため、VsPkg.csに次の属性を追加する必要があります。

    ```
    [ProvideLanguageService(typeof(RegularExpressionLanguageService), "RegularExpressionLanguage", 0, RequestStockColors=true)]
    ```

10. ソース.拡張子.vsixmanifest ファイルを追加する必要があります。

    - 既存の拡張子からプロジェクト ディレクトリにこのファイルをコピーします。 このファイルを取得する方法の 1 つは、VSIX プロジェクトを作成することです ( **[ファイル]** の下の [**新規作成**] をクリックし、 **[ プロジェクト**] をクリックします。 [Visual Basic] または [C#] で [**機能拡張**] をクリックし **、[VSIX プロジェクト**] を選択します。

    - ファイルをプロジェクトに追加します。

    - ファイルの **[プロパティ]** で、[**ビルド アクション] を** **[なし]** に設定します。

    - **VSIX マニフェスト エディター**でファイルを開きます。

    - 次のフィールドを変更します。

    - **ID**: レジェックスラングサーブ

    - **製品名**: 正規表現

    - **説明**: 正規表現言語サービス。

    - [**資産**] の [**新規作成**] をクリックし、[**種類]** を選択して**Source** **[現在**の**ソリューションのプロジェクト]** を選択し、**プロジェクト**を**RegExLangServ**に設定します。

    - ファイルを保存して閉じます。

11. ソリューションをビルドします。 ビルドされたファイルは **、%USERPROFILE%\AppData\ローカル\マイクロソフト\VisualStudio\14.0Exp\拡張機能\MSIT\レジストリーラング\\サーブに**展開されます。

12. デバッグを開始します。 Visual Studio の 2 番目のインスタンスが開きました。

## <a name="see-also"></a>関連項目
- [従来の言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)
