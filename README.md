# Exif to RDF

This tiny tool extracts Exif data from a JPEG image file, and converts it into RDF/XML. Provide image file path as an argument, then it outputs the resulting RDF to STDOUT.

```
perl exif2rdf.pl <imagefile>
```

Requires definition file "exif-tags.json" in the same directory. Also requires Image::ExifTool and JSON modules.

## Tag-RDF Definition JSON

**exif-tags.json** is a mapping file from Exif tag number to RDF property (defined in [Exif data description vocabulary](http://www.kanzaki.com/ns/exif) ).

The root object has keys as Eixf tag, and each value object has RDF property name `propName` and additional information such as `default` or allowable `value` array.

```
{
	"283" : {
		"propName" : "yResolution",
		"default" : "72",
		"datatype" : "&xsd;decimal"
	},
	"284" : {
		"propName" : "planarConfiguration",
		"values" : {
			"1" : "chunky-format",
			"2" : "planar-format"
		}
	}
}
```
	
The above example describes that 
- tag `283` will be interpreted as RDF property `yResolution` whose datatype is `xsd:decimal`, and default value is `72`.
- tag `284` as property `planarConfiguration`, and for Exif value `1` the RDF value is `chunky-format`, and Exif `2` the RDF `planar-format`.


Note that tag numbers for GPS IFD, Interoperability IFD and PIM IFD
will have a prefix 'g', 'i' and 'p' respectively.


## Background

This is an old perl script written in 2007, but still works (as of 2017). See also a [half-written document about Photo and RDF](http://www.kanzaki.com/docs/sw/photo-rdf.html) (mostly in Japanese).
	