---
layout: default
group: fedg
subgroup: B_Layouts
title: Layout overview
menu_title: Layout
menu_order: 1
menu_node: parent
github_link: frontend-dev-guide/layouts/layout-overview.md
---

<h2>Introduction</h2>

Magento application implements the <a href="http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller" target="_blank">Model-view-controller</a> architecture pattern; meaning, the Magento software is architected into *layers*, including the *view layer*.

The major part of the view layer of Magento application is layout. Functionally, layout is a page structure, represented by hierarchy of elements (element tree), which can be of two types: blocks and containers. Technically, layout is defined in the .xml files, which contain element declarations and element manipulation instructions.

This article describes the basic concepts you need to know to create layouts for your custom theme.

<h2 id="layout-over-terms">Terms used</h2>

<span id="handle">*Layout handle*</span>

A *layout handle* is a uniquely identified set of layout instructions that serves as a name of a layout file.

There are three kinds of layout handles:
page type layout handles –  synonyms of the page type identifiers. Correspond to "full action names" of controller actions, for example, catalog_product_view.
page layout handles – identifiers of specific pages. Correspond to controller actions with parameters that identify specific pages, for example, catalog_product_view_type_simple_id_128.
arbitrary handles. Do not correspond to any page type, but other handles use them by including.

<h2 id="layout_overview_blocks">Basic layout elements</h2>

The basic components of Magento page design are blocks and containers. 

A *container* exists for the sole purpose of assigning content structure to a page. A container has no additional content except the content of included elements. Examples of containers include the header, left column, main column, and footer.

The following figure shows an example:

<img src="{{ site.baseurl }}common/images/layouts_containers_defn.jpg" />

 A *block* represents each feature on a page and employs templates to generate the HTML to insert into its parent structural block. Examples of blocks include a category list, a mini cart, product tags, and product listing.

The following figure shows an example:

<img src="{{ site.baseurl }}common/images/layouts_block_defn.jpg"/>.

<h2>Layout files types and conventions</h2>


<h3>Layout file types: by role</h3>

For a particular page, its layout is defined by two major layout components: *page layout* file and *page configuration* file (or *generic layout* for pages returned in AJAX requests, emails, and so on).

Following are the definitions of each layout file type:

* *Page layout*: an XML file declaring a page wireframe inside the `<body>` section of the HTML page markup, for example, two-column page layout. 
* *Page configuration*: an XML file declaring detailed structure, contents and meta-information of a page (includes the `<html>`, `<head>`, and `<body>` sections of the HTML page markup).
* *Generic layout*: an XML file declaring page detailed structure and contents inside the `body` section of the HTML page markup. Used for pages returned by AJAX requests, emails, HTML snippets, and so on.

For details, refer to <a href="{{site.gdeurl}}frontend-dev-guide/layouts/layout-types.html" target="_blank">Layout file types</a>.

In this guide we use *layout files* when talking about concepts which are similarly applied to all of these types of layout files.

<h3 id="layout-loc">Module and theme layout files</h3>

The following terms are used to distinguish layouts provided by different application components:

* *Base layouts*: Layout files provided by modules. Conventional location: 
	* Page configuration and generic layout files: <code>app/code/&lt;Namespace&gt;/&lt;Module&gt;/view/frontend/layout`</code>
	* Page layout files: <code>app/code/&lt;Namespace&gt;/&lt;Module&gt;/view/frontend/page_layout</code>
* *Theme layouts*: Layout files provided by themes. Conventional location:
	* Page configuration and generic layout files: <code>app/design/frontend/&lt;Vendor&gt;/&lt;theme&gt;/&lt;Namespace&gt;_&lt;Module&gt;/layout</code>
	* Page layout files: <code>app/design/frontend/&lt;Vendor&gt;/&lt;theme&gt;/&lt;Namespace&gt;_&lt;Module&gt;/page_layout</code>


<h2 id="layout-custom">Customize layout</h2>

To ensure stability and secure your customizations from being deleted during upgrade, do not change out-of-the-box Magento module and theme layouts.

To make the necessary changes, create <a href="{{site.gdeurl}}frontend-dev-guide/layouts/layout-extend.html" target="_blank">extending</a> and <a href="{{site.gdeurl}}frontend-dev-guide/layouts/layout-override.html" target="_blank">overriding</a> layout files in your custom theme. 

<h2 id="layout_processing">Layout files processing</h2>


The Magento application processes layout files in the following order:

1.	Collects all layout files from modules. The order is determined by the modules order in the module list from `app/etc/config.php`.
2.	Determines the sequence of <a href="{{site.gdeurl}}frontend-dev-guide/themes/theme-inherit.html" target="_blank">inherited</a> themes `[<parent_theme>, ..., <parent1_theme>] <current_theme>`
3.	Iterates the sequence of themes from last ancestor to current:

	a.	Adds all extending theme layout files to the list.

	b.	Replaces overridden layout files in the list.


1.	Merges all layout files from the list.

<div class="bs-callout bs-callout-info" id="info">
  <p>Layout files that belong to inactive modules or modules with disabled output are ignored.</p>
</div>



#### Related topics:

*	<a href="{{ site.gdeurl }}frontend-dev-guide/layouts/xml-instructions.html" target="_blank">Layout instructions</a>
*	<a href="{{ site.gdeurl }}frontend-dev-guide/layouts/xml-manage.html" target="_blank">Common layout customization tasks</a>
*	<a href="{{ site.gdeurl }}frontend-dev-guide/layouts/layout-extend.html" target="_blank">Extend a layout</a>
*	<a href="{{ site.gdeurl }}frontend-dev-guide/layouts/layout-override.html" target="_blank">Override a layout</a>
*	<a href="{{ site.gdeurl }}frontend-dev-guide/layouts/layout-practice.html" target="_blank">Customizing layout - step-by-step illustration</a>



