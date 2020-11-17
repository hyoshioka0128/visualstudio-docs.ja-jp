---
title: Unity を使用したゲーム作成の概要
description: Unity と Visual Studio for Mac の概要
author: heiligerdankgesang
ms.author: dominicn
ms.date: 11/09/2020
ms.technology: vs-ide-general
ms.assetid: D07FA43B-9D18-4DFA-8343-CD538FAD84DB
ms.topic: how-to
ms.openlocfilehash: cae68b54623564028ea85dd1aa319fad5ceaec48
ms.sourcegitcommit: 2cf3a03044592367191b836b9d19028768141470
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94493583"
---
# <a name="getting-started-building-games-with-unity-in-visual-studio-for-mac"></a>Unity を使用した Visual Studio for Mac でのゲーム作成の概要

Unity は、C# でのゲーム開発を可能にするゲーム エンジンです。 このチュートリアルでは、Unity 環境で Visual Studio for Mac と Visual Studio for Mac Tools for Unity 拡張機能を使用して、Unity ゲームを開発およびデバッグする方法を示します。

Visual Studio for Mac Tools for Unity は無料の拡張機能であり、Visual Studio for Mac と共にインストールされます。 これを使用すると、Unity 開発者は、Visual Studio for Mac の優れた IntelliSense サポート、デバッグ機能、その他の生産性向上機能を利用できます。

## <a name="objectives"></a>目的

> [!div class="checklist"]
> * Visual Studio for Mac を使用した Unity 開発について学習する

## <a name="prerequisites"></a>必須コンポーネント

- Visual Studio for Mac ([https://www.visualstudio.com/vs/mac](https://www.visualstudio.com/vs/visual-studio-mac))
- Unity 5.6.1 Personal Edition またはそれ以降 ([https://store.unity.com](https://store.unity.com/)、実行には unity.com アカウントが必要)

## <a name="intended-audience"></a>対象読者

このラボは C# を使い慣れている開発者を対象としていますが、豊富な経験は必要ありません。

## <a name="task-1-creating-a-basic-unity-project"></a>タスク 1:基本的な Unity プロジェクトを作成する

1. **Unity** を起動します。 サインインを求められた場合は、サインインします。

2. **[新規]** をクリックします。

    ![unity の [新規] ボタン](media/unity-image1.png)

3. **[Project name]\(プロジェクト名\)** を **"UnityLab"** と設定し、 **[3D]** を選択します。 **[Create project]\(プロジェクトの作成\)** をクリックします。

    ![新しいプロジェクトの作成画面](media/unity-image2.png)

4. 既定の Unity インターフェイスが表示されます。 左側にゲーム オブジェクトを含むシーンのヒエラルキー、中央に空白のシーンの 3D ビュー、下部にプロジェクト ファイル ペイン、右側にインスペクターとサービスがあります。 もちろん、それだけではありませんが、それらはより重要なコンポーネントのうちのいくつかです。

    ![空白の unity インターフェイス](media/unity-image3.png)

5. Unity を初めて使用する開発者向けの情報として、自作のアプリ内で実行するものはすべて、**シーン** のコンテキストの中に存在します。 シーン ファイルは、現在のシーンとそのプロパティ用にプロジェクト内で使用されるリソースについての、あらゆる種類のメタデータを含む単一のファイルです。 自作のアプリをあるプラットフォーム用にパッケージ化すると、その結果としてのアプリは、1 つ以上のシーンのコレクションに、プラットフォーム依存コードを自分で追加したものになります。 プロジェクトにはシーンを必要な数だけ含めることができます。

6. 新しいシーンにはカメラと指向性ライトのみが存在します。 シーンには、何かを見えるようにするための **カメラ** と、何かを聞こえるようにするための **オーディオ リスナー** が必要です。 これらのコンポーネントを **GameObject** にアタッチします。

7. **[Hierarchy]\(ヒエラルキー\)** ペインで **[Main Camera]** を選択します。

    ![[Hierarchy]\(ヒエラルキー\) ペインで強調表示された main camera オブジェクト](media/unity-image4.png)

8. ウィンドウ右側の **[Inspector]\(インスペクター\)** ペインを選択してプロパティを確認します。 カメラのプロパティには、トランスフォーム情報、背景、プロジェクションの種類、視野角などがあります。 オーディオ リスナー コンポーネントも既定で追加されています。これは基本的に、カメラにアタッチした仮想マイクからシーンのオーディオをレンダリングするコンポーネントです。

    ![[Inspector]\(インスペクター\) ペイン](media/unity-image5.png)

9. **Directional Light** オブジェクトを選択します。 これにより、シーンにライトが提供され、シェーダーなどのコンポーネントでオブジェクトのレンダリング方法を認識できるようになります。

    ![強調表示された指向性ライト オブジェクト](media/unity-image6.png)

10. **インスペクター** を使用して、一般的なライトのプロパティ (タイプ、色、強度、シャドウ タイプなど) が含まれていることを確認します。

    ![[Inspector]\(インスペクター\) ペインでのプロパティの確認](media/unity-image7.png)

11. 重要なこととして、Unity のプロジェクトは Visual Studio for Mac のプロジェクトとは少し異なることに注意してください。 下部の **[Project]\(プロジェクト\)** タブで、**Assets** フォルダーを右クリックし、 **[Reveal in Finder]\(Finder に表示\)** を選択します。

    ![Finder で表示のコンテキスト アクション](media/unity-image8.png)

12. ご覧のように、プロジェクトには **Assets**、**Library**、**ProjectSettings**、**Temp** というフォルダーがあります。 ただし、インターフェイスに表示されているのは **Assets** フォルダーのみです。 **Library** フォルダーは、インポートしたアセットのローカル キャッシュで、アセットに関するすべてのメタデータが保持されます。 **ProjectSettings** フォルダーには、自分で構成できる設定が格納されます。 **Temp** フォルダーは、ビルド プロセス中に、Mono と Unity からの一時ファイル用に使用されます。 Visual Studio for Mac で開くことができるソリューション ファイルもあります (ここでは、**UnityLab.sln**)。

    ![Finder に表示したアセット](media/unity-image9.png)

13. **Finder** ウィンドウを閉じ、**Unity** に戻ります。

14. **Assets** フォルダーには、アート、コード、オーディオなどのすべてのアセットが格納されています。今は空ですが、プロジェクトにファイルを追加するたびに、ここに表示されます。 これは常に **Unity エディター** の最上位フォルダーです。 ただし、ファイルの追加と削除は常に Unity のインターフェイス (または Visual Studio for Mac) 経由で行い、決してファイル システムから直接行わないでください。

    ![unity の assets フォルダー](media/unity-image10.png)

15. **GameObject** は、Unity での開発の中心になります。というのは、モデル、ライト、パーティクル システムなど、ほぼすべてがそのタイプから派生されるからです。 **[GameObject]\(ゲームオブジェクト\) > [3D Object]\(3D オブジェクト\) > [Cube]** メニューを使用して、新しい **Cube** オブジェクトをシーンに追加します。

    ![シーンの cube オブジェクト](media/unity-image11.png)

16. 新しい **GameObject** のプロパティを見て、名前、タグ、レイヤー、トランスフォームが表示されていることを確認します。 これらのプロパティは、すべての **GameObject** に共通です。 さらに、メッシュ フィルター、ボックス コライダー、レンダラーなどの必要な機能を提供するために、**Cube** に複数のコンポーネントが追加されています。

    ![ゲーム オブジェクトのプロパティ](media/unity-image12.png)

17. **Cube** オブジェクトの名前を変更します。既定の **"Cube"** という名前を **"Enemy"** に変更します。 変更を保存するために、必ず **Enter** キーを押してください。 これは、作成する簡単なゲームの敵キューブになります。

    ![cube オブジェクトのプロパティの名前変更](media/unity-image13.png)

18. 上記と同じ処理を使用してシーンに **Cube** オブジェクトをもう 1 つ追加し、 **"Player"** という名前にします。

    ![2 番目の cube オブジェクトの名前変更](media/unity-image14.png)

19. さらに、プレイヤー オブジェクト **"Player"** にタグ付けします (名前フィールドのすぐ下にある **[Tag]\(タグ\)** ドロップダウン コントロールを表示します)。 これを敵のスクリプト内で使用して、プレイヤー ゲーム オブジェクトを見つけやすくします。

    ![プレイヤー オブジェクトへのタグ付け](media/unity-image15.png)

20. **シーン** ビューで、マウスを使用してプレイヤー オブジェクトを敵オブジェクトから離すように Z 軸方向に移動します。 キューブの **赤い** パネルを選択し、**青い** 線の方向にドラッグすることで、Z 軸方向に移動できます。 キューブは 3 次元空間に存在しますが、1 回 1 回のドラッグは 2 次元でしか行えないため、どの軸方向にドラッグするかは特に重要です。

    ![キューブが表示されているシーン ビュー](media/unity-image16.png)

21. キューブを下方向に、それから Z 軸に沿って右に移動します。 これにより、**インスペクター** 上の **Transform.Position** プロパティが更新されます。 ラボでの以降の手順が簡単になるように、ここに示されている位置と同じような位置にドラッグしてください。

    ![1 個のキューブを軸に沿って移動](media/unity-image17.png)

22. これで、プレイヤーを追跡するように敵のロジックを駆動するコードを追加することができます。 **[Project]\(プロジェクト\)** ウィンドウの **Assets** フォルダーを右クリックし、 **[Create]\(作成\)、[C# Script]\(C# スクリプト\)** の順に選択します。

    ![C# スクリプトのコンテキスト アクション](media/unity-image18.png)

23. その新しい C# スクリプトに **"EnemyAI"** という名前を付けます。

    ![C# スクリプト](media/unity-image19.png)

24. ゲーム オブジェクトにスクリプトをアタッチするには、新しく作成したスクリプトを **[Hierarchy]\(ヒエラルキー\)** ペインの **Enemy** オブジェクトにドラッグします。 これで、そのオブジェクトにこのスクリプトの動作が使用されます。

    ![ゲーム オブジェクトへのスクリプト追加を示す強調表示](media/unity-image20.png)

25. **[File]\(ファイル\) > [Save Scenes]\(シーンの保存\)** を選択して現在のシーンを保存します。 それに **"MyScene"** という名前を付けます。

## <a name="task-2-working-with-visual-studio-for-mac-tools-for-unity"></a>タスク 2:Visual Studio for Mac Tools for Unity を使用する

1. C# コードを編集する最良の方法は、Visual Studio for Mac を使用することです。 既定のハンドラーとして Visual Studio for Mac を使用するように Unity を構成できます。 **[Unity] > [Preferences]\(環境設定\)** を選択します。

2. **[External Tools]\(外部ツール\)** タブを選択します。 **[External Script Editor]\(外部スクリプト エディター\)** ボックスの一覧で **[Browse]\(参照\)** を選択し、 **[Applications/Visual Studio.app]** を選択します。 または、既に **[Visual Studio]** オプションがある場合は、それを選択します。

    ![基本設定の外部ツールのタブ](media/unity-image21.png)

3. これでスクリプト編集に **Visual Studio for Mac** を使用するように Unity を構成できました。 **[Unity Preferences]\(Unity の環境設定\)** ダイアログを閉じます。

    ![環境設定で Visual Studio を選択したところ](media/unity-image22.png)

4. **EnemyAI.cs** をダブルクリックして **Visual Studio for Mac** で開きます。

    ![Enemy アセットを unity で選択したところ](media/unity-image23.png)

5. Visual Studio ソリューションは、わかりやすいものです。 **Assets** フォルダー (**Finder** にあるものと同じ) と、先ほど作成した **EnemyAI.cs** スクリプトが含まれています。 より高度なプロジェクトでは、ヒエラルキーは Unity に表示されているものとは違って見えます。

    ![Visual Studio for Mac の [ソリューション] ウィンドウ](media/unity-image24.png)

6. **EnemyAI.cs** がエディターで開かれます。 スクリプトには最初、**Start** メソッドと **Update** メソッドのスタブだけが含まれています。

7. 最初の敵コードを次のコードで置き換えます。

    ```csharp
    public class EnemyAI : MonoBehaviour
    {
        public float Speed = 50;
        private Transform _playerTransform;
        private Transform _myTransform;

        void Start()
        {
            var player = GameObject.FindGameObjectWithTag("Player");
            if (!player)
            {
                Debug.LogError(
                    "Could not find the main player. Ensure it has the player tag set.");
            }
            else
            {
                _playerTransform = player.transform;
            }
            _myTransform = this.transform;
        }

        void Update()
        {
            var moveAmount = Speed * Time.deltaTime;
            _myTransform.position = Vector3.MoveTowards(_myTransform.position,
                _playerTransform.position, moveAmount);

            if (_myTransform.position == _playerTransform.position)
            {
                _myTransform.position = Vector3.back * 10;
            }
        }
    }
    ```

8. ここで定義されている簡単な敵の動作を大まかに確認します。 **Start** メソッドでは、プレイヤー オブジェクトへの (タグによる) 参照と、そのオブジェクトの **トランスフォーム** を取得します。 フレームごとに呼び出される **Update** メソッドでは、敵がプレイヤー オブジェクトに向かって移動します。 Visual Studio for Mac では、コードベースを理解しやすいようにキーワードと名前が色分けして示されます。

9. **Visual Studio for Mac** で敵のスクリプトへの変更を保存します。

## <a name="task-3-debugging-the-unity-project"></a>タスク 3:Unity プロジェクトをデバッグする

1. **Start** メソッドの最初のコード行にブレークポイントを設定します。 目的の行のエディターの余白をクリックします。その行にカーソルを置いて **F9** キーを押すこともできます。

    ![Visual Studio for Mac でのブレークポイントの設定](media/unity-image25.png)

2. **[デバッグの開始]** ボタンをクリックするか、**F5** キーを押します。 これによりプロジェクトがビルドされ、Unity にアタッチされて、デバッグできるようになります。

    ![Visual Studio for Mac の開始ボタン](media/unity-image26.png)

3. **Unity** に戻り、**実行** ボタンをクリックしてゲームを開始します。

    ![unity の実行ボタン](media/unity-image27.png)

4. ブレークポイントがヒットし、Visual Studio for Mac のデバッグ ツールを使用することができます。

    ![Visual Studio for Mac でのブレークポイントのヒット](media/unity-image28.png)

5. **[ローカル]** ウィンドウで **this** ポインターを見つけます。これは **EnemyAI** オブジェクトを参照しています。 参照を展開し、**Speed** のような関連付けられたメンバーを閲覧できることを確認します。

    ![Visual Studio for Mac の [ローカル] ウィンドウ](media/unity-image29.png)

6. 余白でブレークポイントをクリックするか、行を選択して **F9** キーを押して、追加したときと同じ方法で **Start** メソッドからブレークポイントを削除します。

    ![Visual Studio for Mac でブレークポイントをクリックし、削除する](media/unity-image30.png)

7. **F10** キーを押して最初のコード行をステップ実行します。この行では、タグをパラメーターとして使用し、**Player** ゲーム オブジェクトを検索します。

8. コード エディター ウィンドウ内でマウス カーソルを **player** 変数の上に置き、関連付けられているメンバーを表示します。 オーバーレイを展開して子プロパティを表示することもできます。

    ![Visual Studio for Mac エディターのデバッグ ウィンドウ](media/unity-image31.png)

9. **F5** キーを押すか、**実行** ボタンを押して、実行を続行します。 Unity に戻り、敵キューブが繰り返しプレイヤー キューブに近づく様子を確認します。 見えない場合は、カメラを調整する必要がある可能性があります。

    ![unity でのシーンの再生](media/unity-image32.png)

10. **Visual Studio for Mac** にまた切り替えて、**Update** メソッドの最初の行にブレークポイントを設定します。 すぐにヒットするはずです。

    ![Visual Studio for Mac でのブレークポイントの削除](media/unity-image33.png)

11. 速度が速すぎるため、アプリを再起動することなく、変更の影響をテストしたいとします。 **[自動]** または **[ローカル]** ウィンドウで **Speed** 変数を見つけ、それを **"10"** に変更して **Enter** キーを押します。

    ![[ローカル] ウィンドウでの変数の調整](media/unity-image34.png)

12. ブレークポイントを削除し、**F5** キーを押して実行を再開します。

13. **Unity** に戻り、実行中のアプリケーションを確認します。 今度は敵キューブが元の速度の 5 倍の速さで移動しています。

    ![実行中のアプリケーションが表示されている unity のウィンドウ](media/unity-image35.png)

14. もう一度 **再生** ボタンをクリックして Unity アプリを停止します。

    ![unity アプリの停止](media/unity-image36.png)

15. **Visual Studio for Mac** に戻ります。 **停止** ボタンをクリックしてデバッグ セッションを停止します。

    ![Visual Studio for Mac でのデバッグ セッションの停止](media/unity-image37.png)

## <a name="task-4-exploring-unity-features-in-visual-studio-for-mac"></a>タスク 4: Visual Studio for Mac で Unity の機能を調べる

1. Visual Studio for Mac では、コード エディター内から Unity のドキュメントに簡単にアクセスできます。 **Update** メソッド内の **Vector3** シンボル上のどこかにカーソルを置いて、**⌘ command + '** キーを押します。

    ![visual studio for mac エディターでのメソッドの選択](media/unity-image38.png)

2. **Vector3** に関するドキュメントが新しいブラウザー ウィンドウで開きます。 確認できたら、ブラウザー ウィンドウを閉じます。

    ![ブラウザー ウィンドウで開かれたドキュメント](media/unity-image39.png)

3. Visual Studio for Mac には、Unity の動作クラスを手早く作成するためのヘルパーも用意されています。 **ソリューション エクスプローラー** で **[Assets]** を右クリックし、 **[追加] > [New MonoBehaviour]\(新しい MonoBehaviour\)** を選択します。

    ![新しい monobehaviour のコンテキスト アクション](media/unity-image40.png)

4. 新しく作成されたクラスによって、**Start** メソッドと **Update** メソッドのスタブが提供されます。 **Update** メソッドの閉じ中かっこの後に、「**onmouseup**」と入力を始めます。 入力するに従い、実装しようとしているメソッドが Visual Studio の IntelliSense によってすぐに特定されることに注目してください。 表示されたオートコンプリート リストから、それを選択します。 パラメーターを含め、メソッド スタブが自動的に設定されます。

    ![Visual Studio for Mac での IntelliSense](media/unity-image41.png)

5. **OnMouseUp** メソッド内で「**base.** 」と入力すると、 呼び出しに使用できる基本メソッドがすべて表示されます。 IntelliSense ポップアップの右上隅にあるページング オプションを使用して、各関数のさまざまなオーバーロードを調べることもできます。

    ![Visual Studio for Mac でのオーバーロードの調査](media/unity-image42.png)

6. Visual Studio for Mac では、新しいシェーダーを簡単に定義することもできます。 **ソリューション エクスプローラー** で **[Assets]** を右クリックし、 **[追加] > [新しいシェーダー]** を選択します。

    ![Visual Studio for Mac での新しいシェーダーのアクション](media/unity-image43.png)

7. シェーダー ファイル形式には、読みやすく理解しやすいようにフルカラーとフォントが適用されます。

    ![構文の強調表示](media/unity-image44.png)

8. **Unity** に戻ります。 Visual Studio for Mac は同じプロジェクト システムで動作するため、どちらの場所で加えた変更も自動的に相互に同期されることがわかります。 これで、タスクに最適なツールをいつでも簡単に使用できます。

    ![unity のアセット パネル](media/unity-image45.png)

## <a name="summary"></a>まとめ

このラボでは、Unity と Visual Studio for Mac でゲームの作成を開始する方法を学習しました。 Unity の詳細については、[https://unity3d.com/learn](https://unity3d.com/learn) を参照してください。
