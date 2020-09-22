---
title: 従来の言語サービスの移行 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services, migrating
ms.assetid: e0f666a0-92a7-4f9c-ba79-d05b13fb7f11
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bc6c5d665367f2d5af9e2dd6d2a7d664e50f4830
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842088"
---
# <a name="migrating-a-legacy-language-service"></a>従来の言語サービスの移行
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

レガシ言語サービスを Visual Studio の新しいバージョンに移行するには、プロジェクトを更新し、source.extension.vsixmanifest ファイルをプロジェクトに追加します。 言語サービス自体は以前と同様に機能します。これは、Visual Studio エディターによってそれが適応されるためです。  
  
 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 言語サービスを実装する新しい方法の詳細については、「 [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。  
  
> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。  
  
## <a name="migrating-a-visual-studio-2008-language-service-solution-to-a-later-version"></a>Visual Studio 2008 言語サービスソリューションを新しいバージョンに移行する  
 次の手順では、RegExLanguageService という名前の Visual Studio 2008 サンプルを適合させる方法を示します。 このサンプルは、visual studio 2008 SDK のインストールで、 *Visual STUDIO sdk のインストールパス*\VisualStudioIntegration\Samples\IDE\CSharp\Example.RegExLanguageService\ フォルダーにあります。  
  
> [!IMPORTANT]
> 言語サービスで色が定義されていない場合は、VSPackage でを明示的にに設定する必要があり <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute.RequestStockColors%2A> `true` ます。  
  
```  
[Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(YourLanguageService), YourLanguageServiceName, 0, RequestStockColors = true)]  
```  
  
#### <a name="to-migrate-a-visual-studio-2008-language-service-to-a-later-version"></a>Visual Studio 2008 言語サービスを新しいバージョンに移行するには  
  
1. 新しいバージョンの Visual Studio と Visual Studio SDK をインストールします。 SDK のインストール方法の詳細については、「 [Visual STUDIO sdk のインストール](../../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
2. RegExLangServ ファイルを編集します (Visual Studio に読み込まれません)。  
  
     次のテキストを使用して、この `Import` ファイルを参照するノードで値をに置き換えます。  
  
    ```  
    $(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\VSSDK\Microsoft.VsSDK.targets  
    ```  
  
3. ファイルを保存して閉じます。  
  
4. RegExLangServ ソリューションを開きます。  
  
5. [ **一方向のアップグレード** ] ウィンドウが表示されます。 **[OK]** をクリックします。  
  
6. プロジェクトのプロパティを更新します。 [ **プロジェクトのプロパティ** ] ウィンドウを開くには、 **ソリューションエクスプローラー**でプロジェクトノードを選択し、右クリックして、[ **プロパティ**] を選択します。  
  
    - [ **アプリケーション** ] タブで、[ **ターゲットフレームワーク** ] を **4.6.1**に変更します。  
  
    - [**デバッグ**] タブの [**外部プログラムの開始**] ボックスに「 ** \<Visual Studio installation path>\Common7\IDE\devenv.exe**」と入力します。  
  
         [ **コマンドライン引数** ] ボックスに、「/**rootsuffix Exp**」と入力します。  
  
7. 次の参照を更新します。  
  
    - Microsoft.VisualStudio.Shell.9.0.dll への参照を削除し、Microsoft.VisualStudio.Shell.14.0.dll と Microsoft.VisualStudio.Shell.Immutable.11.0.dll への参照を追加します。  
  
    - Microsoft.VisualStudio.Package.LanguageService.9.0.dll への参照を削除し、Microsoft.VisualStudio.Package.LanguageService.14.0.dll への参照を追加します。  
  
    - Microsoft.VisualStudio.Shell.Interop.10.0.dll への参照を追加します。  
  
8. VsPkg.cs ファイルを開き、属性の値をに変更します。 `DefaultRegistryRoot`  
  
    ```  
    "Software\\Microsoft\\VisualStudio\\14.0Exp"  
    ```  
  
9. 元のサンプルでは言語サービスが登録されていないため、次の属性を VsPkg.cs に追加する必要があります。  
  
    ```  
    [ProvideLanguageService(typeof(RegularExpressionLanguageService), "RegularExpressionLanguage", 0, RequestStockColors=true)]  
    ```  
  
10. Source.extension.vsixmanifest ファイルを追加する必要があります。  
  
    - このファイルを既存の拡張機能からプロジェクトディレクトリにコピーします。 (このファイルを取得する方法の1つとして、VSIX プロジェクトを作成します ([ **ファイル**] の下にある [ **新規**] をクリックし、[ **プロジェクト**] をクリックします)。 Visual Basic または C# の [ **拡張機能**] をクリックし、[ **VSIX プロジェクト**] を選択します)。  
  
    - ファイルをプロジェクトに追加します。  
  
    - ファイルの **プロパティ**で、[ **ビルドアクション** ] を **[なし**] に設定します。  
  
    - **VSIX マニフェストエディター**を使用してファイルを開きます。  
  
    - 次のフィールドを変更します。  
  
    - **ID**: RegExLangServ  
  
    - **製品名**: RegExLangServ  
  
    - **説明**: 正規表現言語サービス。  
  
    - [ **アセット**] の下にある [ **新規**] をクリックし、[ **種類** ] を [ **VisualStudio**] に選択します。次に、[ **ソース** ] を [ **現在のソリューションのプロジェクト**] に設定し、 **プロジェクト** を [ **RegExLangServ**] に設定します。  
  
    - ファイルを保存して閉じます。  
  
11. ソリューションをビルドします。 ビルドされたファイルは **%USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0Exp\Extensions\MSIT\ RegExLangServ \\ **に配置されます。  
  
12. デバッグを開始します。 Visual Studio の2番目のインスタンスが開かれました。  
  
## <a name="see-also"></a>参照  
 [従来の言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)
