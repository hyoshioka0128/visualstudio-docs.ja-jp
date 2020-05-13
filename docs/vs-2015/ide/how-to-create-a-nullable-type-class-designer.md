---
title: '方法: Null 許容型を作成する (クラス デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- nullable types, Class Designer
- Class Designer [Visual Studio], nullable types
ms.assetid: 84673a89-3f6d-4668-919e-1c0f56182fe5
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 438f84a172c7e0a2d0dc957c578adc568a46495f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668159"
---
# <a name="how-to-create-a-nullable-type-class-designer"></a>方法: Null 許容型を作成する (クラス デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ある種の値の型は、常に値が定義されている (または必要である) とは限りません。 これはデータベースではよくあることであり、一部のフィールドに値が何も割り当てられない場合があります。 たとえば、データベースのフィールドに値がまだ割り当てられていないことを示すために、フィールドに null 値を割り当てることがあります。

 *null 許容型*は、その型の一般的な値の範囲だけでなく null 値も受け付けるように拡張した値型です。 たとえば、`Int32` の null 許容型 (Nullable\<Int32> とも書きます) には、-2147483648 から 2147483647 の任意の値または null 値を代入できます。 Nullable\<bool> には、値 `True`、`False`、または null (値がまったくない) を割り当てることができます。

 Null 許容型は、<xref:System.Nullable%601> 構造体のインスタンスです。 null 許容型の各インスタンスには、2 つのパブリック読み取り専用プロパティ `HasValue` と `Value` があります。

- `HasValue` は `bool` 型であり、変数に定義済みの値が含まれるかどうかを示します。 `True` は、変数に null 以外の値が含まれていることを意味します。 `if (x.HasValue)` や `if (y != null)` などのステートメントを使って、定義済みの値をテストできます。

- `Value` は、基になっている型と同じ型です。 `HasValue` が `True` の場合、`Value` には意味のある値が含まれています。 `HasValue` が `False` の場合は、`Value` にアクセスすると無効操作例外がスローされます。

  既定では、変数を null 許容型として宣言すると、その変数は基になる値型の既定値ではなく定義されていない値になります (`HasValue` は `False`)。

  クラス デザイナーでは、null 許容型はその基になる型と同じように表示されます。

  Visual C# での null 許容型について詳しくは、「[null 許容型](https://msdn.microsoft.com/library/e473cb01-28ca-42be-9cea-f717055d72c6)」をご覧ください。 Visual Basic での null 許容型について詳しくは、「[null 許容値型](https://msdn.microsoft.com/library/9ac3b602-6f96-4e6d-96f7-cd4e81c468a6)」をご覧ください。

  [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

### <a name="to-add-a-nullable-type-by-using-the-class-designer"></a>クラス デザイナーを使って null 許容型を追加するには

1. クラス ダイアグラムで、既存のクラスを展開するか、新しいクラスを作成します。

2. プロジェクトにクラスを追加するには、 **[クラス ダイアグラム]** メニューの **[追加]** をクリックし、 **[クラスの追加]** をクリックします。

3. クラスの図形を展開するには、 **[クラス ダイアグラム]** メニューの **[展開]** をクリックします。

4. クラスの図形を選びます。 **[クラス ダイアグラム]** メニューの **[追加]** をクリックし、 **[フィールド]** をクリックします。 既定の "**フィールド**" という名前の新しいフィールドが、クラスの図形と **[クラスの詳細]** ウィンドウに表示されます。

5. **[クラスの詳細]** ウィンドウの **[名前]** 列 (または、クラスの図形自体) で、新しいフィールドの名前を有効でわかりやすい名前に変更します。

6. **[クラスの詳細]** ウィンドウの **[型]** 列で、次のコードに示すように、null 許容型として型を宣言します。

    ```csharp
    // Declare a nullable type in Visual C#:
    class Test
    {
       int? building_number = 5;
    }
    ```

    ```vb
    ' Declare a nullable type in Visual Basic:
    Class Test
       Dim buildingNumber As Nullable(Of Integer) = 5
    End Class
    ```

### <a name="to-add-a-nullable-type-by-using-the-code-editor"></a>コード エディターを使って null 許容型を追加するには

1. プロジェクトにクラスを追加します。 **ソリューション エクスプローラー**でプロジェクト ノードを選び、 **[プロジェクト]** メニューの **[クラスの追加]** をクリックします。

2. 新しいクラスの .cs または .vb ファイルで、新しいクラスの null 許容型をクラス宣言に追加します。

3. クラス ビューからクラス デザイナーのデザイン サーフェイスに、新しいクラスのアイコンをドラッグします。 クラス ダイアグラムにクラスの図形が表示されます。

4. クラスの図形の詳細を展開し、クラス メンバーをマウスでポイントします。 各メンバーの宣言がツールヒントに表示されます。

5. クラスの図形を右クリックし、 **[クラスの詳細]** をクリックします。 **[クラスの詳細]** ウィンドウで、新しい型のプロパティを表示または変更できます。

## <a name="see-also"></a>参照
 null 許容型[を使用し](https://msdn.microsoft.com/library/0bacbe72-ce15-4b14-83e1-9c14e6380c28)た[null](https://msdn.microsoft.com/library/e473cb01-28ca-42be-9cea-f717055d72c6)許容型の <xref:System.Nullable%601> 方法: null 許容型の[Null 許容値型](https://msdn.microsoft.com/library/9ac3b602-6f96-4e6d-96f7-cd4e81c468a6)[を識別する](https://msdn.microsoft.com/library/d4b67ee2-66e8-40c1-ae9d-545d32c71387)
