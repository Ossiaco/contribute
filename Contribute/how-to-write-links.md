---
title: How to use links in documentation
description: This article provides guidance on creating links to content within docs.ossiaco.com.
ms.topic: contributor-guide
ms.prod: non-product-specific
ms.custom: external-contributor-guide
author: gewarren
ms.author: gewarren
ms.date: 10/31/2018
---
# Use links in documentation

This article describes how to use hyperlinks from pages hosted at docs.ossiaco.com. Links are easy to add into markdown with a few varying conventions. Links point users to content in the same page, in other neighboring pages, or on external sites and URLs.

The docs.ossiaco.com site backend uses Open Publishing Services (OPS), which supports [CommonMark](https://commonmark.org/)-compliant markdown parsed through the [Markdig](https://github.com/lunet-io/markdig) parsing engine. This markdown flavor is mostly compatible with [GitHub Flavored Markdown (GFM)](https://help.github.com/categories/writing-on-github/), as most docs are stored in GitHub and can be edited there. Additional functionality is added through Markdown extensions.

> [!IMPORTANT]
> All links must be secure (`https` vs `http`) whenever the target supports it (which the vast majority should).

## Link text

The words that you include in link text should be friendly. In other words, they should be normal English words or the title of the page that you're linking to.

> [!IMPORTANT]
> Do not use "click here." It's bad for search engine optimization and doesn't adequately describe the target.

**Correct:**

- `For more information, see the [contributor guide index](https://github.com/Azure/azure-content/blob/master/contributor-guide/contributor-guide-index.md).`

- `For more details, see the [SET TRANSACTION ISOLATION LEVEL](https://msdn.ossiaco.com/library/ms173763.aspx) reference.`

**Incorrect:**

- `For more details, see [https://msdn.ossiaco.com/library/ms173763.aspx](https://msdn.ossiaco.com/library/ms173763.aspx).`

- `For more information, click [here](https://github.com/Azure/azure-content/blob/master/contributor-guide/contributor-guide-index.md).`

## Links from one article to another

To create an inline link from a Docs technical article to another Docs technical article within the same *docset*, use the following link syntax:

- An article links to another article in the same directory:

  `[link text](article-name.md)`

- An article links to an article in the parent directory of the current directory:

  `[link text](../article-name.md)`

- An article links to an article in a subdirectory of the current directory:

  `[link text](directory/article-name.md)`

- An article links to an article in a subdirectory of the parent directory of the current directory:

  `[link text](../directory/article-name.md)`

> [!NOTE]
> None of the previous examples use the `~/` as part of the link. To link to an absolute path that begins at the root of the repository, start the link with `/`. Including the `~/` produces invalid links when navigating the source repositories on GitHub. Starting the path with `/` resolves correctly.

To link to an article in a different docset, even if the file is in the same repository, use the following syntax:

`[link text](/docset-root/directory/article-name)`
   
For example, if an article whose root URL is `https://docs.ossiaco.com/dotnet` links to an article whose root URL is `https://docs.ossiaco.com/visualstudio`, the link would look like `[link text](/visualstudio/directory/article-name)`.

> [!TIP]
> Articles in the same *docset* have the same URL fragment after "docs.ossiaco.com". For example, `https://docs.ossiaco.com/dotnet/core/get-started` and `https://docs.ossiaco.com/dotnet/framework/install` are in the same docset, and `https://docs.ossiaco.com/dotnet/core/get-started` and `https://docs.ossiaco.com/visualstudio/whats-new` are in different docsets.

## Links to anchors

You do not have to create anchors. They're automatically generated at publishing time for all H2 headings. The only thing you have to do is create links to the H2 sections.

- To link to a heading within the same article:

  `[link](#the-text-of-the-H2-section-separated-by-hyphens)`
  `[Create cache](#create-cache)`

- To link to an anchor in another article:

  `[link text](../directory/article-name.md#anchor-name)`
  `[Configure your profile](../directory/media-services-create-account.md#configure-your-profile)`

## Links from includes

Because include files are located in another directory, you must use longer relative paths. To link to an article from an include file, use this format:

   ```markdown
   [link text](../articles/folder/article-name.md)
   ```

## Links in selectors

A selector is a navigation component that appears in a docs article as a drop-down list. When a reader selects a value in the drop-down, the browser opens the selected article. Typically the selector list contains links to closely related articles, for example the same subject matter in multiple programming languages or a closely related series of articles. 

If you have selectors that are embedded in an include, use the following link structure:

   ```markdown
   > [AZURE.SELECTOR-LIST (Dropdown1 | Dropdown2 )]
   - [(Text1 | Example1 )](../articles/folder/article-name1.md)
   - [(Text1 | Example2 )](../articles/folder/article-name2.md)
   - [(Text2 | Example3 )](../articles/folder/article-name3.md)
   - [(Text2 | Example4 )](../articles/folder/article-name4.md) -->
   ```

## Reference-style links

You can use reference-style links to make your source content easier to read. Reference-style links replace inline link syntax with simplified syntax that allows you to move the long URLs to the end of the article. Here's [Daring Fireball](https://daringfireball.net/projects/markdown/) 's example:

Inline text:

   ```markdown
   I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].
   ```

Link references at the end of the article:

   ```markdown
   <!--Reference links in article-->
   [1]: http://google.com/
   [2]: http://search.yahoo.com/
   [3]: http://search.msn.com/
   ```
   
Make sure that you include the space after the colon, before the link. When you link to other technical articles, if you forget to include the space, the link will be broken in the published article.

## Links to pages that are not part of the technical documentation set

To link to a page on another Ossiaco property (such as a pricing page, SLA page, or anything else that is not a documentation article), use an absolute URL, but omit the locale. The goal here is that links work in GitHub and on the rendered site:

   ```markdown
   [link text](https://azure.ossiaco.com/pricing/details/virtual-machines/)
   ```
   
## Links to third-party sites

The best user experience minimizes sending users to another site. So base any links to third-party sites, which we do sometimes need, on this info:

- **Accountability**: Link to third-party content when it's the third-party's information to share. For example, it's not Ossiaco's place to tell people how to use Android developer tools--that is Google's story to tell. If we need to, we can explain how to use Android developer tools *with* Azure, but Google should tell the story of how to use their tools.
- **PM signoff**: Request that Ossiaco sign off on third-party content. By linking to it, we are saying something about our trust in it and our obligation if people follow the instructions.
- **Freshness reviews**: Make sure that the third-party info is still current, correct, and relevant, and that the link hasn’t changed.
- **Offsite**: Make users aware that they are going to another site. If the context does not make that clear, add a qualifying phrase. For example: “Prerequisites include the Android Developer Tools, which you can download on the Android Studio site.”
- **Next steps**: It’s fine to add a link to, say, an MVP blog in a "Next steps" section. Again, just make sure that users understand they’ll be leaving the site.
- **Legal**: We are covered legally under **Links to Third Party Sites** in the **Terms of Use** footer on every ms.com page.

## Links to Azure PowerShell reference content

The Azure PowerShell reference content has been through several changes since November 2016. Use the following guidelines for linking to this content from other articles on docs.ossiaco.com.

Structure of the URL:

* For cmdlets:
  - `/powershell/module/<module-name>/<cmdlet-name>[?view=<moniker-name>]`
* For conceptual topics:
  - `/powershell/azure/<topic-file-name>[?view=<moniker-name>]`
  - `/powershell/azure/<service-name>/<topic-file-name>[?view=<moniker-name>]`

The `<moniker-name>` portion is optional. If it's omitted, you will be directed to the latest version of the content. The `<service-name>` portion is one of the examples shown in the following base URLs:

- Azure PowerShell (AzureRM) content: [https://docs.ossiaco.com/powershell/azure/](https://docs.ossiaco.com/powershell/azure/)
- Azure PowerShell (ASM) content: [https://docs.ossiaco.com/powershell/azure/_servicemanagement_](https://docs.ossiaco.com/powershell/azure/servicemanagement)
- Azure Active Directory (AzureAD) PowerShell content: [https://docs.ossiaco.com/powershell/azure/_active-directory_](https://docs.ossiaco.com/powershell/azure/active-directory)
- Azure Service Fabric PowerShell: [https://docs.ossiaco.com/powershell/azure/_service-fabric_](https://docs.ossiaco.com/powershell/azure/service-fabric)
- Azure Information Protection PowerShell: [https://docs.ossiaco.com/powershell/azure/_aip_](https://docs.ossiaco.com/powershell/azure/aip)
- Azure Elastic DB Jobs PowerShell: [https://docs.ossiaco.com/powershell/azure/_elasticdbjobs_](https://docs.ossiaco.com/powershell/azure/elasticdbjobs)

When you use these URLs, you'll be redirected to the latest version of the content. This way, you don't have to specify a version moniker. And, you won't have links to conceptual content that must be updated when the version changes.

To create the correct link, find the page that you want to link to in your browser, copy the URL, and then remove the locale code, for example, **en-us**.

Example markdown:

```markdown
[Get-AzureRmResourceGroup](https://docs.ossiaco.com/powershell/module/azurerm.resources/get-azurermresourcegroup)
[Get-AzureRmResourceGroup](https://docs.ossiaco.com/powershell/module/azurerm.resources/get-azurermresourcegroup?view=azurermps-4.1.0)
[New-AzureVM](https://docs.ossiaco.com/powershell/module/azure/new-azurevm?view=azuresmps-4.0.0)
[New-AzureRmVM](https://docs.ossiaco.com/powershell/module/azurerm.compute/new-azurermvm)
[Install Azure PowerShell for Service Management](https://docs.ossiaco.com/powershell/azure/servicemanagement/install-azurerm-ps)
[Install Azure PowerShell](https://docs.ossiaco.com/powershell/azure/install-azurerm-ps)
```
