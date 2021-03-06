##Hypermedia Response Format
Use existing standard formats like JSON, ATOM, Collection-JSON, HAL (both JSON and XML) etc. over home made formats. The list here represents only a subset of possible formats. Refer to [On Choosing a Hypermedia Format](http://sookocheff.com/post/api/on-choosing-a-hypermedia-format/) for a more detailed overview of Hypermedia Formats.

Regardless of your choice all formats need to support link relation elements.

* Use **IANA** defined link relation attribute values by default
You can find the list of supported values [here](http://www.iana.org/assignments/link-relations/link-relations.xhtml).
* if new link relation attributes are required, register them with IANA (alternative or fallback is the canonicalized list maintained by Haufe CTO Office). Please contact the CTO Office for the latter.

A response SHOULD return related and valid link elements, and MUST return a link element to **self**.

An API client should not hardcode any resource URL or make assumptions about an existing URL. Instead URL’s should be derived from link elements via the appropriate link relation Attribute.

[Here](https://en.wikipedia.org/wiki/Internet_media_type) you can find a list of Content types.

> Our prefered way for hypermedia support is HAL. Other formats like Atom are also a valid choice. It is strongly recommended that the URLs generated by the API should be absolute URLs.


###HAL – Hypermedia Application Language

It has custom content and profile media type, the description of the data.

The content types are:

    application/hal+json
    application/hal+xml

More about it in their official [website](http://stateless.co/hal_specification.html).

This is the desciption from the Website http://stateless.co/hal_specification.html.

HAL provides a set of conventions for expressing hyperlinks in either JSON or XML.

**The rest of a HAL document is just plain old JSON or XML with optional embedded resources**

Instead of using ad-hoc structures, or spending valuable time designing your own format; you can adopt HAL's conventions and focus on building and documenting the data and transitions that make up your API.

HAL is a little bit like HTML for machines, in that it is generic and designed to drive many different types of application via hyperlinks. The difference is that HTML has features for helping 'human actors' move through a web application to achieve their goals, whereas HAL is intended for helping 'automated actors' move through a web API to achieve their goals.

Having said that, **HAL is actually very human-friendly too**. Its conventions make the documentation for an API discoverable from the API messages themselves.  This makes it possible for developers to jump straight into a HAL-based API and explore its capabilities, without the cognitive overhead of having to map some out-of-band documentation onto their journey.

###ATOM
	Content-Type: application/Atom+XML

Mike Amundsen described the format [here.](http://amundsen.com/hypermedia/atom/) The next paragraph is a copy from his page.

_<span class="quoted">Atom is an XML-based document format that describes lists of related information known as "feeds". Feeds are composed of a number of items, known as "entries", each with an extensible set of attached metadata. For example, each entry has a title. The primary use case that Atom addresses is the syndication of Web content such as weblogs and news headlines to Web sites as well as directly to user agents. </span>[<sup>[1]</sup>](http://amundsen.com/hypermedia/atom/#ref-atom "The Atom Syndication Format")_

_<span class="quoted">The Atom Publishing Protocol is an application-level protocol for publishing and editing Web Resources using HTTP [RFC2616] and XML 1.0\. The protocol supports the creation of Web Resources and provides facilities for: 1) Collections: Sets of Resources, which can be retrieved in whole or in part; 2) Services: Discovery and description of Collections; and 3) Editing: Creating, editing, and deleting Resources. </span>[<sup>[2]</sup>](http://amundsen.com/hypermedia/atom/#ref-atompub "The Atom Publishing Protocol")_

###Collection+JSON

	Content-Type: application/vnd.collection+json

Mike Amundsen described the format [here](http://amundsen.com/media-types/collection/format/) in a clear and lucid way. The next paragraph is a copy from his page.

_The [Collection+JSON](http://amundsen.com/media-types/collection/) hypermedia type is designed to support full read/write capability for simple lists (contacts, tasks, blog entries, etc.). The standard application semantics supported by this media type include Create, Read, Update, and Delete (CRUD) along w/ support for predefined queries including [query templates](http://amundsen.com/media-types/collection/format/#query-templates) (similar to HTML "GET" forms). Write operations are defined using a [template](http://amundsen.com/media-types/collection/format/#objects-template) object supplied by the server as part of the response representation._

_Each [item](http://amundsen.com/media-types/collection/format/#arrays-items) in a [Collection+JSON](http://amundsen.com/media-types/collection/)[collection](http://amundsen.com/media-types/collection/format/#objects-collection) has an assigned URI (via the [href](http://amundsen.com/media-types/collection/format/#properties-href) property) and an optional array of one or more [data](http://amundsen.com/media-types/collection/format/#arrays-data) elements along with an optional array of one or more [link](http://amundsen.com/media-types/collection/format/#arrays-links) elements. Both arrays support a [name](http://amundsen.com/media-types/collection/format/#properties-name) property for each object in the collection in order to decorate these elements with domain-specific semantic information (e.g. `"data" : [{"name" : "first-name", ...},...]`)._

_The [Collection+JSON](http://amundsen.com/media-types/collection/) hypermedia type has a limited set of predefined [link relation](http://amundsen.com/media-types/collection/format/#link-relations) values and supports [additional values](http://amundsen.com/media-types/collection/format/#rels-other) applied by implementors in order to better describe the application domain to which the media type is applied._

_The following sections describe the process of reading and writing data using the [Collection+JSON](http://amundsen.com/media-types/collection/) hypermedia type as well as the way to parse and execute [Query Templates](http://amundsen.com/media-types/collection/format/#query-templates). Additional examples can be found in the [Examples](http://amundsen.com/media-types/collection/examples/) section of this documentation._

###JSON

[Here](https://en.wikipedia.org/wiki/JSON) you can find a more detailed explanation.

	Content-Type: application/json

The following example shows a possible JSON representation describing a person.

	{
	  "firstName": "John",
	  "lastName": "Smith",
	  "isAlive": true,
	  "age": 25,
	  "address": {
	    "streetAddress": "21 2nd Street",
	    "city": "New York",
	    "state": "NY",
	    "postalCode": "10021-3100"
	  },
	  "phoneNumbers": [
	    {
	      "type": "home",
	      "number": "212 555-1234"
	    },
	    {
	      "type": "office",
	      "number": "646 555-4567"
	    }
	  ],
	  "children": [],
	  "spouse": null
	}
 
###XML

JSON has outrun XML as response format. However it is a good idea to support both.

	Content-Type: application/xml

The following example shows a possible XML representation describing a person. 

	<person>
	  <firstName>John</firstName>
	  <lastName>Smith</lastName>
	  <age>25</age>
	  <address>
	    <streetAddress>21 2nd Street</streetAddress>
	    <city>New York</city>
	    <state>NY</state>
	    <postalCode>10021</postalCode>
	  </address>
	  <phoneNumbers>
	    <phoneNumber>
	      <type>home</type>
	      <number>212 555-1234</number>
	    </phoneNumber>
	    <phoneNumber>
	      <type>fax</type>
	      <number>646 555-4567</number>
	    </phoneNumber>
	  </phoneNumbers>
	  <gender>
	    <type>male</type>
	  </gender>
	</person>
	 
### Hypermedia Link base URLs

For a discussion of the `Forwarded` header and its usage, see [Hypermedia and REST](../hypermedia-and-rest/hypermedia-and-rest.md).
