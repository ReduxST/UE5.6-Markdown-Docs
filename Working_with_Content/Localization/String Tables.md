# String Tables

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-string-tables-for-text-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-string-tables-for-text-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:08

---

**String Tables** provide a way to centralize your localized text into one (or several) known locations, and then reference the entries within a string table from other assets or code in a robust way that allows for easy re-use of localized text.

## Creating String Tables

String Tables can be defined in C++, loaded using a CSV file, or created as an Asset.

### Creating String Tables in C++

String Tables can be created in C++ by using the `LOCTABLE` family of macros.

| Macro | Description |
| --- | --- |
| `LOCTABLE_NEW` | Creates an empty string table instance. |
| `LOCTABLE_FROMFILE_X` | Creates a string table instance and populates it from the given CSV file. When using the `_ENGINE` variant, the file is relative to the Engine content directory, and when using the `_GAME` variant, the file is relative to the project content directory. |
| `LOCTABLE_SETSTRING` | Sets an entry in a string table. |
| `LOCTABLE_SETMETA` | Sets optional meta-data for an entry in a string table. |

**Example:**

```
	`// Create and populate a string table using only C++ 	LOCTABLE_NEW("CodeStringTable","CodeStringTable"); 	LOCTABLE_SETSTRING("CodeStringTable","HelloWorld","Hello World!"); 	LOCTABLE_SETMETA("CodeStringTable","HelloWorld","Comment","This is a comment about hello world"); 	LOCTABLE_SETSTRING("CodeStringTable","GoodbyeWorld","Goodbye World!"); 	LOCTABLE_SETMETA("CodeStringTable","GoodbyeWorld","Comment","This is a comment about goodbye world");`

Copy full snippet
```
// Create and populate a string table using only C++ LOCTABLE\_NEW("CodeStringTable","CodeStringTable"); LOCTABLE\_SETSTRING("CodeStringTable","HelloWorld","Hello World!"); LOCTABLE\_SETMETA("CodeStringTable","HelloWorld","Comment","This is a comment about hello world"); LOCTABLE\_SETSTRING("CodeStringTable","GoodbyeWorld","Goodbye World!"); LOCTABLE\_SETMETA("CodeStringTable","GoodbyeWorld","Comment","This is a comment about goodbye world");

### Creating String Tables Using CSV

String Tables defined in CSV can be loaded using the `LOCTABLE_FROMFILE_X` macros, or can also be imported to/exported from a String Table asset.

**Example**:

```
	`// Create and populate a string table from a CSV file 	LOCTABLE_FROMFILE_GAME("CSVStringTable","CSVStringTable","StringTableCSV/TestStrings.csv");`

Copy full snippet
```
// Create and populate a string table from a CSV file LOCTABLE\_FROMFILE\_GAME("CSVStringTable","CSVStringTable","StringTableCSV/TestStrings.csv");

The CSV format used for string tables has two mandatory columns, **Key** and **SourceString**, with any extra columns being parsed as meta-data for your string table entries.

```
	`Key,SourceString,Comment 	"HelloWorld","Hello World!","This is a comment about hello world" 	"GoodbyeWorld","Goodbye World!","This is a comment about goodbye world"`

Copy full snippet
```
Key,SourceString,Comment "HelloWorld","Hello World!","This is a comment about hello world" "GoodbyeWorld","Goodbye World!","This is a comment about goodbye world"

Quotes in CSV files are escaped using two sets of quotes ("") rather than C-style escaping (\\"), however other control characters in your string (including tabs and new-lines) should be escaped using C-style escaping.

CSV string tables loaded using the `LOCTABLE_FROMFILE_X` macros are monitored for changes, and are automatically re-imported if they change on the disk (this is for Editor builds only).

CSV string tables aren't staged automatically. It is recommended that you place your CSV string tables in a known folder and then add them to the **Additional Non-Asset Directories to Package** in your project's **Packaging** settings.

### Creating a String Table Asset

String Table assets can be created using the **Content Browser** (**Add > Miscellaneous > String Table**), and can be managed through the String Table editor. The String Table editor cannot currently edit meta-data, however any meta-data imported from a CSV file is preserved.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90d3eabf-1059-4e4c-9f41-1ca2f76347b6/stringtables-01.png)

String Table assets are binary, so they cannot be resolved if a merge conflict happens. We recommend that you keep the String Table assets more granular than when you are using C++ or CSV to minimize your conflict domain.

## Referencing a String Table

You can reference string tables in C++, in INI files, or as an Asset.

### Referencing a String Table in C++

String Tables can be referenced in C++ using either the `LOCTABLE` macro, or the static [`FText::FromStringTable`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/FromStringTable/index.html) function. The underlying logic is identical, although the macro is easier to type but will only work with literal values, whereas the function will work with both literal and variable arguments.

### Referencing a String Table in the INI File

String Tables can be referenced in INI files using the `LOCTABLE` macro syntax.

### Referencing a String Table Asset

String Tables can be referenced using `FText` properties. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f328238-f1a1-4782-84be-32cd44921049/stringtables-02.png)

Click the white flag next to a text property to link that property instance to a string table entry, instead of defining your localized text inline. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ea13f19-7587-466a-bc3d-fc146b99668f/stringtables-03.png)

## Redirecting a String Table

It is recommended that you avoid renaming or moving string tables when possible. However, if you need to rename or move a string table, there is a way to redirect whole tables, and to redirect individual keys. You can do this in INI files, or by redirecting a String Table Asset.

### Redirecting a String Table in the INI File

String Tables can be redirected using an INI file. The following example will redirect an entire string table to point to another string table:

```
	`[Core.StringTable] 	+StringTableRedirects=(OldStringTable="Foo",NewStringTable="Bar")`

Copy full snippet
```
\[Core.StringTable\] +StringTableRedirects=(OldStringTable="Foo",NewStringTable="Bar")

If you want to redirect an entry in one string table to an entry in another string table, use the following example:

```
	`[Core.StringTable] 	+StringTableRedirects=(StringTable="Foo",OldKey="Bar",NewKey="Baz")`

Copy full snippet
```
\[Core.StringTable\] +StringTableRedirects=(StringTable="Foo",OldKey="Bar",NewKey="Baz")

### Redirecting a String Table Asset

Moving or renaming a String Table Asset will leave an Asset Redirector behind. This is processed and followed like any other Asset Redirector.