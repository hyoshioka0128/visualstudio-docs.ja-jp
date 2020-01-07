---
title: '方法 : ビルド イベントを指定する (Visual Basic) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- pre-build events
- events [Visual Studio], builds
- post-build events
- build events [Visual Studio]
- builds [Visual Studio], events
ms.assetid: 40dc83bf-a7c5-4a14-816a-fa0980b6e4c3
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 820f4ac8b154579664e01b12aa8146e4668cc17b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670677"
---
# <a name="how-to-specify-build-events-visual-basic"></a>方法 : ビルド イベントを指定する (Visual Basic)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Basic のビルド イベントを使用して、コンパイル処理の一部として、スクリプト、マクロ、またはその他のアクションを実行することができます。 コンパイル前のイベントはコンパイル前に発生し、ビルド後のイベントはコンパイル後に発生します。

 ビルド イベントは、**プロジェクト デザイナー**の **[コンパイル]** ページから使用可能な **[ビルド イベント]** ダイアログ ボックスで指定されます。

> [!NOTE]
> Visual Basic Express では、ビルド イベントのエントリはサポートされていません。 これは、完全な Visual Studio 製品でのみサポートされます。

## <a name="how-to-specify-pre-build-and-post-build-events"></a>ビルド前のイベントとビルド後のイベントを指定する方法

#### <a name="to-specify-a-build-event"></a>ビルド イベントを指定するには

1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[コンパイル]** タブをクリックします。

3. **[ビルド イベント]** ボタンをクリックして **[ビルド イベント]** ダイアログ ボックスを開きます。

4. ビルド前またはビルド後のアクションのコマンドライン引数を入力し、 **[OK]** をクリックします。

    > [!NOTE]
    > .bat ファイルを実行するすべてのビルド後コマンドの前に `call` ステートメントを追加します。 たとえば、`call C:\MyFile.bat` または `call C:\MyFile.bat call C:\MyFile2.bat` のようにします。

    > [!NOTE]
    > ビルド前またはビルド後イベントが正常に完了しない場合は、アクションの成功を示すゼロ (0) 以外のコードでイベント アクションを終了させて、ビルドを強制終了することができます。

## <a name="example-how-to-change-manifest-information-using-a-post-build-event"></a>例: ビルド後のイベントを使用してマニフェスト情報を変更する方法
 次の手順は、ビルド後のイベントから呼び出される .exe コマンドを使用して、アプリケーション マニフェスト (プロジェクト ディレクトリ内の .exe.manifest ファイル) 内にオペレーティング システムの最小バージョンを設定する方法を示しています。 オペレーティング システムの最小バージョンは、4.10.0.0 などの 4 つの部分に分かれた数字です。 これを行うには、次のように、コマンドでマニフェストの `<dependentOS>` セクションを変更します。

```
<dependentOS>
   <osVersionInfo>
      <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
   </osVersionInfo>
</dependentOS>
```

#### <a name="to-create-an-exe-command-to-change-the-application-manifest"></a>アプリケーション マニフェストを変更する .exe コマンドを作成するには

1. コマンド用のコンソール アプリケーションを作成します。 **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[Visual Basic]** ノードで、 **[Windows]** 、 **[コンソール アプリケーション]** テンプレートの順に選択します。 プロジェクトに `ChangeOSVersionVB` という名前を付けます。

3. Module1.vb で、ファイルの先頭にある他の `Imports` ステートメントに次の行を追加します。

   ```
   Imports System.Xml
   ```

4. `Sub Main` に次のコードを追加します。

   ```
   Sub Main()
      Dim applicationManifestPath As String
      applicationManifestPath = My.Application.CommandLineArgs(0)
      Console.WriteLine("Application Manifest Path: " & applicationManifestPath.ToString)

      'Get version name
      Dim osVersion As Version
      If My.Application.CommandLineArgs.Count >= 2 Then
         osVersion = New Version(My.Application.CommandLineArgs(1).ToString)
      Else
         Throw New ArgumentException("OS Version not specified.")
      End If
      Console.WriteLine("Desired OS Version: " & osVersion.ToString())

      Dim document As XmlDocument
      Dim namespaceManager As XmlNamespaceManager
      namespaceManager = New XmlNamespaceManager(New NameTable())
      With namespaceManager
         .AddNamespace("asmv1", "urn:schemas-microsoft-com:asm.v1")
         .AddNamespace("asmv2", "urn:schemas-microsoft-com:asm.v2")
      End With

      document = New XmlDocument()
      document.Load(applicationManifestPath)

      Dim baseXPath As String
      baseXPath = "/asmv1:assembly/asmv2:dependency/asmv2:dependentOS/asmv2:osVersionInfo/asmv2:os"

      'Change minimum required OS Version.
      Dim node As XmlNode
      node = document.SelectSingleNode(baseXPath, namespaceManager)
      node.Attributes("majorVersion").Value = osVersion.Major.ToString()
      node.Attributes("minorVersion").Value = osVersion.Minor.ToString()
      node.Attributes("buildNumber").Value = osVersion.Build.ToString()
      node.Attributes("servicePackMajor").Value = osVersion.Revision.ToString()

      document.Save(applicationManifestPath)
   End Sub
   ```

    このコマンドは 2 つの引数を受け取ります。 最初の引数はアプリケーション マニフェストへのパス (つまり、ビルド処理でマニフェストが作成されるフォルダー。通常は Projectname.publish) です。 2 番目の引数は新しいオペレーティング システムのバージョンです。

5. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

6. `C:\TEMP\ChangeOSVersionVB.exe` などのディレクトリに .exe ファイルをコピーします。

   次に、ビルド後のイベントでこのコマンドを呼び出して、アプリケーション マニフェストを変更します。

#### <a name="to-invoke-a-post-build-event-to-change-the-application-manifest"></a>ビルド後のイベントを呼び出してアプリケーション マニフェストを変更するには

1. 発行するプロジェクト用の Windows アプリケーションを作成します。 **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[Visual Basic]** ノードで、 **[Windows]** 、 **[Windows アプリケーション]** テンプレートの順に選択します。 プロジェクトに `VBWinApp` という名前を付けます。

3. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

4. プロジェクト デザイナーで、 **[発行]** ページに移動し、 **[発行場所]** を `C:\TEMP\` に設定します。

5. **[今すぐ発行]** をクリックして、プロジェクトを発行します。

     マニフェスト ファイルがビルドされ、`C:\TEMP\VBWinApp_1_0_0_0\VBWinApp.exe.manifest` に配置されます。 マニフェストを表示するには、ファイルを右クリックし、 **[プログラムから開く]** 、 **[一覧からプログラムを選択する]** 、 **[メモ帳]** の順にクリックします。

     ファイルで `<osVersionInfo>` 要素を探します。 たとえば、バージョンは次のように記述されています。

    ```
    <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
    ```

6. プロジェクト デザイナーで、 **[コンパイル]** タブに移動し、 **[ビルド イベント]** ボタンをクリックして **[ビルド イベント]** ダイアログ ボックスを開きます。

7. **[ビルド後に実行するコマンド ライン]** ボックスに次のコマンドを入力します。

     `C:\TEMP\ChangeOSVersionVB.exe "$(TargetPath).manifest" 5.1.2600.0`

     プロジェクトをビルドすると、このコマンドでアプリケーション マニフェストのオペレーティング システムの最小バージョンが 5.1.2600.0 に変更されます。

     `$(TargetPath)` マクロは、作成される実行可能ファイルの完全なパスを表します。 そのため、$(TargetPath).manifest と記述すると、bin ディレクトリに作成されるアプリケーション マニフェストが指定されます。 発行することにより、前に設定した発行場所にこのマニフェストがコピーされます。

8. プロジェクトを再び発行します。 **[発行]** ページに移動して、 **[今すぐ発行]** をクリックします。

     マニフェストを再び表示します。 マニフェストを表示するには、発行ディレクトリに移動し、ファイルを右クリックして、 **[プログラムから開く]** 、 **[一覧からプログラムを選択する]** 、 **[メモ帳]** の順にクリックします。

     これで、バージョンは次のように表示されます。

    ```
    <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" />
    ```

## <a name="see-also"></a>参照
 [コンパイルプロパティの管理](https://msdn.microsoft.com/94308881-f10f-4caf-a729-f1028e596a2c) [[コンパイル] ページ、プロジェクトデザイナー (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md) [[発行] ページ、プロジェクトデザイナーの [](../ide/reference/publish-page-project-designer.md) [ビルド前に実行するコマンドライン]/[ビルド後に実行するコマンドライン] ダイアログボックス](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)[方法: ビルドイベントを指定するC#()](../ide/how-to-specify-build-events-csharp.md)
