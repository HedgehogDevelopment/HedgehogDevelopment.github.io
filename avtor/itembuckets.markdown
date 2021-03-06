﻿---
title: Item Buckets in Avtor
layout: AvtorLayout
---
<script>
	window.location.replace("https://doc.sitecore.com/users/100/sitecore-experience-platform/en/item-buckets.html");
</script>

## Item Buckets in Avtor
Avtor is designed to make working with content in Item Buckets as easy as other types of Sitecore content. Avtor has a simple search mechanism for locating items in the bucket and when items are found, they are added to the content tree like any other content.

## Finding items in an Item Bucket
When working with items in an Item Bucket, the user is presented with a search box when the item bucket is opened.

![Bucket Search](/Images/Avtor/ItemBuckets_Search.png)

**Please Note:** This search box will only show up if the "View Buckets" check box in the content editor is disabled. This shouldn't be a problem in most cases since this is only available to administrators.

Entering a value into the "Find in bucket" search causes Avtor to add any content items containing the search value into the content tree and editing area.

![Bucket Search Results](/Images/Avtor/ItemBuckets_SearchResults.png)

The content editor can update these items the same way they would update any other items in the content tree.

Performing an additional search will append any newly found items to the list on the tree under the bucket. These additional items will all be availble for editing by the content editor in addition to the previous results.

Pressing the Clear Results button will remove any Items located by the user from the result list under the bucket.

## Creating a Field Set for an item in a bucket
Items in the item buckets may contain fields that are not available in other items in the content tree. To create a field set for these items, search for an item and then right-click on the item and select "Add Field Set". This procedure is the same as [creating a field set](/avtor/fieldsets.html#creating-a-field-set) for any other item.

## Avtor search and Item Buckets
The Avtor search ribbon will search for items in item buckets. When an item bucket is expanded, the bucket will find and highlight the items matching your search criteria.

![Ribbon Search Results](/Images/Avtor/ItemBuckets_RibbonSearch.png)

If the Item Bucket is already showing results, the items containing content found by Avtor Search will automatically be highlighted in the bucket results.