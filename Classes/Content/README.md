# getContentArray()

A wrapper for getContent(), useful for getting array output from the CMS.

@author - Chris Ullyott <chris@monkdevelopment.com>

@url - https://github.com/MonkDev/monkcms-snippets/

@demo - http://files.monkdev.com/chris/getContentArray-Demo-Small.mp4

##Example
```
$array = Content::getContentArray(array(
	'module' => 'linklist',
	'display' => 'links',
	'params' => array('find:featured-links','howmany:2'), 
	'tags' => 'slug, url, customicon'
));
```

```
Array
(
    [0] => Array
        (
            [slug] => this-week
            [url] => /resources/events
            [customicon] => icon-calendar
        )

    [1] => Array
        (
            [slug] => small-group
            [url] => /contact-form
            [customicon] => icon-user
        )
)
```


##Options

####Module
The MonkCMS module to be queried.

####Display
The display mode. Default is `detail`.

####Params
An array of normal MonkCMS API parameters and their values, such as "find", "howmany". Can be written in any of the following three formats:

1. `array('find:featured-links', 'howmany:10')`

2. `array('find' => featured-links, 'howmany' => 10)`

3. `"find:featured-links, howmany:10"`

####Show
The default and only show tag used is `show`, so you will need to use `'show' => 'show_postlist'` or etc. for various modules. There are no "before_show" or "after_show" capabilities.

####Tags
An array of API tags to include in the query, without the double underscores. Pass either as an array or as a comma-separated list.

####Keys
Sets the keys of the array with the value of one of the specified TAGS. Ideal with unique 'id' or 'slug' values (this does not work with `'display' => 'detail'`). For numerical keys, use `'keys' => false`.

#### Output
Set to `json` for JSON output.


## Tips

#### Find
Pass "find" either as a first-level parameter, or within the "params" option.

#### Booleans
Some tags that respond by outputting a single space are considered to be a boolean of TRUE. They are:

`__custom(.*?)__`  `__if(.*?)__`  `__is(.*?)__`

####Howmany
`"howmany" => <INTEGER>` will limit the number of items returned even where the API does not do this.

####Easy Edit
Add the HTML for the Easy Edit links to your query by adding `'easyEdit' => true`

## More examples

####Page
	
```
$array = Content::getContentArray(array(
	'module' => 'page',
	'find' => 'giving',
	'tags' => 'name, slug, url, text, tags'
));
```


####Media

```
$array = Content::getContentArray(array(
	'module' => 'media',
	'display' => 'list',
	'params' => array(
		'howmany' => 10,
		'nocache' => true
	),
	'tags' => 'id, name, filename, url',
	'keys' => 'id'
));
```
	
	
####Blog Posts

```
$array = Content::getContentArray(array(
	'module' => 'blog',
	'display' => 'list',
	'params' => 'name:all, find_category:missions, howmany:10',
	'show' => 'show_postlist',
	'tags' => array(
		"blogposttitle",
		"__blogpostdate format='Y-m-d'__"
	),
	'output' => 'json'
));
```
