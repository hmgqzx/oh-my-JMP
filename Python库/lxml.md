## lxml.etree

```Python
 from lxml import etree
```

#### The fromstring() function

The fromstring() function is the easiest way to parse a string:

```Python
>>> some_xml_data = "<root>data</root>"

>>> root = etree.fromstring(some_xml_data)
>>> print(root.tag)
root
>>> etree.tostring(root)
b'<root>data</root>'
```

lxml.etree.fromstring

```Python
fromstring(text, parser=None, base_url=None)
```

Parses an XML document or fragment from a string. **Returns the root node** (or the result returned by a parser target).

To override the default parser with a different parser you can pass it to the `parser` keyword argument.

The `base_url` keyword argument allows to set the original base URL of the document to support relative Paths when looking up external entities (DTD, XInclude, ...).