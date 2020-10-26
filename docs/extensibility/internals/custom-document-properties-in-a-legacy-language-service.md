---
title: 従来の言語サービスでのカスタムドキュメントプロパティ
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom document properties, language services [managed package framework]
- document properties, custom
- language services [managed package framework], custom document properties
ms.assetid: cc714a67-b33e-4440-9203-3c90f648bd9c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3c38ad28456ab8b9bccf29d2249307b718a5767b
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90036835"
---
# <a name="custom-document-properties-in-a-legacy-language-service"></a>従来の言語サービスでのカスタムドキュメントプロパティ
ドキュメントのプロパティは、[ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **プロパティ** ] ウィンドウに表示できます。 プログラミング言語には、通常、個々のソースファイルに関連付けられたプロパティはありません。 ただし、XML では、エンコード、スキーマ、およびスタイルシートに影響するドキュメントプロパティがサポートされています。

## <a name="discussion"></a>考察 (Discussion)
 言語にカスタムドキュメントプロパティが必要な場合は、クラスからクラスを派生させ、 <xref:Microsoft.VisualStudio.Package.DocumentProperties> 派生クラスに必要なプロパティを実装する必要があります。

 また、通常、ドキュメントのプロパティはソースファイル自体に格納されます。 そのためには、言語サービスでソースファイルからプロパティ情報を解析して [ **プロパティ** ] ウィンドウに表示し、[ **プロパティ** ] ウィンドウでドキュメントプロパティが変更されたときにソースファイルを更新する必要があります。

## <a name="customize-the-documentproperties-class"></a>DocumentProperties クラスをカスタマイズする
 カスタムドキュメントプロパティをサポートするには、クラスからクラスを派生させ、 <xref:Microsoft.VisualStudio.Package.DocumentProperties> 必要な数だけプロパティを追加する必要があります。 また、[ **プロパティ** ] ウィンドウの表示で整理するためのユーザー属性も指定する必要があります。 プロパティがアクセサーだけを持つ場合 `get` は、[ **プロパティ** ] ウィンドウに読み取り専用として表示されます。 プロパティにアクセサーとアクセサーの両方がある場合 `get` `set` 、プロパティは [ **プロパティ** ] ウィンドウでも更新できます。

### <a name="example"></a>例
 から派生したクラスの例を次に示し <xref:Microsoft.VisualStudio.Package.DocumentProperties> ます。2つのプロパティとを示し `Filename` `Description` ます。 プロパティが更新されると、クラスのカスタムメソッド <xref:Microsoft.VisualStudio.Package.LanguageService> が呼び出され、プロパティがソースファイルに書き込まれます。

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestDocumentProperties : DocumentProperties
    {
        private string m_filename;
        private string m_description;

        public TestDocumentProperties(CodeWindowManager mgr)
            : base(mgr)
        {
        }

        // Helper function to initialize this property without
        // going through the FileName property (which does a lot
        // more than we need when the filename is set).
        public void SetFileName(string filename)
        {
            m_filename = filename;
        }

        // Helper function to initialize this property without
        // going through the Description property (which does a lot
        // more than we need when the description is set).
        public void SetDescription(string description)
        {
            m_description = description;
        }

        ////////////////////////////////////////////////////////////
        // The document properties

        [CategoryAttribute("General")]
        [DescriptionAttribute("Name of the file")]
        [DisplayNameAttribute("Filename")]
        public string FileName
        {
            get { return m_filename; }
            set
            {
               if (value != m_filename)
               {
                    m_filename = value;
                    SetPropertyValue("Filename", m_filename);
               }
            }
        }

        [CategoryAttribute("General")]
        [DescriptionAttribute("Description of the file")]
        [DisplayNameAttribute("Description")]
        public string Description
        {
            get { return m_description; }
            set
            {
                if (value != m_description)
                {
                    m_description = value;
                    SetPropertyValue("Description", m_description);
                }
            }
        }

        ///////////////////////////////////////////////////////////
        // Private methods.

        private void SetPropertyValue(string propertyName, string propertyValue)
        {
            Source src = this.GetSource();
            if (src != null)
            {
                TestLanguageService service = src.LanguageService as TestLanguageService;
                if (service != null)
                {
                    // Set the property in to the source file.
                    service.SetPropertyValue(src, propertyName, propertyValue);
                }
            }
        }
    }
}
```

## <a name="instantiate-the-custom-documentproperties-class"></a>カスタム DocumentProperties クラスのインスタンスを作成する
 カスタムドキュメントプロパティクラスをインスタンス化するには、クラスのバージョンのメソッドをオーバーライドして、 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> クラスの単一のインスタンスを返す必要があり <xref:Microsoft.VisualStudio.Package.DocumentProperties> ます。

### <a name="example"></a>例

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestLanguageService : LanguageService
    {
        private TestDocumentProperties m_documentProperties;

        public override DocumentProperties CreateDocumentProperties(CodeWindowManager mgr)
        {
            if (m_documentProperties == null)
            {
                m_documentProperties = new TestDocumentProperties(mgr);
            }
            return m_documentProperties;
        }
    }
}
```

## <a name="properties-in-the-source-file"></a>ソースファイル内のプロパティ
 通常、ドキュメントのプロパティはソースファイルに固有であるため、値はソースファイル自体に格納されます。 これらのプロパティを定義するには、言語パーサーまたはスキャナーからのサポートが必要です。 たとえば、XML ドキュメントのプロパティは、ルートノードに格納されます。 ルートノードの値は、[ **プロパティ** ] ウィンドウの値が変更されると変更され、ルートノードはエディターで更新されます。

### <a name="example"></a>例
 この例では、 `Filename` `Description` ソースファイルの最初の2行に、次のように、特殊なコメントヘッダーに埋め込まれたプロパティとを格納します。

```
//!Filename = file.testext
//!Description = A sample file
```

 この例では、ソースファイルの最初の2行からドキュメントのプロパティを取得して設定するために必要な2つのメソッド、およびユーザーがソースファイルを直接変更した場合のプロパティの更新方法を示します。 `SetPropertyValue`ここで示した例のメソッドは、 `TestDocumentProperties` 「 *DocumentProperties クラスのカスタマイズ*」セクションで示すように、クラスから呼び出されたものと同じです。

 この例では、スキャナーを使用して、最初の2行のトークンの種類を判別します。 この例は、説明を目的としたものです。 この状況に対する一般的なアプローチでは、ソースファイルを解析ツリーと呼びます。ツリーの各ノードには、特定のトークンに関する情報が含まれています。 ルートノードには、ドキュメントのプロパティが含まれます。

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    // TokenType.Comment is the last item in that enumeration.
    public enum TestTokenTypes
    {
        DocPropertyLine = TokenType.Comment + 1,
        DocPropertyName,
        DocPropertyAssign,
        DocPropertyValue
    }

    class TestLanguageService : LanguageService
    {
        // Search this many lines from the beginning for properties.
        private static int maxLinesToSearch = 2;

        private TestDocumentProperties m_documentProperties;

        // Called whenever a full parsing operation has completed.
        public override void OnParseComplete(ParseRequest req)
        {
            if (m_documentProperties != null)
            {
                Source src = GetSource(req.View);
                if (src != null)
                {
                    string value = GetPropertyValue(src, "Filename");
                    m_documentProperties.SetFileName(value);

                    value = GetPropertyValue(src, "Description");
                    m_documentProperties.SetDescription(value);

                    // Update the Properties Window.
                    m_documentProperties.Refresh();
                }
            }
        }

        // Retrieves the specified property value from the given source.
        public string GetPropertyValue(Source src, string propertyName)
        {
            string propertyValue = "";

            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    string      line;
                    TokenInfo[] lineInfo = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line.
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                for ( ;
                                     tokenIndex < lineInfo.Length;
                                     tokenIndex++)
                                {
                                    if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyValue)
                                    {
                                        break;
                                    }
                                }
                                if (tokenIndex < lineInfo.Length)
                                {
                                    propertyValue = src.GetText(i,
                                                          lineInfo[tokenIndex].StartIndex,
                                                          i,
                                                          lineInfo[tokenIndex].EndIndex + 1);
                                }
                                break;
                            }
                        }
                    }
                }
            }
            return propertyValue;
        }

        // Sets the specified property into the given source file.
        // Called from the TestDocumentProperties class.
        public void SetPropertyValue(Source src, string propertyName, string propertyValue)
        {
            string newLine;

            if (propertyName == null || propertyName == "")
            {
                // No property name, so nothing to do
                return;
            }
            if (propertyValue == null)
            {
                propertyValue = "";
            }
            // This is the line to be inserted.
            newLine = String.Format("//!{0} = {1}", propertyName, propertyValue);

            // First, find the line on which the property belongs.
            // If line is found, replace it.
            // Otherwise, insert the line at the beginning of the file.
            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    int         lineNumber = -1;
                    string      line;
                    TokenInfo[] lineInfo   = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                lineNumber = i;
                                break;
                            }
                        }
                    }

                    // Set up an undo context that also handles the insert/replace.
                    EditArray editArray = new EditArray(src,
                                                        true,
                                                        "Update Property");
                    if (editArray != null)
                    {
                        TextSpan span = new TextSpan();
                        if (lineNumber != -1)
                        {
                            // Replace line.
                            int lineLength = 0;
                            src.GetTextLines().GetLengthOfLine(lineNumber,
                                                               out lineLength);
                            span.iStartLine  = lineNumber;
                            span.iStartIndex = 0;
                            span.iEndLine    = lineNumber;
                            span.iEndIndex   = lineLength;
                        }
                        else
                        {
                            // Insert new line.
                            span.iStartLine  = 0;
                            span.iStartIndex = 0;
                            span.iEndLine    = 0;
                            span.iEndIndex   = 0;
                            newLine += "\n";
                        }
                        editArray.Add(new EditSpan(span, newLine));
                        editArray.ApplyEdits();
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>参照
- [従来の言語サービス機能](../../extensibility/internals/legacy-language-service-features1.md)
