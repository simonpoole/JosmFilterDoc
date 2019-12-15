[//]: # (The contents of this file were originally extracted from JOSM code and are licensed on GPL terms, see LICENSE for more information)


## Basics

Baker Street                Baker and Street substrings in any key or value

"Baker Street"              Baker Street in any key or value

_key_:_valuefragment_       valuefragment anywhere in key. name:str matches name=Bakerstreet

-_key_:_valuefragment_      valuefragment nowhere in key

_key_                       matches if ''key'' exists

_key_=_value_               ''key'' with exactly ''value''

_key_=*                     ''key'' with any value

_key_=                      ''key'' with empty value

*=_value_                   ''value'' in any key

_key_>_value_               matches if ''key'' is greater than ''value'' (analogously, less than)

\"key\"=\"value\"           "\"\"=\"\"", to quote operators.<br>Within quoted strings the __"__ and __\__ characters need to be escaped " by a preceding __\__ (e.g. __\"__ and __\\__)., name=\"Baker Street\", \"addr:street\"


## Combinators

_expr_ _expr_               logical and (both expressions have to be satisfied), "Baker Street"

_expr_ | _expr_             logical or (at least one expression has to be satisfied)

_expr_ OR _expr_            logical or (at least one expression has to be satisfied)

-_expr_                     logical not

(_expr_)                    use parenthesis to group expressions

## Objects

type:node                   all nodes

type:way                    all ways

type:relation               all relations

closed                      all closed ways

untagged                    object without useful tags

preset:"Annotation/Address" all objects that use the address preset

preset:"Geography/Nature/*" all objects that use any preset under the Geography/Nature group

## Metadata

user:                       objects changed by author, user:_OSM username_ (objects with the author _OSM username_), user:anonymous (objects without an assigned author)

id:                         objects with given ID"), id:0 (new objects)

version:                    objects with given version. version:0 (objects without an assigned version)

changeset:                  objects with given changeset ID, changeset:0 (objects without an assigned changeset)

timestamp:                  objects with last modification timestamp within range, timestamp:2012/, timestamp:2008/2011-02-04T12

## Properties

nodes:_20-_                 ways with at least 20 nodes, or relations containing at least 20 nodes

ways:_3-_                   nodes with at least 3 referring ways, or relations containing at least 3 ways

tags:_5-10_                 objects having 5 to 10 tags

role:                       objects with given role in a relation

areasize:_-100_             closed ways with an area of 100 m^2

waylength:_200-_            ways with a length of 200 m or more

## State

modified                    all modified objects

new                         all new objects

selected                    all selected objects

incomplete                  all incomplete objects

deleted                     all deleted objects

## Related objects

child _expr_               all children of objects matching the expression, child building

parent _expr_              all parents of objects matching the expression, parent bus_stop

hasRole:_stop_             relation containing a member of role _stop_

role:_stop_                objects being part of a relation as role _stop_

nth:_7_                    n-th member of relation and/or n-th node of way, "nth:5 (child type:relation), nth:-1

nth%:_7_                  every n-th member of relation and/or every n-th node of way, nth%:100 (child waterway)

## View

inview                      objects in current view

allinview                   objects (and all its way nodes / relation members) in current view

indownloadedarea            objects in downloaded area

allindownloadedarea         allindownloadedarea objects (and all its way nodes / relation members) in downloaded area

### Copyright 

The contents of this file were originally extracted from JOSM code and are licensed on GPL terms, please see [the JOSM website](https://josm.openstreetmap.de/) and the accompanying LICENCE file for more information.
                 
