[//]: # (The contents of this file were originally extracted from JOSM code and are licensed on GPL terms, see LICENSE for more information)


# JOSM Filter Syntax Documentation

## Basics

| Syntax                         | Description |
|---                             |--- |
| _substr_                       | matches if _substr_ appears in any **key or value** <br /><br />(e.g. `wa` matches both `natural=water` and `highway=path`) <br /><br /> Whitespace or special characters in the search string ( `:`, `(`, `)`, `\|`, `^`, `=`, `~`, `?`, `<`, `>`, `"` ) need to be escaped by prefixing them with `\` (e.g. `area\:highway`), or the whole string needs to be enclosed in double quotes (e.g. `"area:highway"`). Double quotes that are part of the search string always need to be escaped with `\` (e.g. `"abc:de\"fg"`). |
| _key_**:**_valuefragment_      | _valuefragment_ anywhere in _key_. `name:str` matches name=Bakerstreet |
| **-**_key_**:**_valuefragment_ | _valuefragment_ nowhere in _key_ |
| _key_**:**                     | matches if exact _key_ exists |
| _key_**?**                     | matches if _key_ has a truthy value (`true`, `yes`, `1`, `on`) |
| _key_**=**_value_              | _key_ with exactly _value_ |
| _key_**~**_regexp_             | _key_ and value matches _regexp_, supported in JOSM since 16260 |
| *key*__=*__                    | _key_ with any value |
| _key_**=**                     | _key_ with empty value |
| __*=__*value*                  | _value_ in any key |
| _key_**>**_value_              | matches if _key_ is greater than _value_ (analogously, less than _<_) |
| \"key\"=\"value\"              | enclosed key and value in quotes to quote operators.<br>Within quoted strings the __"__ and __\\__ characters need to be escaped " by a preceding __\\__ (e.g. __\\"__ and __\\\\__)., name=\"Baker Street\", \"addr:street\" |


## Combinators

| Syntax                         | Description |
|---                             |--- |
|_expr_ _expr_                   | logical and (both expressions have to be satisfied), e.g. `Baker Street` = `Baker` and `Street` |
|_expr_ __&__ _expr_             | logical and (both expressions have to be satisfied)|
|_expr_ __AND__ _expr_           | logical and (both expressions have to be satisfied) <br /><br />`AND` is case insensitive unlike other functions/properties |
|_expr_ __&#124;__ _expr_        | logical or (at least one expression has to be satisfied)|
|_expr_ __OR__ _expr_            | logical or (at least one expression has to be satisfied)<br /><br />`OR` is case insensitive unlike other functions/properties  |
|_expr_ __^__ _expr_             | logical xor (one and only one expression has to be satisfied)|
|_expr_ __XOR__ _expr_           | logical xor (one and only one expression has to be satisfied)<br /><br />`XOR` is case insensitive unlike other functions/properties  |
|__-__*expr*                     | logical not|
|__(__*expr*__)__                | use parenthesis to group expressions |

## Objects

| Syntax                             | Description |
|---                                 |--- |
|__type:node__                       | all nodes|
|__type:way__                        | all ways|
|__type:relation__                   | all relations|
|__closed__                          | all closed ways|
|__untagged__                        | object without useful tags|
|__preset:"__Annotation/Address__"__ | all objects that use the address preset|
|__preset:"__Geography/Nature/*__"__ | all objects that use any preset under the Geography/Nature group|

## Metadata

| Syntax                       | Description |
|---                           |--- |
| __user:__                    | objects changed by author, user:_OSM username_ (objects with the author _OSM username_), user:anonymous (objects without an assigned author)|
|__id:__                       | objects with given ID"), id:0 (new objects)|
|__version:__                  | objects with given version. version:0 (objects without an assigned version)|
|__changeset:__                | objects with given changeset ID, changeset:0 (objects without an assigned changeset)|
|__timestamp:__                | objects with last modification timestamp within range, timestamp:2012/, timestamp:2008/2011-02-04T12|

## Properties

| Syntax                       | Description |
|---                           |--- |
|__nodes:__*20-*               | ways with at least 20 nodes, or relations containing at least 20 nodes|
|__ways:__*3-*                 | nodes with at least 3 referring ways, or relations containing at least 3 ways|
|__tags:__*5-10*               | objects having 5 to 10 tags|
|__role:__*role*               | objects with given role in a relation|
|__areasize:__*-100*           | closed ways with an area of 100 m^2|
|__waylength:__*200-*          | ways with a length of 200 m or more|
|__members:__*range*           | relations with a member count in *range*, supported in JOSM since 16581 |

## State

| Syntax                       | Description |
|---                           |--- |
|__modified__                  | all modified objects|
|__new__                       | all new objects|
|__selected__                  | all selected objects|
|__incomplete__                | all incomplete objects|
|__deleted__                   | all deleted objects|

## Related objects

| Syntax                       | Description |
|---                           |--- |
|__child__ _expr_              | all children of objects matching the expression, child building|
|__parent__ _expr_             | all parents of objects matching the expression, parent bus_stop|
|__hasRole:__*stop*            | relation containing a member of role _stop_|
|__role:__*stop*               | objects being part of a relation as role _stop_|
|__nth:__*7*                   | n-th member of relation and/or n-th node of way, "nth:5 (child type:relation), nth:-1|
|__nth%:__*7*                  | every n-th member of relation and/or every n-th node of way, nth%:100 (child waterway)|

### Matching objects in relations

* Match all ways of all reations:

	type:way & child type:relation

* Match all ways of all reations that are multipolygons:

	type:way & child type:relation & child type=multipolygon

* Match all ways with role:outer of all reations:

	type:way & role:outer & child type:relation

* Match all ways with role:outer of a reation with a certain _id_:

	type:way & role:outer & child id:_id_

* Select nodes of ways in a multipoligon.  Multipolygons are relations that have ways as members.
Nodes in-turn are children of ways which are members of a multipolygon. Consequently the child operator needs be applied recursively to select nodes in a certain relation. 
Select nodes of ways in relation with id=14297825:

	type:node & child type:way & child child id:14297825


## View

| Syntax                       | Description |
|---                           |--- |
|__inview__                    | objects in current view|
|__allinview__                 | objects (and all its way nodes / relation members) in current view|
|__indownloadedarea__          | objects in downloaded area|
|__allindownloadedarea__       | all objects (and all its way nodes / relation members) in downloaded area|

## Overpass query support

| Syntax                       | Description |
|---                           |--- |
|__newer__**=**_date_          | undocumented magic value? |
|_expr_ __in__ _location_      | objects in location |
|_expr_ __around__ _location_  | objects new location |
|_expr_ __in bbox__            | objects in current bounding box |

### Copyright 

The contents of this file were originally extracted from JOSM code that displays help on the search modal and are licensed on GPL terms, please see [the JOSM website](https://josm.openstreetmap.de/) and the accompanying LICENCE file for more information.
                 
