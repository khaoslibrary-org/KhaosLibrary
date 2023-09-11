## Model
Referenced Bibframe and LRM .
<img width="1000px" src="models.png" align="center" alt="models" />

## Structured data type definitions

While the full definition of Data(Thing) is available at https://schema.org, you only need to consider the following properties.

## [Thing](https://schema.org/Thing)

| Property      | Type                                                      | Required | Description                                                  |
| ------------- | --------------------------------------------------------- | -------- | ------------------------------------------------------------ |
| @context      | [Text](https://schema.org/Text)                           | Yes      | Set to `https://o.khaoslibrary.org/context.json`.            |
| @id           | [Text](https://schema.org/Text)                           | Yes      | A globally unique ID for the Thing in URL format             |
| adminMetadata | [CreativeWork](https://schema.org/CreativeWork)           | Yes      | Metadata about the metadata, such as contributors and etc  <br />Entries are used to describe Things, but the entries themselves have their contributors and other metadata, so this attribute is added. According to the original design of schema.org, DataFeed as top-level data can be solved, but it is very unfavourable for consumption and parsing.<br />Definition in :http://id.loc.gov/ontologies/bibframe/AdminMetadata |
| description   | @container                                                | No       |                                                              |
| alternateName | @container                                                | No       |                                                              |
| identifier    | List of [PropertyValue](https://schema.org/PropertyValue) | Yes      | The external or other ID that unambiguously identifies this edition.   <br />Multiple      identifiers are allowed. For more details, refer to              [`PropertyValue` (`identifier`)](https://developers.google.com/search/docs/appearance/structured-data/book#propertyvalue-identifier). <br /> |



##  [CreativeWork](https://schema.org/CreativeWork)

| Property   | Type                                                         | Required | Description                                                  |
| ---------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| author     | [Person](https://schema.org/Person) or              [Organization](https://schema.org/Organization) | Yes      | The author of this  CreativeWork.                            |
| name       | [Text](https://schema.org/Text)                              | Yes      | The name of the CreativeWork.                                |
| inLanguage | [Text](https://schema.org/Text)                              | Yes      | The main language of the content in the CreativeWork.<br /><br /> For Work, it's the original language of the work. <br />Use one of the two-letter codes   from the [list               of ISO 639-1 alpha-2 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| genre      | [Text](https://schema.org/Text)                              | No       | Use one of the words  from the [Genre/Form Terms (LCGFT)](https://id.loc.gov/authorities/genreForms) |



## Work

Resource reflecting a conceptual essence of a cataloging resource.
Definition in :  http://id.loc.gov/ontologies/bibframe/Work

It is a **CreativeWork** type that does not distinguish between specific subclasses, such as Book, Movie, etc.

One of the most common observations at the last FBRB workshop held at OCLC was that few bibliographic records require FRBR aggregation.

And the latest statistics were presented: 88% of works in WorldCat have only one bibliographic record.

Also due to cost considerations, it is not made a mandatory entity type to implement, i.e:
Not every Book (edition) corresponds to owning a Work,  and Work is only created when several Books are editions of the same Work.



| Property                                      | Type                                                    | Required | Description                                                  |
| --------------------------------------------- | ------------------------------------------------------- | -------- | ------------------------------------------------------------ |
| [workExample](https://schema.org/workExample) | List of [CreativeWork](https://schema.org/CreativeWork) | Yes      | Example/instance/realization/derivation of the concept of this creative  work. E.g. the paperback edition, first edition, or e-book. |

## BookSeries

A collection of Book Edtion. Generally speaking, Book Series contains two types:

- Publishers' reprint series
- [novel sequence](https://en.wikipedia.org/wiki/Book_series)

In the Schema.org use case, BookSeries also contains periodical.

We discuss each of these cases separately:

| Concepts                                                     | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Publishers' reprint series                                   | Instead of creating a separate entry, use the **publisherSeriesName** attribute. |
| [novel sequence](https://en.wikipedia.org/wiki/Book_series)  (contains comic) | use [FictionSquence](FictionSquence) type                    |
| periodical                                                   | use [Periodical](https://schema.org/Periodical)  Type        |

Also see https://en.wikipedia.org/wiki/Book_series.

## FictionSquence

A collection of fictional book editions using the **BookSeries** type, dedicated to representing series of fictional works (especially comics and SF novels), such as

[The Hardy Boys](https://en.wikipedia.org/wiki/The_Hardy_Boys), [Nancy Drew](https://en.wikipedia.org/wiki/Nancy_Drew), [Harry Potter]( https://en.wikipedia.org/wiki/Harry_Potter) series, *[The Lord of the Rings](https://en.wikipedia.org/wiki/The_Lord_of_the_Rings)* volumes, etc.

According to the **FRBR** model, this type of series should also distinguish between **Work** and **Edtion**, where the FictionSquence is closely related to the Edtion of a book, so it is considered the Edtion of "FictionSquence", such as

>  A Song of Ice and Fire (Books 1-5) - xxx Publishing - xxxx.

FictionSquence and Book can belong to the same **Work**.

Note that FictionSquence is a collection of editions with multiple ISBN numbers. If several volumes of the same series of novels share a single ISBN, they are treated as a '**Book**' and belong to the same work as other versions of FictionSquence.


## [Book](https://schema.org/Book)

| Property   | Type                                     | Required   | Description                                                  |
| ---------- | ---------------------------------------- | ---------- | ------------------------------------------------------------ |
| bookFormat | [`Enum`](https://schema.org/Enumeration) | Yes        | The format of the edition. The value of this must be one of the              following:      <br />-  [EBook](https://schema.org/EBook) <br />-  [Hardcover](https://schema.org/Hardcover) <br />-  [Paperback](https://schema.org/Paperback) <br /> -  [GraphicNovel](https://schema.org/GraphicNovel) <br /><br />When the format type is [AudiobookFormat](https://schema.org/EBook), it should be classified as a subclass of Book [Audiobook](https://schema.org/Audiobook). |
| isbn       | Text                                     | No. <br /> | The ISBN-13 of the edition. <br /><br />Normally, at least one of the isbn(13) and isbn10 must be present.<br />Only if the value of "bookFormat" is "EBook" or "AudiobookFormat", it is not required.<br /> |



## [identifier](https://schema.org/identifier)

The `identifier` property of the  [Thing](https://schema.org/Thing)  uses the `PropertyValue`    entity.

| properties   | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| `@type`      | [`Text`](https://schema.org/Text)            Set to `PropertyValue`. |
| `propertyID` | [`Text`](https://schema.org/Text)            The type of ID. |
| `value`      | [`Text`](https://schema.org/Text)            The ID value. The external ID that unambiguously identifies this edition. Remove all              non-numeric prefixes of the external ID. |

PropertyValue in Schema.org is very flexible and can be extended by the user, but it can also be confusing for the parser.

For example, in the usage examples provided by Schema.org, they describe the oclc resource id as 'OCoLC', while [Google uses 'OCLC_NUMBER'.](https://developers.google.com/search/docs/appearance/structured-data/book#isbn-and-other-supported-identifiers)

While it is possible to use URL to describe it accurately, this option is not considered because it is too redundant.

Here, for the time being, we define some ‘propertyID’ for different things with supported identities.
(WIP)
### Person or   Organization

- VIVF
- WIKIDATA

### Book

- OPENLIBRARY
- OCLC_NUMBER
- JP_E-CODE
- LCCN
- GOODREADER
- DOUBAN
- LIBRARYTHING

### Movie And TV

- IMDB
- TMDB
- DOUBAN
- ANIDB
- BANGUMI





