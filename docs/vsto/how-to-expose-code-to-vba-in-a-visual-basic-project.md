---
title: '方法: Visual Basic プロジェクトでコードを VBA に公開する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- Visual Basic [Office development in Visual Studio], exposing code to VBA
- exposing code to VBA
- host items [Office development in Visual Studio], exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8aa29fca9905c9f1ed056949eec64ad967323462
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544847"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-basic-project"></a>方法: Visual Basic プロジェクトでコードを VBA に公開する
  2種類のコードが相互に対話できるようにする場合は、プロジェクトのコード [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] を公開して、Visual Basic for Applications (VBA) コードにすることができます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Visual Basic プロセスは、Visual C# のプロセスとは異なります。 詳細については、「[方法: Visual C&#35; プロジェクトでコードを VBA に公開](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)する」を参照してください。

 このプロセスは、他のクラスのコードの場合とは異なり、ホスト項目クラスのコードでは異なります。

- [ホスト項目クラスでコードを公開する](#HostItemCode)

- [ホスト項目クラスに含まれていないコードを公開する](#NonHostItem)

## <a name="expose-code-in-a-host-item-class"></a><a name="HostItemCode"></a>ホスト項目クラスでコードを公開する
 VBA コードがホスト項目クラスの Visual Basic コードを呼び出せるようにするには、ホスト項目の**EnableVbaCallers**プロパティを**True**に設定します。

 ホスト項目クラスのメソッドを公開してから VBA から呼び出す方法を示すチュートリアルについては、「[チュートリアル: Visual Basic プロジェクトの vba からコードを呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)」を参照してください。 ホスト項目の詳細については、「[ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

#### <a name="to-expose-code-in-a-host-item-to-vba"></a>ホスト項目内のコードを VBA に公開するには

1. [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]マクロをサポートし、既に VBA コードが含まれている Word 文書、excel ブック、または excel テンプレートに基づくドキュメントレベルのプロジェクトを開くか、作成します。

     マクロをサポートするドキュメントファイル形式の詳細については、「 [VBA とドキュメントレベルのカスタマイズの結合](../vsto/combining-vba-and-document-level-customizations.md)」を参照してください。

    > [!NOTE]
    > この機能は、Word テンプレート プロジェクトでは使用できません。

2. マクロを有効にするようユーザーに求めることなく、ドキュメント内の VBA コードの実行が許可されていることを確認します。 Word または Excel のセキュリティ センター設定の信頼できる場所の一覧に Office プロジェクトの場所を追加することによって、VBA コードの実行を信頼することができます。

3. VBA に公開するプロパティ、メソッド、またはイベントをプロジェクトのホスト項目クラスの1つに追加し、新しいメンバーを**パブリック**として宣言します。 クラスの名前は、アプリケーションによって異なります。

    - Word プロジェクトでは、ホスト項目クラスには既定でという名前が付けられ `ThisDocument` ます。

    - Excel プロジェクトでは、ホスト項目クラスは、既定では、、、およびという名前に `ThisWorkbook` `Sheet1` `Sheet2` `Sheet3` なります。

4. ホスト項目の**EnableVbaCallers**プロパティを**True**に設定します。 このプロパティは、デザイナーでホスト項目が開いているときに、[**プロパティ**] ウィンドウで使用できます。

     このプロパティを設定すると、Visual Studio によって自動的に**ReferenceAssemblyFromVbaProject**プロパティが**True**に設定されます。

    > [!NOTE]
    > ブックまたはドキュメントに VBA コードが含まれていない場合、またはドキュメント内の VBA コードの実行が信頼されていない場合は、 **EnableVbaCallers**プロパティを**True**に設定するとエラーメッセージが表示されます。 これは、このような状況では、Visual Studio がドキュメントのVBA プロジェクトを変更できないためです。

5. 表示されるメッセージで **[OK]** をクリックします。 このメッセージは、からプロジェクトを実行しているときに、ブックまたはドキュメントに VBA コードを追加した場合、次にプロジェクトをビルドしたときに VBA コードが失われることを示して [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] います。 これは、プロジェクトをビルドするたびに、ビルド出力フォルダー内のドキュメントが上書きされるためです。

     この時点で、VBA プロジェクトがアセンブリを呼び出すことができるように、Visual Studio によってプロジェクトが構成されます。 また、Visual Studio は、という名前のプロパティを VBA プロジェクトの、、 `CallVSTOAssembly` `ThisDocument` `ThisWorkbook` `Sheet1` 、、またはの各モジュールに追加し `Sheet2` `Sheet3` ます。 このプロパティを使用すると、VBA に公開したクラスのパブリックメンバーにアクセスできます。

6. プロジェクトをビルドします。

## <a name="expose-code-that-is-not-in-a-host-item-class"></a><a name="NonHostItem"></a>ホスト項目クラスに含まれていないコードを公開する
 VBA コードがホスト項目クラスに含まれていない Visual Basic コードを呼び出せるようにするには、コードを変更して VBA に表示されるようにします。

### <a name="to-expose-code-that-is-not-in-a-host-item-class-to-vba"></a>ホスト項目クラスに含まれていないコードを VBA に公開するには

1. [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]マクロをサポートし、既に VBA コードが含まれている Word 文書、excel ブック、または excel テンプレートに基づくドキュメントレベルのプロジェクトを開くか、作成します。

     マクロをサポートするドキュメントファイル形式の詳細については、「 [VBA とドキュメントレベルのカスタマイズの結合](../vsto/combining-vba-and-document-level-customizations.md)」を参照してください。

    > [!NOTE]
    > この機能は、Word テンプレート プロジェクトでは使用できません。

2. マクロを有効にするようユーザーに求めることなく、ドキュメント内の VBA コードの実行が許可されていることを確認します。 Word または Excel のセキュリティ センター設定の信頼できる場所の一覧に Office プロジェクトの場所を追加することによって、VBA コードの実行を信頼することができます。

3. VBA に公開するメンバーをプロジェクトのパブリッククラスに追加し、新しいメンバーを**パブリック**として宣言します。

4. 次の <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性と <xref:Microsoft.VisualBasic.ComClassAttribute> 属性を、VBA に公開するクラスに適用します。 これらの属性により、クラスが VBA に表示されるようになります。

    ```vb
    <Microsoft.VisualBasic.ComClass()> _
    <System.Runtime.InteropServices.ComVisibleAttribute(True)> _
    ```

5. プロジェクトでホスト項目クラスの **GetAutomationObject** メンバーをオーバーライドして、VBA に公開したクラスのインスタンスを返すようにします。 次のコード例では、という名前のクラスを VBA に公開していることを前提としてい `DocumentUtilities` ます。

    ```vb
    Protected Overrides Function GetAutomationObject() As Object
        Return New DocumentUtilities()
    End Function
    ```

6. でドキュメント (Word の場合) またはワークシート (Excel の場合) デザイナーを開き [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

7. **[プロパティ]** ウィンドウで、 **ReferenceAssemblyFromVbaProject** プロパティを選択し、値を **True**に変更します。

    > [!NOTE]
    > ブックまたはドキュメントに VBA コードが含まれていない場合、またはドキュメント内の VBA コードの実行が信頼されていない場合は、 **ReferenceAssemblyFromVbaProject**プロパティを**True**に設定するとエラーメッセージが表示されます。 これは、このような状況では、Visual Studio がドキュメントのVBA プロジェクトを変更できないためです。

8. 表示されるメッセージで **[OK]** をクリックします。 このメッセージは、からプロジェクトを実行しているときに、ブックまたはドキュメントに VBA コードを追加した場合、次にプロジェクトをビルドしたときに VBA コードが失われることを示して [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] います。 これは、プロジェクトをビルドするたびに、ビルド出力フォルダー内のドキュメントが上書きされるためです。

     この時点で、VBA プロジェクトがアセンブリを呼び出すことができるように、Visual Studio によってプロジェクトが構成されます。 また、Visual Studio では、という名前のメソッドが `GetManagedClass` VBA プロジェクトに追加されます。 Vba プロジェクト内の任意の場所からこのメソッドを呼び出して、VBA に公開したクラスにアクセスできます。

9. プロジェクトをビルドします。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [VBA とドキュメントレベルのカスタマイズの結合](../vsto/combining-vba-and-document-level-customizations.md)
- [チュートリアル: Visual Basic プロジェクトで VBA からコードを呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
- [方法: Visual C&#35; プロジェクトでコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
