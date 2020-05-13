---
title: '方法: コードを VBA に公開するC#プロジェクト'
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual C# [Office development in Visual Studio], exposing code to VBA
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ac41f4da29b95ba1fcd1601f98104956d584212a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63419517"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-c-project"></a>方法: Visual c# プロジェクトでのコードを VBA に公開します。
  相互作用するコードの 2 つの種類の場合は、Visual C# プロジェクトを Visual Basic for Applications (VBA) コード内のコードを公開できます。

 Visual C# プロセスは、Visual Basic のプロセスからは異なります。 詳細については、「[方法 :Visual Basic プロジェクトでのコードを VBA に公開](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)します。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="expose-code-in-a-visual-c-project"></a>Visual C# プロジェクトでコードが公開します。
 Visual C# プロジェクトのコードを呼び出す VBA コードを有効にするのには、COM から参照できるようにコードを変更し、設定、 **ReferenceAssemblyFromVbaProject**プロパティを**True**デザイナー。

 VBA から Visual c# プロジェクトでメソッドを呼び出す方法について説明するチュートリアルでは、次を参照してください。[チュートリアル。コードを Visual C での VBA から呼び出す&#35;プロジェクト](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)します。

### <a name="to-expose-code-in-a-visual-c-project-to-vba"></a>VBA に Visual C# プロジェクト内のコードを公開するには

1. 開くか、Word 文書、Excel ブックまたは Excel テンプレート、マクロをサポートして、VBA コードを既に含むに基づくドキュメント レベルのプロジェクトを作成します。

    マクロをサポートするドキュメントのファイル形式の詳細については、次を参照してください。[結合 VBA とドキュメント レベルのカスタマイズ](../vsto/combining-vba-and-document-level-customizations.md)します。

   > [!NOTE]
   > この機能は、Word テンプレート プロジェクトでは使用できません。

2. ドキュメント内の VBA コードがマクロを有効にするユーザーを確認なしで実行を許可されていることを確認します。 Word または Excel のセキュリティ センター設定の信頼できる場所の一覧に Office プロジェクトの場所を追加することによって、VBA コードの実行を信頼することができます。

3. プロジェクトで、パブリック クラスを VBA に公開するメンバーを追加し、新しいメンバーとして宣言**パブリック**します。

4. 次の適用<xref:System.Runtime.InteropServices.ComVisibleAttribute>と<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>属性を VBA に公開するクラス。 これらの属性によってクラスが COM で表示されるようになりますが、クラスのインターフェイスは生成されません。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   [System.Runtime.InteropServices.ClassInterface(
       System.Runtime.InteropServices.ClassInterfaceType.None)]
   ```

5. 上書き、 **GetAutomationObject**を VBA に公開するクラスのインスタンスを返すプロジェクトでホスト項目クラスのメソッド。

   - VBA にホスト項目クラスを公開する場合は、オーバーライド、 **GetAutomationObject** 、このクラスに属しているクラスの現在のインスタンスを返すメソッド。

     ```csharp
     protected override object GetAutomationObject()
     {
         return this;
     }
     ```

   - VBA のホスト項目ではないクラスを公開する場合は、オーバーライド、 **GetAutomationObject**プロジェクト内の項目し、非ホスト項目クラスのインスタンスを返す任意のホストのメソッド。 たとえば、次のコードはという名前のクラスを公開することを仮定`DocumentUtilities`VBA にします。

     ```csharp
     protected override object GetAutomationObject()
     {
         return new DocumentUtilities();
     }
     ```

     ホスト項目の詳細については、次を参照してください。[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)します。

6. VBA に公開するクラスからインターフェイスを抽出します。 **インターフェイスの抽出** ダイアログ ボックスで、インターフェイス宣言で追加するパブリック メンバーを選択します。 詳細については、次を参照してください。[抽出インターフェイス リファクタリング](../ide/reference/extract-interface.md)します。

7. 追加、**パブリック**キーワードをインターフェイスの宣言にします。

8. 次を追加することで、インターフェイスを COM に表示されるように<xref:System.Runtime.InteropServices.ComVisibleAttribute>属性をインターフェイス。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   ```

9. (Word) のドキュメントまたはワークシート (for Excel) をデザイナーで開く[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]します。

10. **[プロパティ]** ウィンドウで、 **ReferenceAssemblyFromVbaProject** プロパティを選択し、値を **True**に変更します。

    > [!NOTE]
    > かどうか、ブックまたはドキュメントが含まれない VBA コードまたはドキュメント内の VBA コードが実行する信頼されていない場合は、設定すると、エラー メッセージが表示されるが、 **ReferenceAssemblyFromVbaProject**プロパティを**True**. これは、このような状況では、Visual Studio がドキュメントのVBA プロジェクトを変更できないためです。

11. 表示されるメッセージで **[OK]** をクリックします。 このメッセージ通知することを追加する場合 VBA コードをブックまたはドキュメントからプロジェクトを実行するときに[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]、VBA コードは失われます、次回、プロジェクトをビルドします。 これは、ビルドでドキュメントを出力フォルダーは、プロジェクトをビルドするたびに上書きされるためです。

     この時点では、VBA プロジェクトがアセンブリを呼び出すことができるように、Visual Studio は、プロジェクトを構成します。 Visual Studio では、という名前のメソッドも追加します`GetManagedClass`VBA プロジェクトにします。 このメソッドは、任意の場所から呼び出すことができますを VBA に公開したクラスにアクセスする VBA プロジェクトにします。

12. プロジェクトをビルドします。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio での Office プロジェクトを作成します。](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [VBA とドキュメント レベルのカスタマイズを結合します。](../vsto/combining-vba-and-document-level-customizations.md)
- [チュートリアル: コードを Visual C での VBA から呼び出す&#35;プロジェクト](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
- [方法: Visual Basic プロジェクトでのコードを VBA に公開します。](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
