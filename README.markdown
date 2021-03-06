# Mo' Variables #

Adds many useful global variables and conditionals to use in your templates.

## Installation

* Copy the /system/expressionengine/third_party/mo_variables/ folder to your /system/expressionengine/third_party/ folder
* Activate extensions and enable the Mo' Variables extension
* Go to extension settings and enable the Mo' Variables that you want to use

## Usage

* Ajax Detect Conditional: {if ajax}
* Secure SSL/HTTPS Conditional and Variable: {if secure} {secure_site_url}
* GET: {get:your_key} or {embed:get:your_key}
* GET and POST: {get_post:your_key} or {embed:get_post:your_key}
* POST: {post:your_key} or {embed:post:your_key}
* Cookies: {cookie:your_key} or {embed:cookie:your_key}
* Page Tracker: {last_page}, {one_page_ago}, {two_pages_ago}, {three_pages_ago}, {four_pages_ago}, {five_pages_ago}
* Reverse Segments: {rev_segment_1}, {rev_segment_2}, etc.
* Segments Starting From X: {segments_from_1}, {segments_from_2}, etc.
* Pagination Detect Conditional and Page Offset: {if paginated}, {page_offset}
* Archive Detect Conditional (detects presence of year, month, date in URI): {if archive} {if yearly_archive} {if monthly_archive} {if daily_archive}
* Theme Folder URL: {theme_folder_url}
* Current Page URL: {current_url}, {uri_string}

For the get, post, get_post, and cookie variables, you can use the {embed:xxx:your_key} syntax, which will prevent unparsed tags when there is no key matching "your_key".

## Change Log

#### v1.0.6

-   removed {current_page} variable in Page Tracker, conflicts with the variable of the same name in paginate tag pair (sorry to anyone who used {current_page})

#### v1.0.5

-   fixed bug where if your DB settings were manually altered, this could throw fatal errors

#### v1.0.4

-   added {uri_string} variable
-   fixed bug when using {if paginated} and no url segments (like on homepage for instance)
-   added {secure_site_url} variable
-   added Page Tracker variables

#### v1.0.3

-   added {if secure} conditional

#### v1.0.2

-   added {current_url} variable
-   removed {theme_folder_url} in EE >= 2.1.5

#### v1.0.1

-   added {page_offset} and {theme_folder_url}

#### v1.0.0

-   initial release

## Examples

###Ajax Pagination with graceful degradation using {ajax}

	{if !ajax}
		{embed="_globals/header"}
		<script type="text/javascript">
		jQuery(document).ready(function($){
			$("p#pagination a").live("click", function(event){
				event.preventDefault();
				$("body").load($(this).attr("href"));
				return false;
			});
		});
		</script>
		</head>
		<body>
	{/if}
	
	{exp:channel:entries channel="products"}
	
		{paginate}
		
		<p id="pagination">Page {current_page} of {total_pages} pages {pagination_links}</p>
		
		{/paginate}
	
	{/exp:channel:entries}
	
	{if !ajax}
		{embed="_globals/footer"}
	{/if}