---
title: Editing items with Avtor
layout: AvtorLayout
---

# Avtor Search
Avtor allows the content editor to leverage Sitecore's search capabilities to find items in the content tree. When the user searches for text, the Sitecore content index is queries using the search criteria the user submitted. Items matching the search criteria are highlighted in the content tree.

## Search ribbon bar
The content editor uses the Search ribbon to locate items in the content tree. The search ribbon allows the user to specify the search criteria for the items they are interested in.

![Search ribbon](/Images/Avtor/Search_Ribbon.png)

The five criteria users can use to search Sitecore items are:
- **Contents** - Searches the content index for text values. If any content field contains any part of the text the user has specified in this field, the item is highlighted in the edit pane.
- **Template** - Finds items in the content tree where the item's template contains any part of the text specified in the template field.
- **Edited After** - Any item created or edited after the specified date will be found bysearch
- **Edited Before** - Any item edited before the specified date will be found by search.
- **Edited By** - Any item edited by a content author where the content authors name contains the text would be found by search.

## Viewing search results
When the user searches for content, the search results are shown in the editing pane by highlighting the found items.

![Search results](/Images/Avtor/Search_Results.png)

The above screen shows how search results are indicated in the editing pane. The items highlighted in blue are items matching the search criteria.

Some items may contain a magnifying glass ![Child results](/Images/Avtor/Icon_ChildResults.png) next to the name in the content tree. This icon is present when child items under a collapsed item match the search criteria.

## Search Results in Item Buckets
When content in an item bucket matches the search criteria, the items will be displayed under the item bucket search box and automatically highlighted. Please see [item buckets](/avtor/itembuckets.html) for more information.