---
title: Web パフォーマンス テスト エディターのカスタム HTTP ボディ エディターを作成する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, custom HTTP body editor
ms.assetid: a0b2d8ff-3e2a-487e-9172-90047174f336
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: efc9a959fa02b62583e7bf366e8c580b2876a4a1
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589202"
---
# <a name="how-to-create-a-custom-http-body-editor-for-the-web-performance-test-editor"></a>方法: Web パフォーマンス テスト エディターのカスタム HTTP ボディ エディターを作成する

カスタム コンテンツ エディターを作成して、Web サービス要求 (たとえば、SOAP、REST、asmx、wcf、RIA、その他の種類の Web サービス要求など) の文字列ボディのコンテンツまたはバイナリ ボディのコンテンツを編集できます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

次の種類のエディターを実装できます。

- **文字列コンテンツ エディター** これは <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> インターフェイスを使用して実装されます。

- **バイナリ コンテンツ エディター** これは <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> インターフェイスを使用して実装されます。

これらのインターフェイスは、<xref:Microsoft.VisualStudio.TestTools.WebTesting> 名前空間に含まれます。

## <a name="create-a-windows-control-library-project"></a>Windows コントロール ライブラリ プロジェクトの作成

1. Visual Studio で、新しい **Windows フォーム コントロール ライブラリ** プロジェクトを作成します。 プロジェクトに **MessageEditors** という名前を付けます。

   プロジェクトが新しいソリューションに追加され、*UserControl1.cs* という名前の <xref:System.Windows.Forms.UserControl> がデザイナーに表示されます。

1. **ツールボックス**の **[コモン コントロール]** カテゴリで、<xref:System.Windows.Forms.RichTextBox> を UserControl1 のサーフェイスにドラッグします。

1. <xref:System.Windows.Forms.RichTextBox> コントロールの右上隅にあるアクション タグ グリフ (![スマート タグ グリフ](../test/media/vs_winformsmttagglyph.gif)) を選び、親コンテナーを選択して**ドッキング**します。

1. **ソリューション エクスプローラー**で、Windows フォーム ライブラリ プロジェクトを右クリックし、 **[プロパティ]** を選択します。

1. **[プロパティ]** の **[アプリケーション]** タブを選択します。

1. **[対象とする Framework]** ドロップダウンの一覧で、.NET Framework 4 以降を選択します。

1. **[ターゲット フレームワークの変更]** ダイアログ ボックスが表示されます。

1. **[はい]** をクリックします。

1. **ソリューション エクスプローラー**で、 **[参照設定]** ノードを右クリックし、 **[参照の追加]** を選択します。

1. **[参照の追加]** ダイアログ ボックスが表示されます。

1. **[.NET]** タブを選びます。下にスクロールして、 **[Microsoft.VisualStudio.QualityTools.WebTestFramework]** を選択して、 **[OK]** を選びます。

1. **ソリューション エクスプローラー**で**ビュー デザイナー**がまだ開いていない場合は、**UserControl1.cs** を右クリックし、**[デザイナーの表示]** を選択します。

1. デザイン サーフェイスを右クリックし、 **[コードの表示]** を選択します。

1. (省略可能) クラスとコンストラクターの名前を、UserControl1 からわかりやすい名前 (MessageEditorControl など) に変更します。

    > [!NOTE]
    > このサンプルでは、MessageEditorControl を使用しています。

    ```csharp
    namespace MessageEditors
    {
        public partial class MessageEditorControl : UserControl
        {
            public MessageEditorControl()
            {
                InitializeComponent();
            }
        }
    }
    ```

1. 次のプロパティを追加して、RichTextBox1 のテキストを取得および設定できるようにします。 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> インターフェイスでは EditString を使用し、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> では EditByteArray を使用します。

    ```csharp
    public String EditString
    {
       get
       {
           return this.richTextBox1.Text;
       }
       set
       {
           this.richTextBox1.Text = value;
       }
    }

    public byte[] EditByteArray
    {
       get
       {
           return System.Convert.FromBase64String(richTextBox1.Text);
       }
       set
       {
           richTextBox1.Text = System.Convert.ToBase64String(value, 0, value.Length);
       }
    }
    ```

## <a name="add-a-class-to-the-windows-control-library-project"></a>Windows コントロール ライブラリ プロジェクトへのクラスの追加

プロジェクトにクラスを追加します。 このクラスは <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> インターフェイスと <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> インターフェイスの実装に使用されます。

**この手順でのコードの概要**

前の手順で作成した MessageEditorControl <xref:System.Windows.Forms.UserControl> は、messageEditorControl としてインスタンス化されます。

```csharp
private MessageEditorControl messageEditorControl
```

messageEditorControl インスタンスは、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.CreateEditor*> メソッドによって作成されたプラグイン ダイアログ内でホストされます。 また、messageEditorControl の <xref:System.Windows.Forms.RichTextBox> には、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> のコンテンツが設定されます。 ただし、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.SupportsContentType*> が `true` を返さない場合、プラグインの作成を行うことはできません。 このエディターの場合、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.SupportsContentType*> の `true` に "xml" が含まれているときは、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody.ContentType*> は <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> を返します。

文字列ボディの編集が完了し、ユーザーがプラグイン ダイアログ ボックスで **[OK]** をクリックすると、Web テスト パフォーマンス エディターでは <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.GetNewValue*> が呼び出されて、編集済みのテキストが文字列として取得され、要求の**文字列ボディ**が更新されます。

### <a name="create-a-class-and-implement-the-istringhttpbodyeditorplugin-interface"></a>クラスを作成して IStringHttpBodyEditorPlugin インターフェイスを実装する

1. **ソリューション エクスプローラー**で、Windows フォーム コントロール ライブラリ プロジェクトを右クリックし、 **[新しい項目の追加]** を選択します。

   **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. **[クラス]** を選択します。

3. **[名前]** テキスト ボックスに、クラスのわかりやすい名前 (`MessageEditorPlugins` など) を入力します。

4. **[追加]** をクリックします。

   Class1 がプロジェクトに追加され、コード エディターに表示されます。

5. コード エディターで、次の `using` ステートメントを追加します。

    ```csharp
    using Microsoft.VisualStudio.TestTools.WebTesting;
    ```

6. 次のコードを貼り付けて、インターフェイスを実装します。

    ```csharp
    /// <summary>
    /// Editor for generic text based hierarchical messages such as XML and JSON.
    /// </summary>
    public class XmlMessageEditor : IStringHttpBodyEditorPlugin
    {
        public XmlMessageEditor()
        {
        }

        /// <summary>
        /// Determine if this plugin supports the content type.
        /// </summary>
        /// <param name="contentType">The content type to test.</param>
        /// <returns>Returns true if the plugin supports the specified content type.</returns>
        public bool SupportsContentType(string contentType)
        {
            return contentType.ToLower().Contains("xml");
        }

        /// <summary>
        /// Create a UserControl to edit the specified bytes.
        /// This control will be hosted in the
        /// plugin dialog which provides OK and Cancel buttons.
        /// </summary>
        /// <param name="contentType">The content type of the BinaryHttpBody.</param>
        /// <param name="initialValue">The bytes to edit. The bytes are the payload of a BinaryHttpBody.</param>
        /// <returns>A UserControl capable of displaying and editing the byte array value of the specified content type.</returns>
        public object CreateEditor(string contentType, string initialValue)
        {
            messageEditorControl = new MessageEditorControl();
            messageEditorControl.EditString = initialValue;
            return this.messageEditorControl;
        }

        /// <summary>
        /// Gets the edited bytes after the OK button is clicked on the plugin dialog.
        /// </summary>
        public string GetNewValue()
        {
            return messageEditorControl.EditString;
        }

        private MessageEditorControl messageEditorControl;
    }
    ```

## <a name="add-a-ibinaryhttpbodyeditorplugin-to-the-class"></a>クラスへの IBinaryHttpBodyEditorPlugin の追加

<xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> インターフェイスを実装します。

**この手順でのコードの概要**

<xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> インターフェイスのコードの実装は、前の手順で説明した <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> の場合と似ています。 ただし、バイナリ バージョンではバイト配列を使用して、文字列の代わりにバイナリ データを処理します。

最初の手順で作成された MessageEditorControl <xref:System.Windows.Forms.UserControl> は、messageEditorControl としてインスタンス化されます。

```csharp
private MessageEditorControl messageEditorControl
```

messageEditorControl インスタンスは、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.CreateEditor*> メソッドによって作成されたプラグイン ダイアログ内でホストされます。 また、messageEditorControl の <xref:System.Windows.Forms.RichTextBox> には、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> のコンテンツが設定されます。 ただし、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.SupportsContentType*> が `true` を返さない場合、プラグインの作成を行うことはできません。 このエディターの場合、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.SupportsContentType*> の `true` に "msbin1" が含まれているときは、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody.ContentType*> は <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> を返します。

文字列ボディの編集が完了し、ユーザーがプラグインのダイアログ ボックスで **[OK]** をクリックすると、Web テスト パフォーマンス エディターで <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.GetNewValue*> が呼び出されて、編集済みのテキストが文字列として取得され、要求の **BinaryHttpBody.Data** が更新されます。

### <a name="to-add-the-ibinaryhttpbodyeditorplugin-to-the-class"></a>クラスに IBinaryHttpBodyEditorPlugin を追加するには

- 前の手順で追加された XmlMessageEditor クラスで次のコードを記述またはコピーして、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> インターフェイスから Msbin1MessageEditor クラスをインスタンス化し、必要なメソッドを実装します。

    ```csharp
    /// <summary>
        /// Editor for MSBin1 content type (WCF messages)
        /// </summary>
        public class Msbin1MessageEditor : IBinaryHttpBodyEditorPlugin
        {
            /// <summary>
            ///
            /// </summary>
            public Msbin1MessageEditor()
            {
            }

            /// <summary>
            /// Determine if this plugin supports a content type.
            /// </summary>
            /// <param name="contentType">The content type to test.</param>
            /// <returns>Returns true if the plugin supports the specified content type.</returns>
            public bool SupportsContentType(string contentType)
            {
                return contentType.ToLower().Contains("msbin1");
            }

            /// <summary>
            /// Create a UserControl to edit the specified bytes. This control will be hosted in the
            /// plugin dialog which provides OK and Cancel buttons.
            /// </summary>
            /// <param name="contentType">The content type of the BinaryHttpBody.</param>
            /// <param name="initialValue">The bytes to edit. The bytes are the payload of a BinaryHttpBody.</param>
            /// <returns>A UserControl capable of displaying and editing the byte array value of the specified content type.</returns>
            public object CreateEditor(string contentType, byte[] initialValue)
            {
                messageEditorControl = new MessageEditorControl();
                messageEditorControl.EditByteArray = initialValue;
                return messageEditorControl;
            }

            /// <summary>
            /// Gets the edited bytes after the OK button is clicked on the plugin dialog.
            /// </summary>
            public byte[] GetNewValue()
            {
                return messageEditorControl.EditByteArray;
            }

            private MessageEditorControl messageEditorControl;
            private object originalMessage;
        }
    ```

## <a name="build-and-deploy-the-plug-ins"></a>プラグインのビルドおよび配置

1. **[ビルド]** メニューの **[\<Windows フォーム コントロール ライブラリ プロジェクト名> のビルド]** を選びます。

2. Visual Studio のすべてのインスタンスを閉じます。

   > [!NOTE]
   > Visual Studio を閉じて、 *.dll* ファイルがコピーしようとする前にロックされていないことを確認します。

3. プロジェクトの *bin\debug* フォルダーの生成された *.dll* ファイル (*MessageEditors.dll* など) を *%ProgramFiles%\Microsoft Visual Studio\2017\\\<edition>\Common7\IDE\PrivateAssemblies\WebTestPlugins* にコピーします。

4. Visual Studio を開きます。

   *.dll* が Visual Studio に登録されるようになりました。

## <a name="verify-the-plug-ins-using-a-web-performance-test"></a>Web パフォーマンス テストによるプラグインの検証

1. テスト プロジェクトを作成します。

2. Web パフォーマンス テストを作成し、ブラウザーで Web サービスへの URL を入力します。

3. 記録が終了したら、Web パフォーマンス テスト エディターで Web サービスの要求を展開し、 **[文字列ボディ]** または **[バイナリ ボディ]** を選択します。

4. **[プロパティ]** ウィンドウで、[文字列ボディ] または [バイナリ ボディ] を選択し、省略記号 **[...]** を選択します。

   **[HTTP ボディ データの編集]** ダイアログ ボックスが表示されます。

5. ここでデータを編集できます。 **[OK]** をクリックします。 これにより、該当する GetNewValue メソッドを起動して、<xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> のコンテンツを更新できます。

## <a name="compile-the-code"></a>コードのコンパイル

Windows コントロール ライブラリ プロジェクトの対象のフレームワークが .NET Framework 4.5 であることを確認します。 既定では、Windows コントロール ライブラリ プロジェクトは .NET Framework 4.5 クライアント フレームワークを対象としますが、その場合 Microsoft.VisualStudio.QualityTools.WebTestFramework 参照を含むことは許可されません。

詳しくは、「[[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)」をご覧ください。

## <a name="see-also"></a>参照

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody>
- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.RichTextBox>
- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [方法: 要求レベルのプラグインを作成する](../test/how-to-create-a-request-level-plug-in.md)
- [Web パフォーマンス テストのカスタム抽出規則のコーディング](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
- [Web パフォーマンス テストのカスタム検証規則のコーディング](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
- [方法: ロード テスト プラグインを作成する](../test/how-to-create-a-load-test-plug-in.md)
- [コード化された Web パフォーマンス テストの生成と実行](../test/generate-and-run-a-coded-web-performance-test.md)
- [方法: Web パフォーマンス テスト結果ビューアー用に Visual Studio アドインを作成する](../test/how-to-create-an-add-in-for-the-web-performance-test-results-viewer.md)
