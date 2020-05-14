---
title: レガシ言語サービスの登録2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, language services
- language services, registry information
- registry, language services
ms.assetid: ca312aa3-f9f1-4572-8553-89bf3a724deb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2d9d13f301f6c04c0f7b14cc8c685f08b072ef84
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705885"
---
# <a name="registering-a-legacy-language-service"></a>従来の言語サービスの登録
以下のセクションでは、 で使用できるさまざまな言語サービス オプションのレジストリ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]エントリの一覧を示します。

 次のレジストリ エントリの一覧では *、VS Reg ルート*は HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\\\VisualStudio*X.Y*に等[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]しく *、X.Y*はバージョン番号です。

## <a name="registry-entries-for-language-service-options"></a>言語サービス オプションのレジストリ エントリ
 *VS Reg ルート*\言語\\\言語サービス*言語サービス言語名*キーには、次の値を含めることができます。

|名前|種類|範囲|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|*\<GUID>*|言語サービスの GUID。|
|ラングレスID|REG_DWORD|0x0-0xffff|ローカライズされた言語のテキスト名の文字列リソース識別子 (ResID)。|
|Package|REG_SZ|*\<GUID>*|VS パッケージの GUID。|
|ショー完了|REG_DWORD|0-1|[オプション] ダイアログ ボックスの **[ステートメント補完****] オプション**を有効にするかどうかを指定します。|
|スマートインデントを表示します。|REG_DWORD|0-1|**[オプション]** ダイアログ ボックスで **[スマート**インデント] を選択するオプションを有効にするかどうかを指定します。|
|リクエストストックカラー|REG_DWORD|0-1|キーワードの色付けにカスタムカラーまたはデフォルトカラーを使用するかどうかを指定します。|
|ショーホトルズ|REG_DWORD|0-1|ユーザーが URL をクリックできるかどうかを指定します。|
|既定の非ホット URL|REG_DWORD|0-1|**[オプション]** ダイアログ ボックスの **[シングル クリック URL ナビゲーションを有効にする**] オプションの初期設定を指定します。|
|スペースを挿入するデフォルト|REG_DWORD|0-1|言語サービスに、既定のタブ オプションとして "挿入スペース" を使用するかどうかを指定します。|
|ドロップダウンバーオプション|REG_DWORD|0-1|**ナビゲーション バー**の表示/非表示を切り替える **[オプション]** ダイアログ ボックスの [ナビゲーション**バー**] オプションを有効または無効にします。|
|単一コード ウィンドウのみ|REG_DWORD|0-1|言語サービスの [ウィンドウ] メニューの**Window** **[新しいウィンドウ**] の選択を有効または無効にします。|
|詳細メンバーを有効にするオプション|REG_DWORD|0-1|[**詳細メンバを隠す**] の **[オプション]** ダイアログ ボックスの設定を有効または無効にします。|
|サポートCF_HTML|REG_DWORD|0-1|エディターで HTML データのコピーと貼り付けが可能かどうかを指定します。|
|ライン番号オプションを有効にする|REG_DWORD|0-1|言語サービスの [**オプション]** ダイアログ ボックスの **[行番号**] オプションを有効にするかどうかを指定します。|
|既定で詳細メンバーを非表示にする|REG_DWORD|0-1|入力候補リストで、プライベート フィールドなどの詳細メンバを非表示にするかどうかを指定します。|
|ショーブレイスコンプリート|REG_DWORD|0-1|**[オプション]** ダイアログ ボックスの **[中かっこの補完**] オプションを有効にするかどうかを指定します。|

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

## <a name="registry-entries-for-debugger-languages-options"></a>デバッガ言語オプションのレジストリ エントリ
 *VS Reg ルート*\言語\\\言語サービス*言語名*\\\デバッガー言語*GUID*\ キーには、次の値を含めることができます。

|名前|種類|範囲|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|text|既定値は、言語の名前を文書化するために使用できます。 このキーの名前は*\<、VS Reg ルート>* \AD7Metrics\式エバリュエーターに対応するエントリを持つ式エバリュエーターの GUID です。|

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

## <a name="registry-entries-for-editor-tools-options"></a>エディタ ツール オプションのレジストリ エントリ
 プロパティ ページとプロパティ ノードの [エディタツール] オプション キーの下にレジストリ キーを追加できます。 これらのキーとその値は、言語サービスの構成に使用される **[オプション]** ダイアログ ボックス **([ツール**] メニュー) のプロパティ ページを識別します。 次の例では、*ページ名*はプロパティ ページの名前で、[*ノード名]* は **[オプション]** ダイアログ ボックスのツリー内のノードの名前です。 ページ項目とノード項目は別々に指定する必要があります。

|名前|種類|範囲|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|レシドID|このオプション ページのローカライズされた表示名。 名前はリテラル テキストまたは #`nnn`を`nnn`指定した VSPackage のサテライト DLL 内の文字列リソース ID です。|
|Package|REG_SZ|*Guid*|このオプション ページを実装する VSPackage の GUID。|
|ページ|REG_SZ|*Guid*|メソッドを呼び出すことによって VSPackage から要求するプロパティ<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>ページの GUID。 このレジストリ エントリが存在しない場合、レジストリ キーはページではなくノードを示します。|

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

## <a name="registry-entries-for-file-name-extension-options"></a>ファイル名拡張子オプションのレジストリ エントリ
 ファイル拡張子のエントリには、先頭のピリオド (".myext" など) を含める必要があります。

|名前|種類|範囲|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|*Guid*|このファイル名拡張子の種類の既定の言語サービスのサービス GUID です。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    File Extensions\
      .cpp\
        (Default) = {B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}
```

## <a name="registry-entries-for-editor-options"></a>エディタ オプションのレジストリ エントリ
 *VS Reg ルート*\Editors キーには、次の値を含めることができます。

|名前|種類|範囲|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|""|未使用。ドキュメント用に名前をここに入力できます。|
|DefaultToolboxTab|REG_SZ|""|エディターがアクティブな場合に既定にするツールボックス タブの名前。|
|DisplayName|REG_SZ|レシドID|**[ファイルを開く**] ダイアログ ボックスに表示する名前。 名前は、文字列リソース ID または標準形式の名前です。|
|テキスト エディターを除外します。|REG_DWORD|0-1|[ファイルを**開く**] メニュー コマンドに使用します。 特定のファイルタイプで使用可能なエディタのリストにデフォルトのテキストエディタを表示しない場合は、この値を 1 に設定します。|
|リンクされたエディター GUID|REG_SZ|*\<GUID>*|コードページをサポートするファイルを開くことができるすべての言語サービスに使用されます。 たとえば、[**ファイルから開く**] コマンドを使用して .txt ファイルを開くと、エンコードの有無にかかわらずソース コード エディターを使用するためのオプションが提供されます。<br /><br /> サブキーの名前で指定された GUID は、コード ページ エディター ファクトリ用です。この特定のレジストリ エントリで指定されたリンクされた GUID は、通常のエディター ファクトリ用です。 このエントリの目的は、IDE が既定のエディターを使用してファイルを開かない場合、IDE は、リスト内の次のエディターを使用しようとします。 このエディター ファクトリは基本的に、失敗したエディター ファクトリと同じなので、この次のエディターはコード ページ エディター ファクトリにしないでください。|
|Package|REG_SZ|*\<GUID>*|表示名の ResID の VSPackage GUID。|

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

## <a name="registry-entries-for-logical-view-options"></a>論理ビュー オプションのレジストリ エントリ
 *VS Reg ルート*\\\*エディタ エディタの GUI>* \LogicalViews キーには、次の値を含めることができます。

|名前|種類|範囲|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ||未使用。|
|*\<GUID>*|REG_SZ|""|サポートされている論理ビューのキー。 必要なだけ多くのこれらのを持つことができます。 レジストリ エントリの名前は重要な値ではなく、常に空の文字列です。|

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

## <a name="registry-entries-for-editor-extension-options"></a>エディター拡張機能オプションのレジストリ エントリ
 *VS Reg ルート*\\\*エディター エディターの GUID*\拡張キーには、次の値を含めることができます。 ファイル名拡張子には、先頭のピリオドは含まれません。

|名前|種類|範囲|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ||未使用。|
|*\<>*|REG_DWORD|0-0xffffffff|拡張機能の相対的な優先順位。 複数の言語が同じ拡張子を共有する場合は、優先順位の高い言語が選択されます。|

 さらに、現在のユーザーのエディターの既定の選択は\\、HKEY_Current_User\ソフトウェア\\VisualStudio*X.Y*\既定の\\エディターの*ext*に格納されます。選択した言語サービスの GUID は、カスタム エントリにあります。 これは、現在のユーザーに優先されます。

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

## <a name="registry-entries-for-managed-package-framework-language-service-options"></a>管理パッケージ フレームワーク言語サービス オプションのレジストリ エントリ
 次のレジストリ エントリは、管理パッケージ フレームワーク (MPF) 言語サービス クラスに固有です。 これらのレジストリ エントリは、さまざまな IntelliSense 機能およびその他の高度な編集機能の言語サービスでのサポートを示します。

 これらのレジストリ エントリは、クラス<xref:Microsoft.VisualStudio.Package.LanguagePreferences>を通じてアクセスされます。

|名前|種類|範囲|説明|
|----------|----------|-----------|-----------------|
|コードセンス|REG_DWORD|0-1|インテリセンス操作のサポート。|
|マッチブレース|REG_DWORD|0-1|中かっこ、かっこ、かっこなどの言語ペアの一致をサポートします。|
|QuickInfo|REG_DWORD|0-1|IntelliSense クイック ヒント操作のサポート。|
|マッチングブレースを表示します。|REG_DWORD|0-1|ステータス バーに一致する言語ペアを表示するためのサポート。|
|マッチブレイスアットカレト|REG_DWORD|0-1|一致する言語ペアの表示をサポートします 。|
|最大エラー メッセージ|REG_DWORD|0-n|[**エラー一覧**] ウィンドウに表示できるエラーの最大数。|
|コードセンスディレイ|REG_DWORD|0-n|IntelliSense 操作のバックグラウンド解析を開始するまでの遅延時間 (ミリ秒単位)。|
|非同期完了を有効にする|REG_DWORD|0-1|バックグラウンド解析のサポート。|
|コメントを有効にする|REG_DWORD|0-1|選択したテキストブロックをコメントアウトするサポートと、選択したテキストのコメント解除のサポートもサポートします。|
|フォーマット選択を有効にする|REG_DWORD|0-1|自動インデントや中かっこの位置の調整などのテキストの書式設定をサポートします。|
|オートアウトライニング|REG_DWORD|0-1|アウトライン (折りたたむことができる領域) のサポート。|
|最大地域|REG_DWORD|0-n|ファイルごとの隠し領域の最大数。|

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

## <a name="see-also"></a>関連項目
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
