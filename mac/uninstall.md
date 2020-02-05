---
title: Visual Studio for Mac をアンインストールする
description: Visual Studio for Mac と関連ツールをアンインストールする方法を説明します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.technology: vs-ide-install
ms.assetid: 4EB95F75-BC2E-4982-9564-2975805712D8
ms.openlocfilehash: 348a6ad1bde58c17b2bbb1ef4868fcfa6835ef9f
ms.sourcegitcommit: 6375001ab26786af8d4d449f5846f8a49779ed18
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2020
ms.locfileid: "76892169"
---
# <a name="uninstalling-visual-studio-for-mac"></a>Visual Studio for Mac のアンインストール

このガイドを使用すると、関連するセクションに移動することで、Visual Studio for Mac の各コンポーネントを個別にアンインストールすることができます。または、「[アンインストール スクリプト](#uninstall-script)」で示されるスクリプトを使用して、すべてをアンインストールすることができます。

> [!NOTE]
> この情報で扱われているのは、ご利用のコンピューターからの Visual Studio 2019 for Mac または Visual Studio 2017 for Mac の削除のみです。 Visual Studio Code をアンインストールする場合、詳細については[こちらのイシュー](https://github.com/Microsoft/vscode/issues/52151)を参照してください。

## <a name="uninstall-script"></a>アンインストール スクリプト

Visual Studio for Mac とご利用のコンピューター用のコンポーネントをすべてアンインストールするために使用できるスクリプトが 2 つあります。

- [Visual Studio と Xamarin スクリプト](#visual-studio-for-mac-and-xamarin-script)
- [.NET Core スクリプト](#net-core-script)

次のセクションでは、スクリプトのダウンロードと使用に関する情報が示されます。

### <a name="visual-studio-for-mac-and-xamarin-script"></a>Visual Studio for Mac と Xamarin スクリプト

[アンインストール スクリプト](https://raw.githubusercontent.com/MicrosoftDocs/visualstudio-docs/master/mac/resources/uninstall-vsmac.sh)を使うと、Visual Studio と Xamarin コンポーネントを一度にアンインストールできます。

このアンインストール スクリプトには、この記事で説明されているほとんどのコマンドが含まれます。 外部依存関係の可能性のためにスクリプトからは次の 3 つが除外されています。 これを削除するには、以下の関連セクションにジャンプして手動で削除してください。

- **[Mono のアンインストール](#uninstall-mono-sdk-mdk)**
- **[Android AVD のアンインストール](#uninstall-android-avd)**
- **[Android SDK と Java SDK をアンインストールする](#uninstall-android-sdk-and-java-sdk)**

スクリプトを実行するには、次の手順のようにします。

1. スクリプトを右クリックして **[名前を付けて保存]** を選び、ご利用の Mac 上にファイルを保存します。
2. ターミナルを開き、スクリプトをダウンロードした場所に作業ディレクトリを変更します。

    ```bash
    cd /location/of/file
    ```

3. スクリプトを実行可能にして、**sudo** で実行します。

    ```bash
    chmod +x ./uninstall-vsmac.sh
    sudo ./uninstall-vsmac.sh
    ```

4. 最後に、アンインストール スクリプトを削除し、ドックから Visual Studio for Mac を削除します (ある場合)。

### <a name="net-core-script"></a>.NET Core スクリプト

.NET Core 用のアンインストール スクリプトは、[dotnet cli repo](https://raw.githubusercontent.com/dotnet/cli/master/scripts/obtain/uninstall/dotnet-uninstall-pkgs.sh) にあります。

スクリプトを実行するには、次の手順のようにします。

1. スクリプトを右クリックして **[名前を付けて保存]** を選び、ご利用の Mac 上にファイルを保存します。
2. ターミナルを開き、スクリプトをダウンロードした場所に作業ディレクトリを変更します。

    ```bash
    cd /location/of/file
    ```

3. スクリプトを実行可能にして、**sudo** で実行します。

    ```bash
    chmod +x ./dotnet-uninstall-pkgs.sh
    sudo ./dotnet-uninstall-pkgs.sh
    ```

4. 最後に、.NET Core のアンインストール スクリプトを削除します。

## <a name="uninstall-visual-studio-for-mac"></a>Visual Studio for Mac をアンインストールする

Mac から Visual Studio をアンインストールするときは最初に、 **/Applications** ディレクトリで **Visual Studio.app** を探して、それを**ごみ箱**にドラッグします。 または、次の図のように、右クリックして **[ごみ箱に移動]** を選びます。

![Visual Studio アプリケーションをごみ箱に移動する](media/uninstall-image1.png)

このアプリ バンドルを削除すると、Visual Studio for Mac は削除されますが、Xamarin 関連の他のファイルがファイル システムにまだ残っている可能性があります。

Visual Studio for Mac のすべてのトレースを削除するには、ターミナルで次のコマンドを実行します。

```bash
sudo rm -rf "/Applications/Visual Studio.app"
rm -rf ~/Library/Caches/VisualStudio
rm -rf ~/Library/Preferences/VisualStudio
rm -rf ~/Library/Preferences/Visual\ Studio
rm -rf ~/Library/Logs/VisualStudio
rm -rf ~/Library/VisualStudio
rm -rf ~/Library/Preferences/Xamarin/
rm -rf ~/Library/Application\ Support/VisualStudio
rm -rf ~/Library/Application\ Support/VisualStudio/7.0/LocalInstall/Addins/
rm -rf ~/Library/Application\ Support/VisualStudio/8.0/LocalInstall/Addins/
```

Xamarin のさまざまなファイルやフォルダーを含む次のディレクトリを削除することもできます。 ただし、実行する前に、このディレクトリに Android の署名キーが含まれていることに注意してください。 詳細については、セクション「 **[Android SDK と Java SDK をアンインストールする](#uninstall-android-sdk-and-java-sdk)** 」を参照してください。

```bash
rm -rf ~/Library/Developer/Xamarin
```

## <a name="uninstall-mono-sdk-mdk"></a>Mono SDK (MDK) をアンインストールする

Mono は Microsoft .NET Framework のオープン ソースの実装であり、すべての Xamarin 製品 (Xamarin.iOS、Xamarin.Android、Xamarin.Mac) によって、C# でこれらのプラットフォームの開発を可能にするために使われています。

> [!WARNING]
> Visual Studio for Mac 以外にも Mono を使うアプリケーションがあります (Unity など)。
> Mono をアンインストールする前に、Mono に依存するアプリケーションが他にないことを確認してください。

Mono Framework をコンピューターから削除するには、ターミナルで次のコマンドを実行します。

```bash
sudo rm -rf /Library/Frameworks/Mono.framework
sudo pkgutil --forget com.xamarin.mono-MDK.pkg
sudo rm -rf /etc/paths.d/mono-commands
```

## <a name="uninstall-xamarinandroid"></a>Xamarin.Android をアンインストールする

Xamarin.Android をインストールして使うために必要なものがいくつかあります (Android SDK や Java SDK など)。

Xamarin.Android を削除するには、次のコマンドを使います。

```bash
sudo rm -rf /Developer/MonoDroid
rm -rf ~/Library/MonoAndroid
sudo pkgutil --forget com.xamarin.android.pkg
sudo rm -rf /Library/Frameworks/Xamarin.Android.framework
```

### <a name="uninstall-android-sdk-and-java-sdk"></a>Android SDK と Java SDK をアンインストールする

Android アプリケーションの開発には Android SDK が必要です。 Android SDK のすべての部分を完全に削除するには、 **~/Library/Developer/Xamarin/** でファイルを探して、**ごみ箱**に移動します。

> [!WARNING]
> Visual Studio for Mac によって生成された Android の署名キーは `~/Library/Developer/Xamarin/Keystore` 内にあります。 キーストアを残しておきたい場合は、これらを適切にバックアップするか、このディレクトリを削除しないでください。

Java SDK (JDK) は Mac OS X/macOS の一部として既にあらかじめパッケージ化されているので、アンインストールする必要はありません。

### <a name="uninstall-android-avd"></a>Android AVD をアンインストールする

> [!WARNING]
> Android Studio など、Visual Studio for Mac 以外にも Android AVD とこれらの追加 Android コンポーネントを使うアプリケーションがあります。このディレクトリを削除すると、Android Studio のプロジェクトが中断される可能性があります。

Android AVD および追加 Android コンポーネントを削除するには、次のコマンドを使います。

```bash
rm -rf ~/.android
```

Android AVD のみを削除するには、次のコマンドを使います。

```bash
rm -rf ~/.android/avd
```

## <a name="uninstall-xamarinios"></a>Xamarin.iOS をアンインストールする

Xamarin.iOS により、Visual Studio for Mac で C# または F# を使って iOS アプリケーションを開発できます。

ターミナルで次のコマンドを使って、ファイル システムからすべての Xamarin.iOS ファイルを削除します。

```bash
rm -rf ~/Library/MonoTouch
sudo rm -rf /Library/Frameworks/Xamarin.iOS.framework
sudo rm -rf /Developer/MonoTouch
sudo pkgutil --forget com.xamarin.monotouch.pkg
sudo pkgutil --forget com.xamarin.xamarin-ios-build-host.pkg
sudo pkgutil --forget com.xamarin.xamarin.ios.pkg
```

## <a name="uninstall-xamarinmac"></a>Xamarin.Mac をアンインストールする

次の 2 つのコマンドを使って Mac から製品とライセンスを除去することにより、コンピューターから Xamarin.Mac を削除できます。

```bash
sudo rm -rf /Library/Frameworks/Xamarin.Mac.framework
rm -rf ~/Library/Xamarin.Mac
```

## <a name="uninstall-workbooks-and-inspector"></a>Workbooks と Inspector をアンインストールする

1\.2.2 以降では、ターミナルで次のコマンドを実行して、Xamarin Workbooks と Inspector をアンインストールできます。

```bash
sudo /Library/Frameworks/Xamarin.Interactive.framework/Versions/Current/uninstall
```

古いバージョンでは、次の成果物を手動で削除する必要があります。

* `"/Applications/Xamarin Workbooks.app"` の Workbooks アプリを削除します
* `"Applications/Xamarin Inspector.app"` の Inspector アプリを削除します
* アドイン `"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Interactive"` と `"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Inspector"` を削除します
* `/Library/Frameworks/Xamarin.Interactive.framework` および `/Library/Frameworks/Xamarin.Inspector.framework` にある Inspector のファイルとサポート ファイルを削除します

## <a name="uninstall-the-xamarin-profiler"></a>Xamarin Profiler をアンインストールする

```bash
sudo rm -rf "/Applications/Xamarin Profiler.app"
```

## <a name="uninstall-the-visual-studio-installer"></a>Visual Studio インストーラーをアンインストールする

次のコマンドを使って、Xamarin Universal Installer のすべてのトレースを削除します。

```bash
rm -rf ~/Library/Caches/XamarinInstaller/
rm -rf ~/Library/Caches/VisualStudioInstaller/
rm -rf ~/Library/Logs/XamarinInstaller/
rm -rf ~/Library/Logs/VisualStudioInstaller/
rm -rf ~/Library/Preferences/Xamarin/
rm -rf "~/Library/Preferences/Visual Studio/"
```

* * * 





## <a name="uninstall-visual-studio-2019-for-mac-preview"></a>Visual Studio 2019 for Mac プレビューをアンインストールする

Visual Studio 2019 for Mac プレビューは、独立したプレビューとして提供されており、サイドバイサイド Visual Studio 2017 for Mac インストールを引き続き使用できます。

Visual Studio 2019 for Mac がリリースされたので、Visual Studio 2019 for Mac プレビュー アプリケーションを安全に削除できます。

プレビュー アプリケーション バンドルをアンインストールするには、次の図に示すように、**アプリケーション** フォルダーで **[Visual Studio (プレビュー)]** を選択し、 **[ごみ箱に移動]** をクリックします。

![ファインダーで [ごみ箱に移動] オプションを選択](media/uninstall-remove-vspreview.png)

また、次のコマンドを使用してプレビューの plist ファイルを削除することもできます。

```bash
rm -rf ~/Library/Preferences/com.microsoft.visual-studio-preview.plist
```

## <a name="see-also"></a>関連項目

- [Visual Studio のアンインストール (Windows)](/visualstudio/install/uninstall-visual-studio)