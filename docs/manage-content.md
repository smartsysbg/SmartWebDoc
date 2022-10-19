#
This chapter describes the admin interface related to content management. The **SmartWEB** admin interface, also known as the `Back-End` or `Admin Panel`, is essentially the control panel for the entire website. The `Admin Panel` is the interface where administrators and other site officials with appropriate privileges can create and manage content, change functionality and styling and etc. The [Admin Interface Overview](/admin-interface-overview) chapter provides a brief overview of all the administration options, with links to chapters with in-depth descriptions.  

## Content Management

Navigate to the `Dashboard` via the user options in the top-right of the page.  

![](./media/manage-content/user-dashboard.png)

All of the `Content Types` that the current user can use to create content are on the left side of the page, located under the `NEW` dropdown list. The administrator of course sees all `Content Types`. In the picture below, there are only four `Content Types` that users can use to create `Content Items`. The [Content Anatomy](/content-anatomy/#content-type) chapter describes what the `Content Types` is and what the `Content Item` is. The [Users and Roles](/users-and-roles) chapter describes how to create roles with limited access to the site's administrative options and also limited access to the `Content Types`.  

![](./media/manage-content/content-types.png)

Under available content types, there is a `Content` link as shown in the previous picture. This link leads to the `Manage Content` section shown in the next picture. Here content can be viewed, searched, created and edited. All available `Content Items` (pages) can be found here. On the right side of each `Content Item` there are list of actions allowed for that `Content Item`.  

![](./media/manage-content/Screenshot_3.png)


The actions which users can perform on `Content Items` will depend on the permissions their role has ([Users and Roles](/Users-and-Roles)). The administrator has unlimited access to every `Content item` and can perform every action. These actions include:

* `Preview` – preview an unpublished version of the `Content Item`.

* `View` –  view a published version of the `Content Item`.

* `Save` - save the current version of the `Content Item` without publishing it.

* `Publish` – save the current version of the `Content Item` and publish it.

* `Publish Later` - schedule the publication of `Content Item` for a future time by setting a date and time

* `Publish Draft` –  publish a draft.

* `Unpublish` – convert a published `Content Item` into a draft.

* `Clone` – clone the `Content Item`.

* `Edit` – edit the `Content Item`.

* `Delete` – delete the `Content Item`.

Users will only have access to two actions on `Content Items` that are not created by them -  `View` and `Clone`.

The following image represents the flow of content and the overall structure that is responsible for its management:

![](./media/manage-content/manage-content.png)

!!! attention "Attention:"
     When a page is published, the `Edit` option will not be available **to users**. If a user has to edit a published page, the page must, first, be converted to a draft via the `Unpublish` action. The user will then be able to edit the page. The **administrators** have the ability to `Edit`, `Save` and `Publish` content without having to `Unpublish` it first. This is represented in the image above via the `Save Published` element.


`Content Items` to which the user has no access will not have any actions displayed. If a short description can be seen, but there are no available actions, this means that the author of the `Content Item` does not have a published version, just a draft. When the draft is published, the user will be able to view the page and clone it. When a page is cloned, the user will receive a copy, which he is the author of. The user can then edit this copy and publish it under his own name.

 
![](./media/manage-content/Screenshot_4.png)

In the case where only the `View` action is available, the content author has a published version of the page, but has started editing a new draft, which is not published yet. In this case, the user can only view the last published version. When the author publishes the draft, the user will be able to clone the latest version.

![](./media/manage-content/Screenshot_5.png)

At the top of the `Manage Content` section, there is toolbar that is used to filter search results. The search results will strictly depend on the user's role. If the role is not authorized to create pages from a specific `Content Type`, results from that `Content Type` will not be returned.


![](./media/manage-content/Screenshot_6.png)

The options that are provided by the toolbar consist of:

* `Show` – filter the pages by `Content Type`. 

* `ordered by` –  select the order in which the search results are returned:

     * `recently created` –  show the most-recently created pages first.

     * `recently modified` – show the most-recently edited pages first.

     * `recently published` – show the most-recently published pages first.

* `filter by` – filter the results by: 

     * `latest` – returns the latest version for each of the pages.

     * `published` –  return only the published versions of the pages.

* `own items only` – (if checked) return only the pages created by the user.
 

## Searching


The system has built-in functionality that provides the ability to index and search `Content Items` (pages) in the application. In the admin panel, navigate to `Content` and select the Search `Tab`.

!!! note "Note:"
      The indexing functionality is provided by enabling the Indexing feature, along with a specific implementation of indexing (Lucene-based is included by default). In addition to the Indexing, the Search feature provides the ability to query the index (by keyword or using Lucene query syntax) to return a list of content items. Visit the [Site Settings](/Site-Settings) chapter for more information on indexing.

![](./media/manage-content/Screenshot_7.png)

There is a selection of ways to search for a `Content Item` (page). The specific fields which represent the search criteria are configured within an index ([Site Settings](/Site-Settings)). For demonstration purposes, some of the ways to search for content will be shown:

!!!note "Note:"
          Due to the nature of indexing, it's good practice to use lowercase when searching for an item.

To look for a  `Content Item` page by its title, simply enter the title in the search box and press the `Search` button. This will return all items that have a title that corresponds to the search criteria. 

![](./media/manage-content/Screenshot_11.png)


Additionally, specific words or phrases, found within a `Content Item` (page), can also be used to locate the specific item. In the example, all of the returned pages contain the word "**report**".

![](./media/manage-content/Screenshot_13.png)

Searching for `Content Items` (pages) can also be done by using the technical name of their `Content Type`. This will return every available item from that **specific** `Content Type`. Example: **unit3**.

![](./media/manage-content/Screenshot_12.png)

Using the authors name as the search criteria is also an option. This will return all available `Content Items` (pages) that are owned by the author, whos name was used in the search. Example: **admin**.

![](./media/manage-content/Screenshot_14.png)

 The [lucene query syntax](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html) can be used to specify the index field that is being used as a search criteria. This will ensure that a specific criteria will be used in the search. In the example, we will search for pages that belong to the `Content Type` with the technical name - unit2. Example: **ltype:unit2**.

![](./media/manage-content/Screenshot_15.png)

!!! attention "Important:"  
      In order for the [lucene query syntax](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html) to be used in the search, the `Do Not Escape Query` option must be checked ([Site Settings](/Site-Settings)).


##Recycle Bin
The `Recycle Bin` tab is an administrator feature that displays the items that are marked for deletion. When a `Content Item` (page) is deleted via the `Delete` action, it is not immediately destroyed, rather, it is moved to the `Recycle Bin` tab, where it can be viewed and restored later. In the admin panel, navigate to `Content`. Then select the `Recycle Bin` tab.

![](./media/manage-content/Screenshot_8.png)

At the top of the tab, there is toolbar that is used to filter search results by `Content Type`. Additionally, the number of items returned can also be selected.
![](./media/manage-content/Screenshot_9.png)

The pages are presented with a brief description, consisting of:

* `Id` - represents the position of the page in the database.

* `route` - the route of the page (used in `urls`).

* `owner` - the owner of the page.

* `date deleted` - the date and time when the page was deleted.

Only two actions are available for the deleted pages:

* `Undelete` -  undelete the page.

* `View` - view the deleted page.

![](./media/manage-content/Screenshot_10.png)

!!!warning "Important"
         When a `Content Item` is undeleted, the system will automatically generate a new `Id` for that item. This will cause changes in indexing, and in the database.