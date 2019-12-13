---
title: コントロールのコード化された UI テストの有効化 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 5ef1188f-89dc-413d-801d-0efdaf9b0427
caps.latest.revision: 24
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 331dabfe8e219383fdc04187482b17b9048886a9
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302577"
---
# <a name="enable-coded-ui-testing-of-your-controls"></a>コントロールのコード化された UI テストの有効化
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード化された UI テスト フレームワークのサポートを実装している場合は、コントロールをより簡単にテストできます。 サポート レベルを徐々に上げることができます。 記録と再生およびプロパティの検証のサポートから始めることができます。 この最初のサポートに加えて、コード化された UI テスト ビルダーがコントロールのカスタム プロパティを認識し、生成されたコードからそれらのプロパティにアクセスするためのカスタム クラスを提供できるようにすることができます。 また、コード化された UI テスト ビルダーが、記録される操作の目的に近い方法で操作をキャプチャできるようにすることもできます。

 **このトピックの内容:**

1. [アクセシビリティの実装によって記録と再生およびプロパティの検証をサポートする](../test/enable-coded-ui-testing-of-your-controls.md#recordandplayback)

2. [プロパティ プロバイダーの実装によってカスタム プロパティの検証をサポートする](../test/enable-coded-ui-testing-of-your-controls.md#customproprties)

3. [カスタム プロパティにアクセスするためのクラスを実装してコード生成をサポートする](../test/enable-coded-ui-testing-of-your-controls.md#codegeneration)

4. [操作フィルターの実装によって目的に応じた操作をサポートする](../test/enable-coded-ui-testing-of-your-controls.md#intentawareactions)

   ![CUIT&#95;全体](../test/media/cuit-full.png "CUIT_Full")

## <a name="recordandplayback"></a>アクセシビリティの実装によって記録と再生およびプロパティの検証をサポートする
 コード化された UI テスト ビルダーは、記録時に出現したコントロールに関する情報をキャプチャし、そのセッションを再生するコードを生成します。 コントロールがユーザー補助をサポートしていない場合、コード化された UI テスト ビルダーは画面座標を使用して操作 (マウス クリックなど) をキャプチャします。 テストの再生時、生成されたコードは同じ画面座標にそれらのマウス クリックを表示します。 テストの再生時にコントロールが画面上の別の場所に表示される場合、生成されたコードはコントロールに対するその操作の実行に失敗します。 テストが異なる画面構成や異なる環境で再生される場合、または UI レイアウトが変更された後に再生される場合、これは失敗する可能性があります。

 ![CUIT&#95;recordnosupport](../test/media/cuit-recordnosupport.png "CUIT_RecordNoSupport")

 しかし、ユーザー補助を実装している場合は、コード化された UI テスト ビルダーがテストを記録してコードを生成するときに、コントロールに関する情報をキャプチャするためにそれを使用します。 その後、テストを実行すると、コントロールがユーザー インターフェイスの別の場所にあっても、生成されたコードがコントロールに対してそれらのイベントを再生します。 テストの作成者は、コントロールの基本的なプロパティを使用してアサートを作成することもできます。

 ![CUIT&#95;レコード](../test/media/cuit-record.png "CUIT_Record")

### <a name="to-support-record-and-playback-property-validation-and-navigation-for-a-windows-forms-control"></a>Windows フォーム コントロールの記録と再生、プロパティの検証、およびナビゲーションをサポートするには
 次のプロシージャに概要を示し、<xref:System.Windows.Forms.AccessibleObject> で詳しく説明しているように、コントロールのユーザー補助を実装します。

 ![CUIT&#95;アクセス可能](../test/media/cuit-accessible.png "CUIT_Accessible")

1. <xref:System.Windows.Forms.Control.ControlAccessibleObject> から派生するクラスを実装し、クラスのオブジェクトを返すように <xref:System.Windows.Forms.Control.AccessibilityObject%2A> プロパティをオーバーライドします。

    ```csharp
    public partial class ChartControl : UserControl
    {
        // Overridden to return the custom AccessibleObject for the control.
        protected override AccessibleObject CreateAccessibilityInstance()
        {
            return new ChartControlAccessibleObject(this);
        }

        // Inner class ChartControlAccessibleObject represents accessible information
        // associated with the ChartControl and is used when recording tests.
        public class ChartControlAccessibleObject : ControlAccessibleObject
        {
            ChartControl myControl;
            public ChartControlAccessibleObject(ChartControl ctrl)
                : base(ctrl)
            {
                myControl = ctrl;
            }
        }
    }
    ```

2. アクセス可能なオブジェクトの <xref:System.Windows.Forms.AccessibleObject.Role%2A>、<xref:System.Windows.Forms.AccessibleObject.State%2A>、<xref:System.Windows.Forms.AccessibleObject.GetChild%2A>、および <xref:System.Windows.Forms.AccessibleObject.GetChildCount%2A> プロパティおよびメソッドをオーバーライドします。

3. 子コントロールの別のユーザー補助オブジェクトを実装し、そのユーザー補助オブジェクト返すように子コントロールの <xref:System.Windows.Forms.Control.AccessibilityObject%2A> プロパティをオーバーライドします。

4. 子コントロールのユーザー補助オブジェクトの <xref:System.Windows.Forms.AccessibleObject.Bounds%2A>、<xref:System.Windows.Forms.AccessibleObject.Name%2A>、<xref:System.Windows.Forms.AccessibleObject.Parent%2A>、<xref:System.Windows.Forms.AccessibleObject.Role%2A>、<xref:System.Windows.Forms.AccessibleObject.State%2A>、<xref:System.Windows.Forms.AccessibleObject.Navigate%2A>、および <xref:System.Windows.Forms.AccessibleObject.Select%2A> プロパティおよびメソッドをオーバーライドします。

> [!NOTE]
> このトピックでは、まずこのプロシージャの <xref:System.Windows.Forms.AccessibleObject> でユーザー補助のサンプルを作成し、それを基に残りのプロシージャで他の要素を作成します。 ユーザー補助サンプルの作業バージョンを作成する場合は、コンソール アプリケーションを作成し、Program.cs のコードをサンプル コードで置き換えます。 ユーザー補助、System.Drawing、および System.Windows.Forms への参照を追加する必要があります。 ビルド警告を除去するために、アクセシビリティの **[相互運用機能型の埋め込み]** を **False** に変更してください。 アプリケーションの実行時にコンソール ウィンドウが表示されないように、プロジェクトの出力の種類を **[コンソール アプリケーション]** から **[Windows アプリケーション]** に変更できます。

## <a name="customproprties"></a>プロパティ プロバイダーの実装によってカスタム プロパティの検証をサポートする
 記録と再生およびプロパティの検証の基本的なサポートを実装したら、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> プラグインを実装して、コントロールのカスタム プロパティをコード化された UI テストから使用できるようにすることができます。 たとえば、次のプロシージャでは、コード化された UI テストがグラフ コントロールの CurveLegend 子コントロールの State プロパティにアクセスできるようにするプロパティ プロバイダーを作成します。

 ![CUIT&#95;customprops](../test/media/cuit-customprops.png "CUIT_CustomProps")

### <a name="to-support-custom-property-validation"></a>カスタム プロパティの検証をサポートするには
 ![CUIT&#95;Props](../test/media/cuit-props.png "CUIT_Props")

1. 曲線の凡例のアクセス可能なオブジェクトの <xref:System.Windows.Forms.AccessibleObject.Description%2A> プロパティを、説明文字列の豊富なプロパティ値を渡すようにオーバーライドします。主要な説明とは (複数のプロパティを実装している場合はそれぞれを) セミコロン (;) で区切ります。

    ```csharp
    public class CurveLegendAccessibleObject : AccessibleObject
    {
        // add the state property value to the description
        public override string Description
        {
            get
            {
                // Add “;” and the state value to the end
                // of the curve legend’s description
                return "CurveLegend; " + State.ToString();
            }
        }
    }
    ```

2. クラス ライブラリ プロジェクトを作成し、ユーザー補助、Microsoft.VisualStudio.TestTools.UITesting、Microsoft.VisualStudio.TestTools.UITest.Common、および Microsoft.VisualStudio.TestTools.Extension への参照を追加して、コントロール用の UI テスト拡張パッケージを作成します。 アクセシビリティの **[相互運用機能型の埋め込み]** を **False** に変更します。

3. <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> から派生したプロパティのプロバイダー クラスを追加します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using Accessibility;
    using Microsoft.VisualStudio.TestTools.UITesting;
    using Microsoft.VisualStudio.TestTools.UITest.Extension;
    using Microsoft.VisualStudio.TestTools.UITesting.WinControls;
    using Microsoft.VisualStudio.TestTools.UITest.Common;

    namespace ChartControlExtensionPackage
    {
        public class ChartControlPropertyProvider : UITestPropertyProvider
        {
        }
    }
    ```

4. <xref:System.Collections.Generic.Dictionary%602> でプロパティ名とプロパティ記述子を設定して、プロパティ プロバイダーを実装します。

    ```csharp
    // Define a map of property descriptors for CurveLegend
    private static Dictionary<string, UITestPropertyDescriptor> curveLegendPropertiesMap = null;
    private static Dictionary<string, UITestPropertyDescriptor> CurveLegendPropertiesMap
    {
        get
        {
            if (curveLegendPropertiesMap == null)
            {
                UITestPropertyAttributes read =
                    UITestPropertyAttributes.Readable |
                    UITestPropertyAttributes.DoNotGenerateProperties;
                curveLegendPropertiesMap =
                    new Dictionary<string, UITestPropertyDescriptor>
                        (StringComparer.OrdinalIgnoreCase);
                curveLegendPropertiesMap.Add("State",
                    new UITestPropertyDescriptor(typeof(string), read));
            }
            return curveLegendPropertiesMap;
        }
    }

    // return the property descriptor
    public override UITestPropertyDescriptor GetPropertyDescriptor(UITestControl uiTestControl, string propertyName)
    {
        return CurveLegendPropertiesMap[propertyName];
    }

    // return the property names
    public override ICollection<string> GetPropertyNames(UITestControl uiTestControl)
    {
        if (uiTestControl.ControlType.NameEquals("Chart") || uiTestControl.ControlType.NameEquals("Text"))
        {
            // the keys of the property map are the collection of property names
            return CurveLegendPropertiesMap.Keys;
        }

        // this is not my control
        throw new NotSupportedException();
    }

    // Get the property value by parsing the accessible description
    public override object GetPropertyValue(UITestControl uiTestControl, string propertyName)
    {
        if (String.Equals(propertyName, "State", StringComparison.OrdinalIgnoreCase))
        {
            object[] native = uiTestControl.NativeElement as object[];
            IAccessible acc = native[0] as IAccessible;

            string[] descriptionTokens = acc.accDescription.Split(new char[] { ';' });
            return descriptionTokens[1];
        }

        // this is not my control
        throw new NotSupportedException();
    }
    ```

5. アセンブリがコントロールとその子コントロールにコントロール固有のサポートを提供することを示すように、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetControlSupportLevel%2A?displayProperty=fullName> をオーバーライドします。

    ```csharp
    public override int GetControlSupportLevel(UITestControl uiTestControl)
    {
        // For MSAA, check the control type
        if (string.Equals(uiTestControl.TechnologyName, "MSAA",
            StringComparison.OrdinalIgnoreCase) &&
            (uiTestControl.ControlType == "Chart"||uiTestControl.ControlType == "Text"))
        {
            return (int)ControlSupport.ControlSpecificSupport;
        }

        // This is not my control, so return NoSupport
        return (int)ControlSupport.NoSupport;
    }
    ```

6. <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider?displayProperty=fullName> の残りの抽象メソッドをオーバーライドします。

    ```csharp
    public override string[] GetPredefinedSearchProperties(Type specializedClass)
    {
        throw new NotImplementedException();
    }

    public override Type GetSpecializedClass(UITestControl uiTestControl)
    {
        throw new NotImplementedException();
    }

    public override Type GetPropertyNamesClassType(UITestControl uiTestControl)
    {
        throw new NotImplementedException();
    }

    public override void SetPropertyValue(UITestControl uiTestControl, string propertyName, object value)
    {
        throw new NotImplementedException();
    }

    public override string GetPropertyForAction(UITestControl uiTestControl, UITestAction action)
    {
        throw new NotImplementedException();
    }

    public override string[] GetPropertyForControlState(UITestControl uiTestControl, ControlStates uiState, out bool[] stateValues)
    {
        throw new NotImplementedException();
    }

    ```

7. <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> から派生した拡張パッケージ クラスを追加します。

    ```csharp
    using System;
    using Microsoft.VisualStudio.TestTools.UITesting;
    using Microsoft.VisualStudio.TestTools.UITest.Extension;
    using Microsoft.VisualStudio.TestTools.UITest.Common;

    namespace ChartControlExtensionPackage
    {
        internal class ChartControlExtensionPackage : UITestExtensionPackage
        {
        }
    }
    ```

8. アセンブリの `UITestExtensionPackage` 属性を定義します。

    ```csharp
    [assembly: Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage(
                    "ChartControlExtensionPackage",
                    typeof(ChartControlExtensionPackage.ChartControlExtensionPackage))]
    namespace ChartControlExtensionPackage
    {
       …
    ```

9. 拡張パッケージ クラスで、プロパティ プロバイダーが要求されたときにプロパティ プロバイダー クラスを返すように <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A?displayProperty=fullName> をオーバーライドします。

    ```csharp
    internal class ChartControlExtensionPackage : UITestExtensionPackage
    {
        public override object GetService(Type serviceType)
        {
            if (serviceType == typeof(UITestPropertyProvider))
            {
                if (propertyProvider == null)
                {
                    propertyProvider = new ChartControlPropertyProvider();
                }
                return propertyProvider;
            }
            return null;
        }

        private UITestPropertyProvider propertyProvider = null;
    }
    ```

10. <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> の残りの抽象メソッドと抽象プロパティをオーバーライドします。

    ```csharp

    public override void Dispose() { }

    public override string PackageDescription
    {
        get { return "Supports coded UI testing of ChartControl"; }
    }

    public override string PackageName
    {
        get { return "ChartControl Test Extension"; }
    }

    public override string PackageVendor
    {
        get { return "Microsoft (sample)"; }
    }

    public override Version PackageVersion
    {
        get { return new Version(1, 0); }
    }

    public override Version VSVersion
    {
        get { return new Version(10, 0); }
    }
    ```

11. バイナリをビルドし、 **%ProgramFiles%\Common\Microsoft Shared\VSTT\10.0\UITestExtensionPackages** にコピーします。

> [!NOTE]
> この拡張パッケージは、"Text" 型であるすべてのコントロールに適用されます。 同じ種類の複数のコントロールをテストしている場合は、別々にテストし、テストを記録するときにどの拡張パッケージが配置されているかを管理する必要があります。

## <a name="codegeneration"></a>カスタム プロパティにアクセスするためのクラスを実装してコード生成をサポートする
 コード化された UI テスト ビルダーはセッションの記録からコードを生成するとき、<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl> クラスを使用してコントロールにアクセスします。

```csharp

      UITestControl uIAText = this.UIItemWindow.UIChartControlWindow.UIAText;
Assert.AreEqual(this.AssertMethod3ExpectedValues.UIATextState, uIAText.GetProperty("State").ToString());
```

 コントロールのカスタム プロパティへのアクセスを提供するためにプロパティ プロバイダーを実装している場合は、生成されるコードが簡略化されるように、これらのプロパティへのアクセスに使用する特別なクラスを追加できます。

```csharp

      ControlLegend uIAText = this.UIItemWindow.UIChartControlWindow.UIAText;
Assert.AreEqual(this.AssertMethod3ExpectedValues.UIATextState, uIAText.State);
```

### <a name="to-add-a-specialized-class-to-access-your-control"></a>特殊なクラスを追加してコントロールにアクセスするには
 ![CUIT&#95;CodeGen](../test/media/cuit-codegen.png "CUIT_CodeGen")

1. <xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinControl> から派生したクラスを実装し、コンストラクターの検索プロパティのコレクションにコントロールの型を追加します。

    ```csharp
    public class CurveLegend:WinControl
    {
       public CurveLegend(UITestControl c) : base(c)
       {
          // The curve legend control is a “text” type of control
          SearchProperties.Add(
             UITestControl.PropertyNames.ControlType, "Text");
       }
    }
    ```

2. クラスのプロパティとして、コントロールのカスタム プロパティを実装します。

    ```csharp
    public virtual string State
    {
        get
        {
            return (string)GetProperty("State");
        }
    }
    ```

3. 曲線の凡例の子コントロールの新しいクラスの型を返すように、プロパティ プロバイダーの <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetSpecializedClass%2A?displayProperty=fullName> メソッドをオーバーライドします。

    ```csharp
    public override Type GetSpecializedClass(UITestControl uiTestControl)
    {
       if (uiTestControl.ControlType.NameEquals("Text"))
       {
          // This is text type of control. For my control,
          // that means it’s a curve legend control.
          return typeof(CurveLegend);
       }

       // this is not a curve legend control
       return null;
    }
    ```

4. 新しいクラスの PropertyNames メソッドの型を返すように、プロパティ プロバイダーの <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetPropertyNamesClassType%2A> メソッドをオーバーライドします。

    ```csharp
    public override Type GetPropertyNamesClassType(UITestControl uiTestControl)
    {
        if (uiTestControl.ControlType.NameEquals("Text"))
        {
          // This is text type of control. For my control,
          // that means it’s a curve legend control.
            return typeof(CurveLegend.PropertyNames);
        }

        // this is not a curve legend control
        return null;
    }
    ```

## <a name="intentawareactions"></a>操作フィルターの実装によって目的に応じた操作をサポートする
 Visual Studio はテストを記録するとき、各マウス イベントとキーボード イベントをキャプチャします。 ただし、一連のマウス イベントとキーボード イベントで操作の目的が失われる場合があります。 たとえば、コントロールがオートコンプリートをサポートしている場合は、テストを別の環境で再生すると、同じマウス イベントとキーボード イベントのセットで別の値になることがあります。 一連のキーボード イベントとマウス イベントを単一の操作に置き換える操作フィルター プラグインを追加できます。 こうすることで、結果として値を選択することになる一連のマウス イベントとキーボード イベントを、値を設定する単一の操作に置き換えることができます。 これによって、コード化された UI テストは環境の違いによるオートコンプリートの結果の違いから保護されます。

### <a name="to-support-intent-aware-actions"></a>目的に応じた操作をサポートするには
 ![CUIT&#95;アクション](../test/media/cuit-actions.png "CUIT_Actions")

1. [ApplyTimeout](/previous-versions/visualstudio/visual-studio-2012/dd984649%28v%3dvs.110%29)、[Category](/previous-versions/visualstudio/visual-studio-2012/dd986905(v=vs.110))、[Enabled](/previous-versions/visualstudio/visual-studio-2012/dd985633(v=vs.110))、[FilterType](/previous-versions/visualstudio/visual-studio-2012/dd778726(v=vs.110))、[Group](/previous-versions/visualstudio/visual-studio-2012/dd779219(v=vs.110))、および [Name](/previous-versions/visualstudio/visual-studio-2012/dd998334(v=vs.110)) の各プロパティをオーバーライドして、[uitestactionfilter](/previous-versions/visualstudio/visual-studio-2012/dd985757(v=vs.110))から派生したアクションフィルタークラスを実装します。

    ```csharp
    internal class MyActionFilter : UITestActionFilter
    {
       // If the user actions we are aggregating exceeds the time allowed,
       // this filter is not applied. (The timeout is configured when the
       // test is run.)
       public override bool ApplyTimeout
       {
          get { return true; }
       }

       // Gets the category of this filter. Categories of filters
       // are applied in priority order.
       public override UITestActionFilterCategory Category
       {
          get { return UITestActionFilterCategory.PostSimpleToCompoundActionConversion; }
       }

       public override bool Enabled
       {
          get { return true; }
       }

       public override UITestActionFilterType FilterType
       {
          // This action filter operates on a single action
          get { return UITestActionFilterType.Unary; }
       }

       // Gets the name of the group to which this filter belongs.
       // A group can be enabled/disabled using configuration file.
       public override string Group
       {
          get { return "ChartControlActionFilters"; }
       }

       // Gets the name of this filter.
       public override string Name
       {
          get { return "Convert Double-Click to Single-Click"; }
       }
    ```

2. `UITestActionFilter.ProcessRule` をオーバーライドします。 次の例では、ダブルクリック操作をシングルクリック操作に置き換えています。

    ```csharp
    public override bool ProcessRule(IUITestActionStack actionStack)
    {
        if (actionStack.Count > 0)
        {
            MouseAction lastAction = actionStack.Peek() as MouseAction;
            if (lastAction != null)
            {
                if (lastAction.UIElement.ControlTypeName.Equals(
                     ControlType.Text.ToString(),
                     StringComparison.OrdinalIgnoreCase))
                {
                    if(lastAction.ActionType == MouseActionType.DoubleClick)
                    {
                        // Convert to single click
                        lastAction.ActionType = MouseActionType.Click;
                    }
                }
            }
        }
        // Do not stop aggregation
        return false;
    }
    ```

3. 拡張パッケージの <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A> メソッドに操作フィルターを追加します。

    ```csharp
    public override object GetService(Type serviceType)
    {
       if (serviceType == typeof(UITestPropertyProvider))
       {
          if (propertyProvider == null)
          {
             propertyProvider = new PropertyProvider();
          }
          return propertyProvider;
       }
       else if (serviceType == typeof(UITestActionFilter))
       {
          if (actionFilter == null)
          {
             actionFilter = new RadGridViewActionFilter();
          }
          return actionFilter;
       }
       return null;
    }
    ```

4. バイナリをビルドし、%ProgramFiles%\Common Files\Microsoft Shared\VSTT\10.0\UITestExtensionPackages にコピーします。

> [!NOTE]
> 操作フィルターは、ユーザー補助の実装またはプロパティ プロバイダーに依存しません。

## <a name="debug-your-property-provider-or-action-filter"></a>プロパティ プロバイダーまたは操作フィルターをデバッグする
 プロパティ プロバイダーと操作フィルターは、アプリケーションとは別のプロセスで、コード化された UI テスト ビルダーによって読み込まれて実行される拡張パッケージで実装されます。

#### <a name="to-debug-your-property-provider-or-action-filter"></a>プロパティ プロバイダーまたは操作フィルターをデバッグするには

1. 拡張パッケージのデバッグ バージョンをビルドし、.dll ファイルと .pdb ファイルを %ProgramFiles%\Common Files\Microsoft Shared\VSTT\10.0\UITestExtensionPackages にコピーします。

2. アプリケーションを実行します (デバッガーの外部で)。

3. コード化された UI テスト ビルダーを実行します。

     `codedUITestBuilder.exe  /standalone`

4. codedUITestBuilder プロセスにデバッガーをアタッチします。

5. コード内にブレークポイントを設定します。

6. コード化された UI テスト ビルダーで、プロパティ プロバイダーを実行するためのアサートを作成し、操作フィルターを実行するための操作を記録します。

## <a name="external-resources"></a>外部リソース

### <a name="guidance"></a>ガイダンス
 Visual Studio 2012 を使用した継続的デリバリーのための [テスト–第2章:単体テスト:内部](https://go.microsoft.com/fwlink/?LinkID=255188) のテスト

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.AccessibleObject>
- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
