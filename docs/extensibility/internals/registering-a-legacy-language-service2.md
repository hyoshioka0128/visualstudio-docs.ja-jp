---
title: レガシ言語の登録 Service2 |Microsoft Docs
description: この記事では、Visual Studio で使用できるさまざまな言語サービスオプションのレジストリエントリの一覧を示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, language services
- language services, registry information
- registry, language services
ms.assetid: ca312aa3-f9f1-4572-8553-89bf3a724deb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fbad469b28c0b8a6aab070d47cf12c326beb92d8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062786"
---
# <a name="registering-a-legacy-language-service-2"></a>従来の言語サービスの登録2
以下のセクションでは、で使用できるさまざまな言語サービスオプションのレジストリエントリの一覧を提供し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

 次のレジストリエントリの一覧では、 *VS Reg Root* は HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudioの \\ *x. y* と等しくなります。ここで、 *x.y* は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] バージョン番号です。

## <a name="registry-entries-for-language-service-options"></a>言語サービスオプションのレジストリエントリ
 *VS Reg Root*\Languages\Language Services \\ *言語名* キーには、次の値を含めることができます。

|Name|Type|Range|Description|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|*\<GUID>*|言語サービスの GUID。|
|LangResID|REG_DWORD|0x0-0xffff|言語のローカライズされたテキスト名の文字列リソース識別子 (ResID)。|
|パッケージ|REG_SZ|*\<GUID>*|VSPackage の GUID。|
|ShowCompletion|REG_DWORD|0-1|[**オプション**] ダイアログボックスの [**ステートメント入力候補**] オプションを有効にするかどうかを指定します。|
|ShowSmartIndent|REG_DWORD|0-1|[**オプション**] ダイアログボックスで **スマート** インデントを選択するオプションを有効にするかどうかを指定します。|
|RequestStockColors|REG_DWORD|0-1|キーワードに色を設定するために、カスタム色と既定の色のどちらを使用するかを指定します。|
|Sho, Turls|REG_DWORD|0-1|ユーザーが Url をクリックできるかどうかを指定します。|
|非ホット Url の既定値|REG_DWORD|0-1|[**オプション**] ダイアログボックスの **[シングルクリックでの URL ナビゲーションを有効にする**] オプションの初期設定を指定します。|
|DefaultToInsertSpaces|REG_DWORD|0-1|言語サービスの既定のタブオプションとして "スペースの挿入" があるかどうかを指定します。|
|ShowDropdownBarOption|REG_DWORD|0-1|**ナビゲーションバー** を表示または非表示にする [**オプション**] ダイアログボックスの [**ナビゲーションバー** ] オプションを有効または無効にします。|
|単一のコードウィンドウのみ|REG_DWORD|0-1|言語サービスの [**ウィンドウ**] メニューで選択できる **新しいウィンドウ** を有効または無効にします。|
|Enableadvanced Membersoption|REG_DWORD|0-1|**[詳細メンバーを非表示** にする] の [**オプション**] ダイアログボックスの設定を有効または無効にします。|
|サポート CF_HTML|REG_DWORD|0-1|エディターで HTML データのコピーと貼り付けを有効にするかどうかを指定します。|
|EnableLineNumbersOption|REG_DWORD|0-1|言語サービスで [**オプション**] ダイアログボックスの [**行番号**] オプションを有効にするかどうかを指定します。|
|Hideadvanced Membersデフォルト|REG_DWORD|0-1|プライベートフィールドなどの高度なメンバーを入力候補一覧で非表示にするかどうかを指定します。|
|ShowBraceCompletion|REG_DWORD|0-1|[**オプション**] ダイアログボックスの [中 **かっこの完了**] オプションを有効にするかどうかを指定します。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      C/C++\
        (Default)             = reg_sz:{B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}
        LangResID             = reg_dword:0x00000000
        Package               = reg_sz:{8C2EA640-ABC1-11D0-9D62-00C04FD9DFD9}
        ShowCompletion        = reg_dword:0x00000001
        ShowSmartIndent       = reg_dword:0x00000001
        ShowDropdownBarOption = reg_dword:0x00000001
```

## <a name="registry-entries-for-debugger-languages-options"></a>デバッガー言語オプションのレジストリエントリ
 *VS Reg Root*\Languages\Language Services の \\ *言語名*\ デバッガー言語 \\ *GUID*\ キーには、次の値を含めることができます。

|Name|Type|Range|Description|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|text|既定値を使用して、言語の名前を文書化できます。 このキーの名前は、式エバリュエーターの GUID であり、\ ad7metricor 式エバリュエーターに対応するエントリが含まれてい *\<VS Reg Root>* ます。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      C/C++\
        Debugger Languages\
          {3A12D0B7-C26C-11D0-B442-00A0244A1DD2}\
            (Default) = reg_sz:C++
```

## <a name="registry-entries-for-editor-tools-options"></a>エディターツールオプションのレジストリエントリ
 レジストリキーは、プロパティページとプロパティノードの EditorToolsOptions キーの下に追加できます。 これらのキーとその値は、言語サービスを構成するために使用される [ **オプション** ] ダイアログボックス ([ **ツール** ] メニュー) のプロパティページを識別します。 次の例では、 *Page name* はプロパティページの名前、 *node Name* は [ **オプション** ] ダイアログボックスのツリー内のノードの名前です。 ページエントリとノードエントリを別々に指定する必要があります。

|Name|Type|Range|Description|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|ResID|このオプションページのローカライズされた表示名。 名前には、リテラルテキストまたは # `nnn` を `nnn` 指定できます。ここで、は、指定された VSPackage のサテライト DLL 内の文字列リソース ID です。|
|パッケージ|REG_SZ|*GUID*|このオプションページを実装する VSPackage の GUID。|
|ページ|REG_SZ|*GUID*|メソッドを呼び出すことによって、VSPackage から要求するプロパティページの GUID <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> 。 このレジストリエントリが存在しない場合、レジストリキーはページではなくノードを記述します。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      CSharp\
        EditorToolsOptions\
          Formatting\
            (Default) = reg_sz:#242
            Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
            General\
              (Default) = reg_sz:#255
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
              Page      = reg_sz:{3EB2CC0B-033E-4D75-B26A-B2362C25227E}
            Indentation\
              (Default) = reg_sz:#250
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
              Page      = reg_sz:{5E21D017-6D2A-4114-A1F1-C923F001CBBB}
            Newlines\
              (Default) = reg_sz:#253
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
              Page      = reg_sz:{607D8062-68D1-41E4-9A35-B5E7F14D0481}
```

## <a name="registry-entries-for-file-name-extension-options"></a>ファイル名拡張子オプションのレジストリエントリ
 ファイル拡張子のエントリには、先頭のピリオド ("myext" など) を含める必要があります。

|Name|Type|Range|Description|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|*GUID*|このファイル名拡張子の種類の既定の言語サービスのサービス GUID。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    File Extensions\
      .cpp\
        (Default) = {B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}
```

## <a name="registry-entries-for-editor-options"></a>エディターオプションのレジストリエントリ
 *VS Reg Root* エディターキーには、次の値を含めることができます。

|Name|Type|Range|Description|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|""|未使用ここで、ドキュメントの名前を入力できます。|
|DefaultToolboxTab|REG_SZ|""|エディターがアクティブなときに既定で作成されるツールボックスタブの名前。|
|DisplayName|REG_SZ|ResID|[ **ファイルを開くアプリケーション** の選択] ダイアログボックスに表示する名前。 名前は、文字列リソース ID または標準形式の名前です。|
|ExcludeDefTextEditor|REG_DWORD|0-1|[ **ファイルを開くアプリケーションの表示** ] コマンドで使用します。 特定のファイルの種類で使用可能なエディターの一覧に既定のテキストエディターを表示しない場合は、この値を1に設定します。|
|LinkedEditorGUID|REG_SZ|*\<GUID>*|コードページをサポートするファイルを開くことができるすべての言語サービスに使用されます。 たとえば、 **Open with** コマンドを使用して .txt ファイルを開くと、エンコードなしでソースコードエディターを使用するためのオプションが用意されています。<br /><br /> サブキーの名前に指定された GUID は、コードページエディターファクトリ用です。この特定のレジストリエントリで指定されているリンクされた GUID は、通常のエディターファクトリ用です。 このエントリの目的は、IDE が既定のエディターを使用してファイルを開いていない場合、IDE が一覧の次のエディターを使用しようとすることです。 このエディターファクトリは、基本的には失敗したエディターファクトリと同じであるため、次のエディターはコードページエディターファクトリにしないでください。|
|パッケージ|REG_SZ|*\<GUID>*|表示名の ResID の VSPackage GUID。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  \Editors\
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\
      (Default)            = reg_sz:Html Editor with Encoding
      DefaultToolboxTab    = reg_sz:HTML
      DisplayName          = reg_sz:#20101
      LinkedEditorGUID     = reg_sz:{C76D83F8-A489-11D0-8195-00A0C91BBEE3}
      Package              = reg_sz:{1B437D20-F8FE-11D2-A6AE-00104BCC7269}
```

## <a name="registry-entries-for-logical-view-options"></a>論理ビューオプションのレジストリエントリ
 *VS Reg Root* \\ *エディターエディターの GUI>* \ logicalviews キーには、次の値を含めることができます。

|Name|Type|Range|Description|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ||未使用。|
|*\<GUID>*|REG_SZ|""|サポートされている論理ビューのキー。 これらの数は必要な数だけ持つことができます。 レジストリエントリの名前は、値ではなく、常に空の文字列である重要なものです。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  \Editors\
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\
      LogicalViews\
       (Default) = reg_sz:
       {7651a700-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
       {7651a701-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
       {7651a702-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
       {7651a703-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
```

## <a name="registry-entries-for-editor-extension-options"></a>エディター拡張機能のオプションのレジストリエントリ
 *VS Reg Root* エディターエディターの \\ *GUID*\ Extensions キーには、次の値を含めることができます。 ファイル名の拡張子には、先頭のピリオドは含まれません。

|Name|Type|Range|Description|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ||未使用。|
|*\<ext>*|REG_DWORD|0-0xffffffff|拡張機能の相対的な優先順位。 複数の言語で同じ拡張機能が共有されている場合は、優先度の高い言語が選択されます。|

 また、エディターの現在のユーザーの既定の選択は、HKEY_Current_User \Software\Microsoft\VisualStudio の \\ 既定のエディター \\ *ext* に格納されます。選択された言語サービスの GUID は、カスタムエントリに含まれています。 これは、現在のユーザーに対して優先されます。

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\
  \Editors\
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\
      Extensions\
       (Default) = reg_sz:
       *         = reg_dword:0x00000018
       html      = reg_dword:0x00000027
       shtm      = reg_dword:0x00000027
       shtml     = reg_dword:0x00000027
```

## <a name="registry-entries-for-managed-package-framework-language-service-options"></a>Managed Package Framework 言語サービスオプションのレジストリエントリ
 次のレジストリエントリは、managed package framework (MPF) 言語サービスクラスに固有のものです。 これらのレジストリエントリは、さまざまな IntelliSense 機能や、その他の高度な編集機能の言語サービスでのサポートを示しています。

 これらのレジストリエントリには、クラスを使用してアクセス <xref:Microsoft.VisualStudio.Package.LanguagePreferences> します。

|Name|Type|Range|Description|
|----------|----------|-----------|-----------------|
|CodeSense|REG_DWORD|0-1|IntelliSense 操作のサポート。|
|MatchBraces|REG_DWORD|0-1|かっこ、かっこ、および角かっこなどの一致する言語のペアのサポート。|
|QuickInfo|REG_DWORD|0-1|IntelliSense のクイックヒント操作のサポート。|
|ShowMatchingBrace|REG_DWORD|0-1|一致する言語ペアをステータスバーに表示するためのサポート。|
|MatchBracesAtCaret|REG_DWORD|0-1|一致する言語のペアを表示するためのサポート。通常は、2つの要素を強調表示します。|
|MaxErrorMessages|REG_DWORD|0-n|**エラー一覧** ウィンドウに表示できるエラーの最大数。|
|方法 Ensedelay|REG_DWORD|0-n|IntelliSense 操作のバックグラウンド解析を開始するまでの遅延時間 (ミリ秒単位)。|
|EnableAsyncCompletion|REG_DWORD|0-1|バックグラウンド解析のサポート。|
|EnableCommenting|REG_DWORD|0-1|選択したテキストブロックのコメント化をサポートします。また、選択したテキストのコメント解除のサポートも意味します。|
|EnableFormatSelection|REG_DWORD|0-1|自動インデントや中かっこの位置の調整などのテキストの書式設定をサポートします。|
|AutoOutlining|REG_DWORD|0-1|アウトライン (折りたたまれる可能性のある領域) のサポート。|
|MaxRegions|REG_DWORD|0-n|ファイルごとの非表示領域の最大数。|

```
ExampleHKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      XML\
        (Default)             = reg_sz:{f6819a78-a205-47b5-be1c-675b3c7f0b8e}
        MatchBraces           = reg_dword:0x00000001
        QuickInfo             = reg_dword:0x00000001
        ShowMatchingBrace     = reg_dword:0x00000001
        MatchBracesAtCaret    = reg_dword:0x00000000
        MaxErrorMessages      = reg_dword:0x00000064
        CodeSenseDelay        = reg_dword:0x000001f4
        MaxRegions            = reg_dword:0x0000000a
```

## <a name="see-also"></a>こちらもご覧ください
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
