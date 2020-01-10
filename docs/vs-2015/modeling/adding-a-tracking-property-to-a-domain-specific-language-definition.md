---
title: ドメイン固有言語の定義への追跡プロパティの追加 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- tracking properties [Domain-Specific Language Tools], walkthrough
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools]
ms.assetid: 4aa47777-de75-4897-a423-a3c4426b4125
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1e98a5902495528082a8328befe724c91f01a3d0
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75852398"
---
# <a name="adding-a-tracking-property-to-a-domain-specific-language-definition"></a>ドメイン固有言語の定義への追跡プロパティの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、ドメインモデルに追跡プロパティを追加する方法について説明します。

 *追跡ドメイン*プロパティは、ユーザーが更新できるが、他のドメインプロパティまたは要素の値を使用して計算される既定値を持つプロパティです。

 たとえば、ドメイン固有言語ツール (DSL ツール) では、ドメインクラスの "表示名" プロパティには、ドメインクラスの名前を使用して計算される既定値がありますが、ユーザーはデザイン時に値を変更するか、計算値にリセットすることができます。

 このチュートリアルでは、モデルの "既定の名前空間" プロパティに基づいて既定値を持つ名前空間追跡プロパティを持つ、ドメイン固有言語 (DSL) を作成します。 追跡プロパティの詳細については、「[追跡プロパティの定義](https://msdn.microsoft.com/0538b0e4-6221-4e7d-911a-b92cd622f0be)」を参照してください。

- DSL ツールは、プロパティ記述子の追跡をサポートしています。 ただし、DSL デザイナーを使用して、追跡プロパティを言語に追加することはできません。 したがって、追跡プロパティを定義および実装するには、カスタムコードを追加する必要があります。

  追跡プロパティには、ユーザーによる追跡と更新の2つの状態があります。 追跡プロパティには、次の機能があります。

- 追跡状態の場合は、追跡プロパティの値が計算され、モデルの他のプロパティが変更されたときに値が更新されます。

- [ユーザーによる更新] 状態の場合、追跡プロパティの値には、ユーザーが最後にプロパティを設定した値が保持されます。

- **プロパティ** ウィンドウでは、プロパティが 更新者 の状態にある場合にのみ、tracking プロパティの**Reset**コマンドが有効になります。 **Reset**コマンドは、tracking プロパティの状態を tracking に設定します。

- **プロパティ** ウィンドウで、tracking プロパティが 追跡中 の状態になっている場合は、その値が通常のフォントで表示されます。

- **プロパティ** ウィンドウで、tracking プロパティが ユーザーによる更新 状態になっている場合、その値が太字のフォントで表示されます。

## <a name="prerequisites"></a>[前提条件]
 このチュートリアルを開始するには、まず次のコンポーネントをインストールする必要があります。

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185579](https://www.visualstudio.com/)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185580](https://docs.microsoft.com/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts)|
|[!INCLUDE[dsl](../includes/dsl-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185581](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)|

## <a name="creating-the-dsl-project"></a>DSL プロジェクトの作成
 ドメイン固有言語のプロジェクトを作成します。

#### <a name="to-create-the-project"></a>プロジェクトを作成するには

1. ドメイン固有言語デザイナープロジェクトを作成します。 これに `TrackingPropertyDSL` という名前を付けます。

2. **ドメイン固有言語デザイナーウィザード**で、次のオプションを設定します。

    1. **MinimalLanguage**テンプレートを選択します。

    2. ドメイン固有言語の既定の名前、`TrackingPropertyDSL`を使用します。

    3. モデルファイルの拡張子を `trackingPropertyDsl`に設定します。

    4. モデルファイルの既定のテンプレートアイコンを使用します。

    5. 製品の名前を `Product Name`に設定します。

    6. 会社の名前を `Company Name`に設定します。

    7. ソリューション内のプロジェクトのルート名前空間の既定値である `CompanyName.ProductName.TrackingPropertyDSL`を使用します。

    8. アセンブリの厳密な名前のキーファイルをウィザードで作成できるようにします。

    9. ソリューションの詳細を確認し、 **[完了]** をクリックして DSL 定義プロジェクトを作成します。

## <a name="customizing-the-default-dsl-definition"></a>既定の DSL 定義のカスタマイズ
 このセクションでは、DSL 定義を次の項目を含むようにカスタマイズします。

- モデルのすべての要素の名前空間追跡プロパティ。

- モデルのすべての要素に対するブール型の IsNamespaceTracking プロパティ。 このプロパティは、追跡プロパティが追跡状態であるか、またはユーザーによって更新された状態であるかを示します。

- モデルの既定の名前空間プロパティ。 このプロパティは、名前空間の追跡プロパティの既定値を計算するために使用されます。

- モデルの CustomElements 計算されるプロパティです。 このプロパティは、カスタム名前空間を持つ要素の比率を示します。

#### <a name="to-add-the-domain-properties"></a>ドメインのプロパティを追加するには

1. DSL デザイナーで、 **examplemodel.store**ドメインクラスを右クリックし、 **[追加]** をポイントして、 **[domainproperty]** をクリックします。

    1. 新しいプロパティに `DefaultNamespace`という名前を指定します。

    2. 新しいプロパティの **プロパティ** ウィンドウで、**既定値** を `DefaultNamespace`に設定し、**型** を **文字列** に設定します。

2. **Examplemodel.store**ドメインクラスに、`CustomElements`という名前のドメインプロパティを追加します。

     新しいプロパティの **[プロパティ]** ウィンドウで、 **[種類]** を **[計算]** 済み に設定します。

3. 例と**して、** `Namespace`という名前のドメインプロパティを追加します。

     新しいプロパティの **[プロパティ]** ウィンドウで、[参照可能 **] を [** **False**] に設定し、 **[種類]** を **[customstorage]** に設定します。

4. 例と**して、** `IsNamespaceTracking`という名前のドメインプロパティを追加します。

     新しいプロパティの **[プロパティ]** ウィンドウで、[参照可能 **] を** **False**に設定し、 **[既定値]** を `true`に設定し、 **[型]** を **[ブール]** に設定します。

#### <a name="to-update-the-diagram-elements-and-dsl-details"></a>図の要素と DSL の詳細を更新するには

1. DSL デザイナーで、 **ExampleShape** geometry 図形を右クリックし、 **[追加]** をポイントして、 **[テキストデコレータ]** をクリックします。

    1. 新しいテキストのデコレータ `NamespaceDecorator`という名前を指定します。

    2. テキストデコレータの **[プロパティ]** ウィンドウで、 **[位置]** を **[inner左下]** に設定します。

2. DSL デザイナーで、 **ExampleShape**図形に対して、[例]**要素**クラスを接続する線を選択します。

    1. DSL の**詳細**ウィンドウで、 **[デコレータマップ]** タブを選択します。

    2. **[デコレーター]** ボックスの一覧で **[NamespaceDecorator]** を選択し、チェックボックスをオンにして、 **[表示プロパティ]** の一覧で **[名前空間]** を選択します。

3. **DSL エクスプローラー**で、 **[ドメインクラス]** フォルダーを展開し、 **[オブジェクト]** の種類 ノードを右クリックして、 **[新しいドメイン型記述子の追加]** をクリックします。

    1. [例]**要素**ノードを展開し、 **[カスタム型記述子 (ドメイン型記述子)]** ノードを選択します。

    2. ドメイン型記述子の **[プロパティ]** ウィンドウで、 **[カスタムコード]** を **[True]** に設定します。

4. **DSL エクスプローラー**で、 **[Xml シリアル化の動作]** ノードを選択します。

    1. **[プロパティ]** ウィンドウで、 **[カスタムポストロード]** を**True**に設定します。

## <a name="transforming-templates"></a>テンプレートの変換
 DSL のドメインクラスとプロパティを定義したので、DSL 定義を正しく変換してプロジェクトのコードを再生成できることを確認できます。

#### <a name="to-transform-the-text-templates"></a>テキストテンプレートを変換するには

1. **ソリューションエクスプローラー**ツールバーで、 **[すべてのテンプレートの変換]** をクリックします。

2. システムによってソリューションのコードが再生成され、DslDefinition が保存されます。 定義ファイルの XML 形式の詳細については、「 [DslDefinition. Dsl ファイル](../modeling/the-dsldefinition-dsl-file.md)」を参照してください。

## <a name="creating-files-for-custom-code"></a>作成 (カスタムコードのファイルを)
 すべてのテンプレートを変換すると、Dsl および DslPackage プロジェクトでドメイン固有言語を定義するソースコードがシステムによって生成されます。 生成されたテキストに干渉しないようにするには、生成されたコードファイルとは別のファイルにカスタムコードを記述します。

 追跡プロパティの値と状態を維持するためのコードを指定する必要があります。 生成されたコードからカスタムコードを区別し、ファイル名の競合を回避するために、カスタムコードファイルを別のサブフォルダーに配置します。

#### <a name="to-create-the-code-files"></a>コードファイルを作成するには

1. **ソリューションエクスプローラー**で、 **DSL**プロジェクトを右クリックし、 **[追加]** をポイントして、 **[新しいフォルダー]** をクリックします。 新しいフォルダーに `CustomCode`という名前を指定します。

2. 新しい**Customcode**フォルダーを右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。

3. **コードファイル**テンプレートを選択し、**名前**を `NamespaceTrackingProperty.cs`に設定して、[ **OK]** をクリックします。

     NamespaceTrackingProperty.cs ファイルが作成され、編集用に開かれます。

4. フォルダーに、`ExampleModel.cs,``HelperClasses.cs`、`Serialization.cs`、および `TypeDescriptor.cs`の各コードファイルを作成します。

5. **Dslpackage**プロジェクトでは、`CustomCode` フォルダーも作成し、`Package.cs` コードファイルに追加します。

## <a name="adding-helper-classes-to-support-tracking-properties"></a>追跡プロパティをサポートするヘルパークラスの追加
 HelperClasses.cs ファイルに、次のように `TrackingHelper` クラスと `CriticalException` クラスを追加します。 これらのクラスは、このチュートリアルの後半で参照します。

#### <a name="to-add-the-helper-classes"></a>ヘルパークラスを追加するには

1. HelperClasses.cs ファイルに次のコードを追加します。

    ```csharp
    using System;
    using System.Collections;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        internal static class TrackingHelper
        {
            /// <summary>Notify each model element in a collection that a tracked
            /// property has changed.</summary>
            /// <param name="store">The store for the model.</param>
            /// <param name="collection">The collection of model elements that
            /// contain the tracking property.</param>
            /// <param name="propertyId">The ID of the tracking property.</param>
            /// <param name="trackingPropertyId">The ID of the property that
            /// indicates whether the tracking property is tracking.</param>
            internal static void UpdateTrackingCollectionProperty(
                Store store,
                IEnumerable collection,
                Guid propertyId,
                Guid trackingPropertyId)
            {
                DomainPropertyInfo propInfo =
                    store.DomainDataDirectory.GetDomainProperty(propertyId);

                DomainPropertyInfo trackingPropInfo =
                    store.DomainDataDirectory.GetDomainProperty(trackingPropertyId);

                Debug.Assert(propInfo != null);
                Debug.Assert(trackingPropInfo != null);
                Debug.Assert(trackingPropInfo.PropertyType.Equals(typeof(bool)),
                    "Tracking property not specified as a boolean");

                foreach (ModelElement element in collection)
                {
                    // If the tracking property is currently tracking, then notify
                    // it that the tracked property has changed.
                    bool isTracking = (bool)trackingPropInfo.GetValue(element);
                    if (isTracking)
                    {
                        propInfo.NotifyValueChange(element);
                    }
                }
            }
        }

        /// <summary>Helper class to flag critical exceptions from ones that are
        /// safe to ignore.</summary>
        internal static class CriticalException
        {
            /// <summary>Gets whether an exception is critical and can not be
            /// ignored.</summary>
            /// <param name="ex">The exception to check.</param>
            /// <returns>True if the exception is critical.</returns>
            internal static bool IsCriticalException(Exception ex)
            {
                if (ex is NullReferenceException
                    || ex is StackOverflowException
                    || ex is OutOfMemoryException
                    || ex is System.Threading.ThreadAbortException)
                    return true;

                if (ex.InnerException != null)
                    return IsCriticalException(ex.InnerException);

                return false;
            }
        }
    }
    ```

## <a name="adding-custom-code-for-the-custom-type-descriptor"></a>カスタム型記述子のカスタムコードを追加する
 `ExampleModel` ドメインクラスの型記述子の `GetCustomProperties` メソッドを実装します。

> [!NOTE]
> DSL ツールがカスタム型記述子のために生成するコード `ExampleModel` `GetCustomProperties`を呼び出します。ただし、DSL ツールは、メソッドを実装するコードを生成しません。

 このメソッドを定義すると、名前空間の追跡プロパティの追跡プロパティ記述子が作成されます。 また、tracking プロパティの属性を指定すると、 **[プロパティ]** ウィンドウでプロパティを正しく表示できます。

#### <a name="to-modify-the-type-descriptor-for-the-examplemodel-domain-class"></a>Examplemodel.store domain クラスの型記述子を変更するには

1. TypeDescriptor.cs ファイルに次のコードを追加します。

    ```csharp
    using System;
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the custom type descriptor for the ExampleElement domain class, add
        // the GetCustomProperties method.
        public partial class ExampleElementTypeDescriptor
        {
            /// <summary>Returns the property descriptors for the described
            /// ExampleElement domain class.</summary>
            /// <remarks>This method adds the tracking property descriptor.
            /// </remarks>
            private PropertyDescriptorCollection GetCustomProperties(
                Attribute[] attributes)
            {
                // Get the default property descriptors from the base class
                PropertyDescriptorCollection propertyDescriptors =
                    base.GetProperties(attributes);

                // Get a reference to the model element that is being described.
                ExampleElement source = this.ModelElement as ExampleElement;

                //Add the descriptor for the tracking property.
                if (source != null)
                {
                    DomainPropertyInfo domainProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.NamespaceDomainPropertyId);

                    DomainPropertyInfo trackingProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.IsNamespaceTrackingDomainPropertyId);

                    // Define attributes for the tracking property so that the
                    // Properties window displays the property correctly.
                    Attribute[] attr = new Attribute[] {
                        new DisplayNameAttribute("Element Namespace"),
                        new DescriptionAttribute("The namespace of the element."),
                        new CategoryAttribute("Tracking Properties"),
                    };

                    propertyDescriptors.Add(new TrackingPropertyDescriptor(
                        source, domainProperty, trackingProperty, attr));
                }

                // Return the property descriptors for this element
                return propertyDescriptors;
            }
        }
    }
    ```

## <a name="adding-custom-code-for-the-package"></a>パッケージのカスタムコードを追加する
 生成されたコードは、例の要素ドメインクラスの型説明のプロバイダーを定義します。ただし、この型説明のプロバイダーを使用するように DSL に指示するコードを追加する必要があります。

#### <a name="to-update-the-dsl-package-to-use-your-custom-type-descriptor"></a>カスタム型記述子を使用するように DSL パッケージを更新するには

1. Package.cs ファイルに次のコードを追加します。

    ```csharp
    using System.ComponentModel;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // Override the default Initialize method.
        internal sealed partial class TrackingPropertyDSLPackage
        {
            protected override void Initialize()
            {
                // Add the custom type descriptor for the ExampleElement type.
                TypeDescriptor.AddProvider(
                    new ExampleElementTypeDescriptionProvider(),
                    typeof(ExampleElement));

                base.Initialize();
            }
        }
    }
    ```

## <a name="adding-custom-code-for-the-model"></a>モデルのカスタムコードを追加する
 `ExampleModel` ドメインクラスの `GetCustomElementsValue` メソッドを実装します。

> [!NOTE]
> DSL ツールが `ExampleModel` を呼び出すために生成するコード `GetCustomElementsValue`;ただし、DSL ツールは、メソッドを実装するコードを生成しません。

 `GetCustomElementsValue` メソッドを定義すると、`ExampleModel`の CustomElements 計算プロパティのロジックが提供されます。 このメソッドは、ユーザーが更新した値を持つ名前空間追跡プロパティを持つ `ExampleElement` ドメインクラスの数をカウントし、モデル内の要素の合計の比率としてこのカウントを表す文字列を返します。

 また、`ExampleModel`に `OnDefaultNamespaceChanged` メソッドを追加し、`ExampleModel` の `DefaultNamespacePropertyHandler` 入れ子になったクラスの `OnValueChanged` メソッドをオーバーライドして `OnDefaultNamespaceChanged`を呼び出します。

 DefaultNamespace プロパティは名前空間の追跡プロパティを計算するために使用されるため、`ExampleModel` は、DefaultNamespace の値が変更されたことをすべての `ExampleElement` ドメインクラスに通知する必要があります。

#### <a name="to-modify-the-property-handler-for-the-tracked-property"></a>追跡対象のプロパティのプロパティハンドラーを変更するには

1. ExampleModel.cs ファイルに次のコードを追加します。

    ```csharp
    using System.Linq;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        public partial class ExampleModel
        {
            public string GetCustomElementsValue()
            {
                if (this.Elements.Count == 0) return "0/0";

                int number = this.Elements.Count(e => !e.IsNamespaceTracking);
                return string.Format("{0}/{1}", number, this.Elements.Count);
            }

            #region Value changed handler for the tracked property

            // When a tracked property changes, it needs to notify all of the properties
            // that track it.

            /// <summary>Called by the DefaultNamespace property value handler when the
            /// DefaultNamespace property changes.</summary>
            /// <param name="oldValue">The previous value of the property.</param>
            /// <param name="newValue">The new value of the property.</param>
            protected virtual void OnDefaultNamespaceChanged(
                string oldValue, string newValue)
            {
                // Use the helper class to notify all of the elements in the model
                // that the default namespace has changed.
                TrackingHelper.UpdateTrackingCollectionProperty(
                    this.Store,
                    this.Elements,
                    ExampleElement.NamespaceDomainPropertyId,
                    ExampleElement.IsNamespaceTrackingDomainPropertyId);
            }

            // Update the change handler for the DefaultNamespace property.
            internal sealed partial class DefaultNamespacePropertyHandler
            {
                /// <summary>Called when the DefaultNamespace property changes.</summary>
                /// <param name="element">The model element that has the property that
                /// changed.</param>
                /// <param name="oldValue">The previous value of the property.</param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleModel element, string oldValue, string newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);

                    if (!element.Store.InUndoRedoOrRollback)
                    {
                        element.OnDefaultNamespaceChanged(oldValue, newValue);
                    }
                }
            }

            #endregion
        }
    }
    ```

## <a name="adding-custom-code-for-the-tracking-property"></a>追跡プロパティのカスタムコードを追加する
 `ExampleElement` ドメインクラスに `CalculateNamespace` メソッドを追加します。

 このメソッドを定義すると、`ExampleModel`の CustomElements 計算プロパティのロジックが提供されます。 このメソッドは、ユーザー状態によって更新された名前空間の追跡プロパティを持つ `ExampleElement` ドメインクラスの数をカウントし、モデル内の要素の合計の比率としてこのカウントを表す文字列を返します。

 また、、、およびメソッドのストレージを追加して、`ExampleElement` ドメインクラスの名前空間カスタムストレージプロパティを取得および設定します。

> [!NOTE]
> DSL ツールが `ExampleModel` 用に生成するコードは、get メソッドと set メソッドを呼び出します。ただし、DSL ツールは、メソッドを実装するコードを生成しません。

#### <a name="to-add-the-method-for-the-custom-type-descriptor"></a>カスタム型記述子のメソッドを追加するには

1. NamespaceTrackingProperty.cs ファイルに次のコードを追加します。

    ```csharp
    using System;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the domain class that has the tracking property, add the caluclation
        // for when the property is tracking.
        public partial class ExampleElement
        {
            /// <summary>Calculates the actual value of the property when it is
            /// tracking.</summary>
            /// <returns>The value of the tracking property when it is
            /// tracking.</returns>
            /// <remarks>Making this method virtual allows child classes to modify
            /// the calculation. This method does not need to perform validation, as
            /// its caller handles validation prior to calling this method.
            /// <para>In this case, the tracking value depends on the default namespace
            /// property of the parent model.</para></remarks>
            protected virtual string CalculateNamespace()
            {
                return this.ExampleModel.DefaultNamespace;
            }

            #region Tracking property implementation

            // Implement the Namespace domain property of the ExampleElement domain class,
            // and update the IsNamespaceTracking domain property value handler.

            /// <summary>Storage for the Namespace property.</summary>
            private string namespaceStorage;

            /// <summary>Gets the value of the Namespace property.</summary>
            /// <returns>The value of the Namespace property.</returns>
            private string GetNamespaceValue()
            {
                // Only retrieve the tracked value if the store is not in the
                // middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!loading && this.IsNamespaceTracking)
                {
                    try
                    {
                        return this.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                        return default(string);
                    }
                    catch (Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                        else
                        {
                            return default(string);
                        }
                    }
                }

                return namespaceStorage;
            }

            /// <summary>Sets the value of the Namespace property.</summary>
            /// <param name="value">The new value for the property.</param>
            private void SetNamespaceValue(string value)
            {
                namespaceStorage = value;

                // Only update the state of the tracking property if the store is
                // not in the middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!this.Store.InUndoRedoOrRollback && !loading)
                {
                    this.IsNamespaceTracking = false;
                }
            }

            // Update the default behavior of the ExampleElement.IsNamespaceTracking
            // domain property value handler.
            internal sealed partial class IsNamespaceTrackingPropertyHandler
            {
                /// <summary>Called after the IsNamespaceTracking property changes.
                /// </summary>
                /// <param name="element">The model element that has the property
                /// that changed.</param>
                /// <param name="oldValue">The previous value of the property.
                /// </param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleElement element, Boolean oldValue, Boolean newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);
                    if (!element.Store.InUndoRedoOrRollback && newValue)
                    {
                        DomainPropertyInfo propInfo =
                            element.Store.DomainDataDirectory.GetDomainProperty(
                                ExampleElement.NamespaceDomainPropertyId);
                        propInfo.NotifyValueChange(element);
                    }
                }

                /// <summary>Performs the reset operation for the IsNamespaceTracking
                /// property for a model element.</summary>
                /// <param name="element">The model element that has the property
                /// to reset.</param>
                internal void ResetValue(ExampleElement element)
                {
                    object calculatedValue = null;

                    try
                    {
                        calculatedValue = element.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                    }
                    catch (System.Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                    }

                    if ((calculatedValue != null
                        && object.Equals(element.Namespace, calculatedValue)))
                    {
                        element.isNamespaceTrackingPropertyStorage = true;
                    }
                }

                /// <summary>Method to set IsNamespaceTracking to false so that this
                /// instance of this tracking property is not storage-based.
                /// </summary>
                /// <param name="element">The element on which to reset the property
                /// value.</param>
                internal void PreResetValue(ExampleElement element)
                {
                    // Force the IsNamespaceTracking property to false so that the value
                    // of the Namespace property is retrieved from storage.
                    element.isNamespaceTrackingPropertyStorage = false;
                }
            }

            #endregion
        }
    }
    ```

## <a name="adding-custom-code-to-support-serialization"></a>シリアル化をサポートするカスタムコードの追加
 XML シリアル化のカスタムの読み込み後動作をサポートするコードを追加します。

> [!NOTE]
> DSL ツールが生成するコードは、`OnPostLoadModel` メソッドと `OnPostLoadModelAndDiagram` メソッドを呼び出します。ただし、DSL ツールは、これらのメソッドを実装するコードを生成しません。

#### <a name="to-add-code-to-support-the-custom-post-load-behavior"></a>カスタムの読み込み後の動作をサポートするコードを追加するには

1. Serialization.cs ファイルに次のコードを追加します。

    ```csharp
    using System;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        #region Helper classes for maintaining state while the store is serializing.

        public abstract partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Reset the tracking state properties to their natural values
            /// based on comparing storage with calculation.</summary>
            /// <param name="store">The store that contains this model.</param>
            internal static void ResetTrackingProperties(Store store)
            {
                // Two passes required - one to set all elements to storage-based
                // then another to set some back to being tracking.
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.PreResetIsTrackingProperties();
                        continue;
                    }
                }
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.ResetIsTrackingProperties();
                        continue;
                    }
                }
            }
        }

        // Add the pre-reset and reset methods for the model element.
        public partial class ExampleElement
        {
            /// <summary>Calls the pre-reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void PreResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.PreResetValue(this);
            }

            /// <summary>Calls the reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void ResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.ResetValue(this);
            }
        }

        #endregion

        #region Custom serialization code

        // To the serialization helper for the TrackingPropertyDSL class, add post
        // load handlers to bind the tracking property to the serialization process.
        // These handlers manage the tracking states and property values when the
        // model is serialized and deserialized.
        public partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Customize model loading.</summary>
            /// <param name="serializationResult">The serialization result from the
            /// load operation.</param>
            /// <param name="partition">The partition in which the new
            /// instance was created.</param>
            /// <param name="fileName">The name of the file from which the
            /// instance was deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.
            /// </param>
            private void OnPostLoadModel(
                SerializationResult serializationResult,
                Partition partition,
                string fileName,
                ExampleModel modelRoot)
            {
            }

            /// <summary>Customize model and diagram loading.</summary>
            /// <param name="serializationResult">Stores serialization result from
            /// the load operation.</param>
            /// <param name="modelPartition">Partition in which the new
            /// instance will be created.</param>
            /// <param name="modelFileName">Name of the file from which the
            /// instance will be deserialized.</param>
            /// <param name="diagramPartition">Partition in which the new
            /// diagram instance will be created.</param>
            /// <param name="diagramFileName">Name of the file from which the
            /// diagram instance will be deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.</param>
            /// <param name="diagram">The diagram matching the modelRoot.</param>
            private void OnPostLoadModelAndDiagram(
                SerializationResult serializationResult,
                Partition modelPartition,
                string modelFileName,
                Partition diagramPartition,
                string diagramFileName,
                ExampleModel modelRoot,
                TrackingPropertyDSLDiagram diagram)
            {
                Debug.Assert(modelPartition != null);
                Debug.Assert(modelPartition.Store != null);

                // Tracking properties need to be set up according to whether the
                // serialization matches the calculated values.
                TrackingPropertyDSLSerializationHelperBase.ResetTrackingProperties(
                    modelPartition.Store);
            }
        }

        #endregion
    }
    ```

## <a name="testing-the-language"></a>言語のテスト
 次の手順では、[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] の新しいインスタンスで DSL デザイナーをビルドして実行し、追跡プロパティが正常に機能していることを確認できるようにします。

#### <a name="to-exercise-the-language"></a>言語を試すには

1. **[ビルド]** メニューで、 **[ソリューションのリビルド]** をクリックします。

2. **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。

     [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] の実験用ビルドでは、空のテストファイルを含む**デバッグ**ソリューションが開きます。

3. **ソリューションエクスプローラー**で、[trackingPropertyDsl] ファイルをダブルクリックしてデザイナーで開き、デザイン画面をクリックします。

     ダイアグラムの **[プロパティ]** ウィンドウでは、既定の**名前空間**プロパティは**Defaultnamespace**であり、**カスタム Elements**プロパティは**0/0**です。

4. **ツールボックス** から 例**要素**要素をダイアグラム画面にドラッグします。

5. 要素の **[プロパティ]** ウィンドウで、 **[要素の名前空間]** プロパティを選択し、 **defaultnamespace**から**othernamespace**に値を変更します。

     **要素の名前空間**の値が太字で表示されていることに注意してください。

6. **[プロパティ]** ウィンドウで、 **[要素の名前空間]** を右クリックし、 **[リセット]** をクリックします。

     プロパティの値が**Defaultnamespace**に変更され、値が通常のフォントで表示されます。

     **要素の名前空間**をもう一度右クリックします。 プロパティが現在追跡中の状態であるため、**リセット**コマンドは無効になりました。

7. 別の例の**要素**を**ツールボックス**から図の画面にドラッグし、その**要素の名前空間**を**othernamespace**に変更します。

8. デザイン画面をクリックします。

     図の **[プロパティ]** ウィンドウで、**カスタム要素**の値は**1/2**になりました。

9. ダイアグラムの**既定の名前空間**を**Defaultnamespace**から**newnamespace**に変更します。

     最初の要素の**名前空間**は、**既定の名前空間**プロパティを追跡します。一方、2番目の要素の**名前**空間は、 **othernamespace**のユーザー更新値を保持します。

10. ソリューションを保存し、実験用ビルドを終了します。

## <a name="next-steps"></a>次のステップ
 複数の追跡プロパティを使用する場合、または複数の DSL で追跡プロパティを実装する場合は、各追跡プロパティをサポートするための共通コードを生成するテキストテンプレートを作成できます。 テキストテンプレートの詳細については、「[コード生成と T4 テキストテンプレート](../modeling/code-generation-and-t4-text-templates.md)」を参照してください。

## <a name="see-also"></a>参照
 <xref:Microsoft.VisualStudio.Modeling.Design.TrackingPropertyDescriptor> <xref:Microsoft.VisualStudio.Modeling.Design.ElementTypeDescriptor>
 [ドメイン固有言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md) [: ドメイン固有言語ソリューションを作成](../modeling/how-to-create-a-domain-specific-language-solution.md)する方法[チュートリアル: ドメイン固有言語定義のカスタマイズ](../misc/walkthrough-customizing-the-domain-specific-language-definition.md)
