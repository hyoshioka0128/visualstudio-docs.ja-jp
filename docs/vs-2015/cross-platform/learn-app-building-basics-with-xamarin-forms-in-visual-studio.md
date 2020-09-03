---
title: Xamarin を使用したアプリ作成の基本事項について説明します
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: d22b5186-9e03-4e85-afc9-7cbe28522a6d
caps.latest.revision: 14
ms.author: crdun
manager: crdun
ms.openlocfilehash: 09da3bd59163cbef8b33b1d5ece732330e32eac7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75918928"
---
# <a name="learn-app-building-basics-with-xamarinforms-in-visual-studio"></a>Visual Studio での Xamarin Froms を使用したアプリ作成の基本事項
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[Setup and install](../cross-platform/setup-and-install.md) と [Verify your Xamarin environment](../cross-platform/verify-your-xamarin-environment.md)の手順を完了すると、このチュートリアルでは、Xamarin.Forms を使用して基本アプリ (下図) を構築する方法を示します。 Xamarin.Forms を使用して、すべての UI コードをポータブル クラス ライブラリ (PCL) に一度記述します。 そうすると、Xamarin では、ネイティブ UI コントロールが iOS、Android、Windows プラットフォームに対して自動的にレンダリングされます。 PCL オプションはすべてのターゲット プラットフォームでサポートされる特定の .NET API のみの使用を最も適切にサポートし、Xamarin.Forms ではプラットフォーム間で UI コードを共有できるため、この方法をお勧めします。

 ![Android、iOS、Windows Phone の天気予報アプリのサンプル](../cross-platform/media/crossplat-xamarin-formsguide-1.png "CrossPlat Xamarin フォームガイド1")

 作成するには次の作業を行います。

- [ソリューションを設定する](#solution)

- [共有データ サービス コードの記述](#dataservice)

- [共有 UI コードの記述の開始](#uicode)

- [Visual Studio Emulator for Android を使用してアプリをテストする](#test)

- [プラットフォーム間で UI をネイティブの外観で終了する](#finish)

> [!TIP]
> このプロジェクトの完全なソース コードは [GitHub の xamarin-forms-samples リポジトリ](https://github.com/xamarin/xamarin-forms-samples/tree/master/Weather)にあります。

## <a name="set-up-your-solution"></a><a name="solution"></a>ソリューションの設定
 次の手順では、共有コードの PCL と 2 つの追加された NuGet パッケージを含む Xamarin.Forms ソリューションを作成します。

1. Visual Studio では、新しい **[空のアプリケーション (Xamarin.Forms ポータブル)]** ソリューションを作成し、名前を「 **WeatherApp**」とします。 このテンプレートは、検索フィールドに「 **Xamarin.Forms** 」と入力することによって、最も簡単に見つけることができます。

     インストールされていない場合は、Xamarin をインストールするか、Visual Studio 2015 の機能を有効にする必要があります。「 [セットアップとインストール](../cross-platform/setup-and-install.md)」を参照してください。

     ![新しい空のアプリを作成する &#40;Xamarin. フォームポータブル&#41; プロジェクト](../cross-platform/media/crossplat-xamarin-formsguide-2.png "CrossPlat Xamarin フォームガイド2")

2. ソリューションを作成するために [OK] をクリックすると、いくつかの個別のプロジェクトが表示されます。

    - **WeatherApp (ポータブル)**: Xamarin.Forms を使用している共通のビジネス ロジックと UI コードを含む、プラットフォームで共有されるコードの記述先である PCL。

    - **WeatherApp.Droid**: ネイティブの Android コードを含むプロジェクト。 これは、既定のスタートアップ プロジェクトとして設定されます。

    - **WeatherApp.iOS**: ネイティブの iOS コードを含むプロジェクト。

    - **WeatherApp.UWP**: Windows 10 UWP コードを含むプロジェクト。

    - **WeatherApp.Windows (Windows 8.1)**: ネイティブの Windows 8.1 コードを含むプロジェクト。

    - **WeatherApp.WinPhone (Windows Phone 8.1)**: ネイティブの Windows Phone コードを含むプロジェクト。

    > [!NOTE]
    > 対象としていないプラットフォーム向けのプロジェクトは、自由に削除できます。 このチュートリアルでは、Android、iOS、Windows Phone 8.1 のプロジェクトを対象とします。 UWP および Windows 8.1 プロジェクトの操作は、Windows Phone 8.1 プロジェクトの操作とよく似ています。

     各ネイティブ プロジェクト内では、対応するプラットフォームのネイティブ デザイナーにアクセスでき、必要に応じてプラットフォーム固有の画面と機能を実装できます。

3. 次の方法で、ソリューション内の Xamarin.Forms NuGet パッケージを最新の安定したバージョンにアップグレードします。 新しい Xamarin ソリューションを作成するたびに、これを行うことをお勧めします。

    - **[ツール] > [NuGet パッケージ マネージャー] > [ソリューションの NuGet パッケージの管理]** の順に選択します。

    - **[更新]** タブで、 **Xamarin.Forms** の更新プログラムを確認し、ソリューション内のすべてのプロジェクトをチェックして更新します。 (注: Xamarin.Android.Support については、すべての更新をオフのままにします。)

    - **[バージョン]** フィールドを利用可能な **最新の安定した** バージョンに更新します。

    - **[更新]** をクリックします。

         ![Xamarin. Forms NuGet パッケージの更新](../cross-platform/media/crossplat-xamarin-formsguide-4.png "CrossPlat Xamarin フォームガイド4")

4. 気象データ サービスから取得した情報を処理するのに使用する **Newtonsoft.Json** と NuGet パッケージを PCL プロジェクトに追加します:

    - NuGet パッケージ マネージャー (手順 3 で開かれたままのもの) で、 **[参照]** タブを選択し、 **Newtonsoft**を検索します。

    - **Newtonsoft.Json**を選択します。

    - **WeatherApp** プロジェクト (パッケージをインストールするのに唯一必要なプロジェクト) をチェックします。

    - **[バージョン]** フィールドが **最新の安定した** バージョンに設定されていることを確認してください。

    - **[インストール]** をクリックします。

    - ![NuGet パッケージでの Newtonsoft.Jsの検索とインストール](../cross-platform/media/crossplat-xamarin-formsguide-5.png "CrossPlat Xamarin フォームガイド5")

5. 手順 4 を繰り返して、 **Microsoft.Net.Http** パッケージを検索し、インストールします。

6. ソリューションをビルドし、ビルド エラーがないことを確認します。

## <a name="write-shared-data-service-code"></a><a name="dataservice"></a> 共有データサービスコードの記述
 **WeatherApp (ポータブル)** プロジェクトは、すべてのプラットフォーム間で共有されるポータブルクラスライブラリ (PCL) のコードを記述する場所です。 PCL は、iOS、Android、Windows Phone 用のプロジェクトでビルドされたアプリ パッケージに自動的に含まれます。

 このサンプルを実行するには、最初にで無料の API キーにサインアップする必要があり [http://openweathermap.org/appid](https://openweathermap.org/appid) ます。

 次の手順では、PCL にコードを追加して、気象サービスからのデータにアクセスし、格納します。

1. **WeatherApp** プロジェクトを右クリックし、**[追加]、[クラス]** の順にクリックします。 **[新しい項目の追加]** ダイアログで、ファイルに **Weather.cs**という名前を指定します。 このクラスは、気象データ サービスからのデータを保存するときに使用します。

2. **Weather.cs** の内容全体を次のコードで置き換えます。

    ```csharp
    namespace WeatherApp
    {
        public class Weather
        {
            public string Title { get; set; }
            public string Temperature { get; set; }
            public string Wind { get; set; }
            public string Humidity { get; set; }
            public string Visibility { get; set; }
            public string Sunrise { get; set; }
            public string Sunset { get; set; }

            public Weather()
            {
                //Because labels bind to these values, set them to an empty string to
                //ensure that the label appears on all platforms by default.
                this.Title = " ";
                this.Temperature = " ";
                this.Wind = " ";
                this.Humidity = " ";
                this.Visibility = " ";
                this.Sunrise = " ";
                this.Sunset = " ";
            }
        }
    }
    ```

3. 別のクラスを **DataService.cs** という名前の PCL プロジェクトに追加します。これは、気象データ サービスからの JSON データを処理するのに使用します。

4. **DataService.cs** の内容全体を次のコードで置き換えます。

    ```csharp
    using System.Threading.Tasks;
    using Newtonsoft.Json;
    using System.Net.Http;

    namespace WeatherApp
    {
        public class DataService
        {
            public static async Task<dynamic> getDataFromService(string queryString)
            {
                HttpClient client = new HttpClient();
                var response = await client.GetAsync(queryString);

                dynamic data = null;
                if (response != null)
                {
                    string json = response.Content.ReadAsStringAsync().Result;
                    data = JsonConvert.DeserializeObject(json);
                }

                return data;
            }
        }
    }
    ```

5. 3 番目のクラスを、 **Core** という名前の PCL に追加します。ここには、郵便番号を使用してクエリ文字列を生成し、気象データ サービスを呼び出した後に、 **Weather** クラスのインスタンスを取り込むロジックなどの共有ビジネス ロジックを配置します。

6. **Core.cs** の内容を次のコードで置き換えます。

    ```csharp
    using System;
    using System.Threading.Tasks;

    namespace WeatherApp
    {
        public class Core
        {
            public static async Task<Weather> GetWeather(string zipCode)
            {
                //Sign up for a free API key at http://openweathermap.org/appid
                string key = "YOUR KEY HERE";
                string queryString = "http://api.openweathermap.org/data/2.5/weather?zip="
                    + zipCode + ",us&appid=" + key + "&units=imperial";

                dynamic results = await DataService.getDataFromService(queryString).ConfigureAwait(false);

                if (results["weather"] != null)
                {
                    Weather weather = new Weather();
                    weather.Title = (string)results["name"];
                    weather.Temperature = (string)results["main"]["temp"] + " F";
                    weather.Wind = (string)results["wind"]["speed"] + " mph";
                    weather.Humidity = (string)results["main"]["humidity"] + " %";
                    weather.Visibility = (string)results["weather"][0]["main"];

                    DateTime time = new System.DateTime(1970, 1, 1, 0, 0, 0, 0);
                    DateTime sunrise = time.AddSeconds((double)results["sys"]["sunrise"]);
                    DateTime sunset = time.AddSeconds((double)results["sys"]["sunset"]);
                    weather.Sunrise = sunrise.ToString() + " UTC";
                    weather.Sunset = sunset.ToString() + " UTC";
                    return weather;
                }
                else
                {
                    return null;
                }
            }
        }
    }
    ```

7. **WeatherApp** PCL プロジェクトをビルドし、コードが正しいことを確認します。

## <a name="begin-writing-shared-ui-code"></a><a name="uicode"></a> 共有 UI コードの記述を開始します
 Xamarin.Forms を使用すると、共有 UI コードを PCL に実装できます。 次の手順では、前のセクションで追加した気象データ サービス コードで返されたデータによってボタンのテキストが更新され、そのボタンを使用して PCL に画面を追加します。

1. **WeatherApp**プロジェクトを右クリックし、[**新しい項目の追加 >**] を選択して、 **WeatherPage.cs**という名前の**フォーム Xaml ページ**を追加します。[**新しい項目の追加**] ダイアログで、"フォーム" を検索し、[**フォーム Xaml**の選択] ページに**WeatherPage.cs**という名前を指定します。

     Xamarin.Forms は XAML ベースのため、この手順では、入れ子にされた分離コード ファイル **WeatherPage.xaml.cs** と共に **WeatherPage.xaml**ファイルを作成します。 これにより、XAML またはコードで UI を生成することができます。 このチュートリアルでは、両方の一部を実行します。

     ![新しい Xamarin. Forms XAML ページの追加](../cross-platform/media/crossplat-xamarin-formsguide-6.png "CrossPlat Xamarin フォームガイド6")

2. WeatherPage 画面にボタンを追加するには、WeatherPage.xaml の内容を次のコードで置き換えます。

    ```xaml
    <?xml version="1.0" encoding="utf-8" ?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
           xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
           x:Class="WeatherApp.WeatherPage">
      <Button x:Name="getWeatherBtn" Text="Get Weather"/>
    </ContentPage>
    ```

     ボタンの名前は **x:Name** 属性を使用して定義する必要があることに注意してください。そうすると、分離コード ファイルでこのボタンを名前で参照することができます。

3. ボタンの **Clicked** イベントにイベント ハンドラーを追加してボタン テキストを更新するには、 **WeatherPage.xaml.cs** の内容を次のコードで置き換えます。 (自由に “60601” を別の郵便番号に変更することができます。)

    ```csharp
    using System;
    using Xamarin.Forms;

    namespace WeatherApp
    {
        public partial class WeatherPage: ContentPage
        {
            public WeatherPage()
            {
                InitializeComponent();
                this.Title = "Sample Weather App";
                getWeatherBtn.Clicked += GetWeatherBtn_Clicked;

                //Set the default binding to a default object for now
                this.BindingContext = new Weather();
            }

            private async void GetWeatherBtn_Clicked(object sender, EventArgs e)
            {
                Weather weather = await Core.GetWeather("60601");
                getWeatherBtn.Text = weather.Title;
            }
        }
    }
    ```

4. アプリの起動時に **WeatherPage** を最初の画面として開くには、 **App.cs** の既定のコンストラクターを次のコードで置き換えます。

    ```csharp
    public App()
    {
        MainPage = new NavigationPage(new WeatherPage());
    }
    ```

5. WeatherApp PCL プロジェクトをビルドし、コードが正しいことを確認します。

## <a name="test-your-app-using-the-visual-studio-emulator-for-android"></a><a name="test"></a>Visual Studio Emulator for Android を使用してアプリをテストする
 これで、アプリを実行する準備ができました。 アプリが気象サービスからデータを取得していることを確認するには、今回は Android バージョンのみを実行します。 さらに UI 要素を追加した後で、iOS と Windows Phone のバージョンも実行します。 (注: Windows 7 で Visual Studio を実行している場合は、これらと同じ手順を実行しますが、Xamarin Player が代わりに実行します。)

1. **WeatherApp.Droid** プロジェクトをスタートアップ プロジェクトに設定するには、そのプロジェクトを右クリックし、 **[スタートアップ プロジェクトに設定]** を選択します。

2. Visual Studio ツールバーには、 **WeatherApp.Droid** がターゲット プロジェクトとして一覧表示されます。 デバッグ用の Android エミュレーターの 1 つを選択し、 **F5**キーをクリックします。 Visual Studio Emulator for Android でアプリを実行するための **VS Emulator** オプションの 1 つを使用することをお勧めします。

     ![VS Emulator デバッグターゲットの選択](../cross-platform/media/crossplat-xamarin-formsguide-7.png "CrossPlat Xamarin フォームガイド7")

3. エミュレーターでアプリが起動されたら、 **[Get Weather]** ボタンをクリックします。 ボタンのテキストが **Chicago, IL**に更新されました。データの *Title* プロパティは気象サービスから取得されたものです。

     ![ボタンをタップする前と後の Weather アプリ](../cross-platform/media/crossplat-xamarin-formsguide-8.png "CrossPlat Xamarin フォームガイド8")

## <a name="finish-the-ui-with-a-native-look-and-feel-across-platforms"></a><a name="finish"></a> プラットフォーム間でネイティブのルックアンドフィールを使用して UI を完成させる
 Xamarin.Forms は各プラットフォームのネイティブ UI コントロールをレンダリングして、アプリが自動的にネイティブな外観を持つようにします。 これをさらに見やすくするには、郵便番号用の入力フィールドで UI を終了し、サービスから返された気象データを表示します。

1. **WeatherPage.xaml** の内容を次のコードで置き換えます。 すべての要素は、前述のとおり **x:Name** 属性を使用して名前を付けられ、それらの要素がコードから参照できるようになっていることに注意してください。 Xamarin.Forms は、さまざまな [レイアウト オプション](/xamarin/xamarin-forms/user-interface/controls/layouts) (xamarin.com) も提供します。ここで、WeatherPage は [StackLayout](/dotnet/api/Xamarin.Forms.StackLayout?view=xamarin-forms) (xamarin.com) を使用しています。

   ```xaml
   <?xml version="1.0" encoding="utf-8" ?>
   <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
          xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
          x:Class="WeatherApp.WeatherPage">

     <ContentPage.Resources>
       <ResourceDictionary>
         <Style x:Key="labelStyle" TargetType="Label">
           <Setter Property="TextColor" Value="#a8a8a8" />
           <Setter Property="FontSize" Value="Small" />
         </Style>
         <Style x:Key="fieldStyle" TargetType="Label">
           <Setter Property="TextColor">
             <OnPlatform x:TypeArguments="Color" iOS="Black" Android="White" WinPhone="White" />
           </Setter>
           <Setter Property="FontSize" Value="Medium" />
         </Style>
         <Style x:Key="fieldView" TargetType="ContentView">
           <Setter Property="Padding" Value="10,0,0,0" />
         </Style>
       </ResourceDictionary>
     </ContentPage.Resources>

     <ContentPage.Content>
       <ScrollView>
         <StackLayout>
           <StackLayout Orientation="Horizontal" HorizontalOptions="FillAndExpand"
                 BackgroundColor="#545454">
             <StackLayout Padding="10,10,10,10" HorizontalOptions="Start">
               <Label Text="Search by Zip Code" TextColor="White" FontAttributes="Bold"
                   FontSize="Medium" />
               <Label x:Name="zipCodeLabel" Text="Zip Code" Style="{StaticResource labelStyle}" />
               <Entry x:Name="zipCodeEntry" />
             </StackLayout>
             <StackLayout Padding="0,0,0,10" VerticalOptions="End">
               <Button x:Name="getWeatherBtn" Text="Get Weather" WidthRequest="185" BorderWidth="1" >
                 <!-- Set iOS colors; use defaults on other platforms -->
                 <Button.TextColor>
                   <OnPlatform x:TypeArguments="Color" iOS="White"/>
                 </Button.TextColor>
                 <Button.BorderColor>
                   <OnPlatform x:TypeArguments="Color" iOS="White"/>
                 </Button.BorderColor>
               </Button>
             </StackLayout>
           </StackLayout>
           <StackLayout Padding="10,10,10,10" HorizontalOptions="Start">
             <Label Text="Location" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label Text="{Binding Title}" Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Temperature" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="tempLabel" Text="{Binding Temperature}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Wind Speed" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="windLabel" Text="{Binding Wind}" Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Humidity" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="humidityLabel" Text="{Binding Humidity}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Visibility" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="visibilitylabel" Text="{Binding Visibility}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Time of Sunrise" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="sunriseLabel" Text="{Binding Sunrise}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Time of Sunset" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="sunsetLabel" Text="{Binding Sunset}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
           </StackLayout>
         </StackLayout>
       </ScrollView>
     </ContentPage.Content>
   </ContentPage>
   ```

    Xamarin.Forms の **OnPlatform** タグの使用に注意してください。 **OnPlatform** により、アプリが実行されている現在のプラットフォーム固有のプロパティ値が選択されます ( [外部 XAML 構文](/xamarin/xamarin-forms/xaml/xaml-basics/essential-xaml-syntax) (xamarin.com) をご覧ください)。 このタグは、個々のデータ フィールドにテキストの色を設定するために使用します。Android と Windows Phone には白、iOS には黒を指定します。 **OnPlatform** を任意のプロパティおよび任意のデータ型に対して使用し、プラットフォーム固有の調整を XAML の任意の場所に行うことができます。 分離コード ファイルで、 [Device.OnPlatform API](/xamarin/xamarin-forms/platform/device) を同じ目的のために使用することができます。

2. **WeatherPage.xaml.cs**で、 **GetWeatherBtn_Clicked** イベント ハンドラーを次のコードで置き換えます。 このコードは、入力フィールドに郵便番号があることを確認し、その郵便番号のデータを取得し、全画面のバインド コンテキストを結果の Weather インスタンスに設定してから、ボタン テキストを “再検索” に設定します。 UI の各ラベルが Weather クラスのプロパティにバインドされるため、画面のバインド コンテキストを **Weather** インスタンスに設定すると、それらのラベルが自動的に更新されることに注意してください。

   ```csharp
   private async void GetWeatherBtn_Clicked(object sender, EventArgs e)
   {
       if (!String.IsNullOrEmpty(zipCodeEntry.Text))
       {
           Weather weather = await Core.GetWeather(zipCodeEntry.Text);
           this.BindingContext = weather;
           getWeatherBtn.Text = "Search Again";
       }
   }
   ```

3. 適切なプロジェクトを右クリックし、[スタートアップ プロジェクトに設定] を選択し、デバイスまたはエミュレーターかシミュレーターのいずれかでアプリを開始して、3 つのすべてのプラットフォーム (Android、iOS、Windows Phone) 上でアプリを実行します。 有効な米国の郵便番号 (60601 など) を入力し、[Get Weather] ボタンを押してその地域の気象データを次のように表示します。 iOS プロジェクトのネットワーク上で Visual Studio が Mac OS X コンピューターに接続されている必要があります。

    ![Android、iOS、Windows Phone の天気予報アプリのサンプル](../cross-platform/media/crossplat-xamarin-formsguide-1.png "CrossPlat Xamarin フォームガイド1")

   このプロジェクトの完全なソース コードは [GitHub の xamarin-forms-samples リポジトリ](https://github.com/xamarin/xamarin-forms-samples/tree/master/Weather)にあります。
