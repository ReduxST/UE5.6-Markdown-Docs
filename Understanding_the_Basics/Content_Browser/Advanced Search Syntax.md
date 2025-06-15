# Advanced Search Syntax

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/advanced-search-syntax-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/advanced-search-syntax-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:12

---

You can search for your content in the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) using advanced search operators. These operators can refine your search, making it easier for you to find what you need. You can also use them to search for key-value pairs from Asset metadata, and access special key values.

![Advanced search in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4023e938-a714-448f-b549-c557fe026c38/advanced-search-content-browser.png)

An example of using an advanced search operator in the Content Browser Search box.

The following table shows all the available operators:

| Operator (Type) | Syntax | Description | Example |
| --- | --- | --- | --- |
| **Equal (Binary)** | 
`=` `==` `:`



 | Tests whether the value returned for a given key is equal to the specified vaDlue. | 

`Name="Blast"` `Name==Blast` `Name:Bla...`



 |
| **NotEqual (Binary)** | 

`!=` `!:`



 | Tests whether the value returned for a given key is not equal to the specified value. | 

`Name!=Blast` `Name!:"Blast"`



 |
| **Less (Binary)** | `<` | Tests whether the value returned for a given key is less than the specified value. This supports numeric values only. | `Triangles<92` |
| **LessOrEqual (Binary)** | 

`<=` `<:`



 | Tests whether the value returned for a given key is less than or equal to the specified value. This supports numeric values only. | 

`Triangles<=92` `Triangles<:92`



 |
| **Greater (Binary)** | `>` | Tests whether the value returned for a given key is greater than the specified value. This supports numeric values only. | `Triangles>92` |
| **GreaterOrEqual (Binary)** | 

`>=` `>:`



 | Tests whether the value returned for a given key is greater than or equal to the specified value. This supports numeric values only. | 

`Triangles>=92` `Triangles>:92`



 |
| **Or (Binary)** | 

`OR` `||` `|`



 | Tests two values and returns `true` if either evaluate to `true`. | 

`Blast OR Type:Blueprint` `!Blast || Path:Testing` `Name:"Blast" | Path:Testing...`



 |
| **And (Binary)** | 

`AND` `&&` `&`



 | Tests two values and returns `true` if both evaluate to `true`. | 

`Blast AND Type:Blueprint` `!Blast || Path:Testing` `Name:"Blast" | Path:Testing...`



 |
| **Not (Pre-Unary)** | 

`NOT` `!`



 | Tests the value that follows it and then returns the inverted results. | 

`NOT Blast` `! "Blast"`



 |
| **TextCmpInvert (Pre-Unary)** | `-` | Modifies a text value so that it will return the inverted result of the operation it is involved in. | 

`-Blast` `-"Blast"`



 |
| **TextCmpExact (Pre-Unary)** | `+` | Modifies a text value so that it will perform an "exact" text comparison. | 

`+Blast` `+"Blast"`



 |
| **TextCmpAnchor (Pre-Unary)** | `...` | Modifies a text value so that it will perform an "ends with" text comparison. | 

`...ast` `..."ast"`



 |
| **TextCmpAnchor (Post-Unary)** | `...` | Modifies a text value so that it will perform a "starts with" text comparison. | 

`Bla...` `"Bla"...`



 |

## Special Keys

Most keys available for searching come from Asset metadata that was extracted from the Asset registry. However, there are several special keys that exist for all Asset types. These special keys only support `Equal` or `NotEqual` comparison operators.

| Key | Alias | Description |
| --- | --- | --- |
| **Name** | N/A | The Asset name. |
| **Path** | N/A | The Asset path. |
| **Class** | Type | The Asset class. |
| **ParentClass** | N/A | The Asset's parrent class. |
| **Collection** | Tag | The names of any collections that contain the Asset. |

## Strings

Strings can either be quoted (single or double) or not quoted. Quoted strings can contain nested quotes; however, you must use a backslash ( \\ ) to exit any nested quotes. The main difference between using unquoted and quoted strings is that quoted strings can use spaces and special characters in search terms. By default, they will perform partial string matches unless a `TextCmpExact` or `TextCmpAnchor` operator is used to modify the behavior.

Below are some examples using single and double quotes and backslashes:

```
	`"Foo\"bar"  ->  Foo"bar 	'Foo\'bar'  ->  Foo'bar 	"Foo\'bar"  ->  Foo'bar 	'Foo\"bar'  ->  Foo"bar 	"Foo\\bar"  ->  Foo\bar 	'Foo\\bar'  ->  Foo\bar`

Copy full snippet
```
"Foo\\"bar" -> Foo"bar 'Foo\\'bar' -> Foo'bar "Foo\\'bar" -> Foo'bar 'Foo\\"bar' -> Foo"bar "Foo\\\\bar" -> Foo\\bar 'Foo\\\\bar' -> Foo\\bar

A literal backslash ( \\ ) must be used to escape using another backslash.

## Asset Metadata

Hovering over an Asset's name in the Content Browser will display its metadata.

![Example metadata for a Texture Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4596da94-17b1-4a9e-87e0-c7903b05c282/example-asset-metadata.png)

Example metadata for a Texture Asset.

Different Assets may list different metadata specific to that type, so Static Meshes would be different than a Skeletal Mesh.

You can use any type of metadata to search for Assets with that characteristic. Your search should use the following syntax:

**\[Metadata Name\] \[Operator\] \[String or Numeric Value\]**

For example:

`Triangles>=10500`

`Type==Skeletal`

`UVChannels>2` 

`CollisionPrims!=0`

Metadata is not case-sensitive, but it does require no spacing between characters. For example, if you want to search for Morph Target, you should use `MorphTarget`.

### Basic Search Example

A basic search takes a metadata object and uses an Operator to test against a string or value.

For example:

-   To search for any Asset that has more than 1500 triangles, you would use `Triangles>1500`.
    
-   To search for all Blueprint Assets, you would use `Type==Blueprint`.
    

### Advanced Search Examples

By using the `AND`, `OR`, and `NOT` operators, you can test against multiple search operations at once. For example, to search for any Asset that is using a Translucent Material that is using the Default Lit Shading Model, you would use the following syntax:

```

	`BlendMode==Translucent AND ShadingModel==DefaultLit`

Copy full snippet
```
BlendMode==Translucent AND ShadingModel==DefaultLit

By using the `AND` operator, both operations testing the Blend Mode and Shading Model must evaluate to `true` to display any results.

When you use the `OR` operator, either operation can independently evaluate to `true` to display its result. For example,not every Material using a Translucent Blend Mode will be using Default Lit. For complex advanced searches, Operators of the same type always combine together. Parentheses can resolve the ambiguity when you start using different operator types. For example, we can perform two searches and then evaluate them to display results. The first operation will evaluate any Material that is Translucent and Default Lit:

```

	`BlendMode==Translucent AND ShadingModel==DefaultLit`

Copy full snippet
```
BlendMode==Translucent AND ShadingModel==DefaultLit

The second operation will evaluate any Material that is a Deferred Decal and that doesn't use Scene Color:

```

	`MaterialDomain==DeferredDecal AND HasSceneColor==False`

Copy full snippet
```
MaterialDomain==DeferredDecal AND HasSceneColor==False

You can use parentheses to evaluate the results of both of these searches, like so:

```

	`(BlendMode==Translucent AND ShadingModel==DefaultLit) OR (MaterialDomain==DeferredDecal AND HasSceneColor==False)`

Copy full snippet
```
(BlendMode==Translucent AND ShadingModel==DefaultLit) OR (MaterialDomain==DeferredDecal AND HasSceneColor==False)

By using the `OR` operator between the parentheticals, the results will evaluate each parenthetical on its own and display results that return `true` for either one. If you were to use the `AND` operator, all four operations would have to return `True` to display any results.