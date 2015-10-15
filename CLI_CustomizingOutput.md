How to customize the output of the CLI module

# Introduction #

Using the "output" option will allow choosing "plain", "json" or "xml" for the output format.

# Details #

The following examples show output for detecting the language of the text "English":

## Plain ##

```
Detections[[Detection{language='en', reliable=false, confidence=0.037936516}]]
```

In order to customize the plain output further, you can pass the following system properties to the JVM (using the java -D option):

  * org.google.translate.api.v2.core.model.toString - allowed values:
    * short - returns the most simple and important info (Default when using the core module).
    * long - returns all the not null fields.
    * full - returns all the fields (Default when using the CLI module).
> A constant with the property name can be found at `org.google.translate.api.v2.core.model.AbstractResponseObject.TO_STRING_FORMAT`.

## XML ##

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?><detections><detection><i
tem><confidence>0.037936516</confidence><language>en</language><isReliable>false
</isReliable></item></detection></detections>
```

In order to customize the XML output further, you can pass the following system properties to the JVM (using the java -D option):

  * jaxb.encoding - value must be a java.lang.String
> > The output encoding to use when marshalling the XML data. The Marshaller will use "UTF-8" by default if this property is not specified.

  * jaxb.formatted.output - value must be a java.lang.Boolean
> > This property controls whether or not the Marshaller will format the resulting XML data with line breaks and indentation. A true value for this property indicates human readable indented xml data, while a false value indicates unformatted xml data. The Marshaller will default to false (unformatted) if this property is not specified.

## JSON ##

```
{"detection":[[{"language":"en","confidence":0.037936516,"isReliable":false}]]}
```