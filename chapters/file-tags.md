# Annex H SPDX File Tags (Informative)

## H.1 Rationale <a name="H.1"></a>

SPDX short-form license identifiers using the [`SPDX-License-Identifier:`](https://spdx.dev/ids) tag, as described in Annex [E](using-SPDX-short-identifiers-in-source-files.md), provide a mechanism for developers to easily convey information about the licenses they declare on a file-by-file basis. That mechanism is intentionally very easy for software tools to identify and detect, since it includes a standard text string that is unlikely to occur in other contexts, and since it uses license identifiers from the [SPDX License List](https://spdx.org/licenses) or from user-defined `LicenseRef-` statements.

The SPDX specification defines various other fields in the File Information section (Clause [8](file-information.md)) that are also useful for conveying information on a file-by-file basis. For example, the [REUSE Software guidelines](https://reuse.software) community expressed interest in having a similar method to recommend that developers use to express their copyright notices in a machine-readable manner.

This appendix describes a mechanism, similar to `SPDX-License-Identifier`, for developers to convey such other file-based information easily in comments in their files. This in turn enables software tools to easily find and extract that information, and to insert it into the corresponding fields of an SPDX document generated by those tools.

## H.2 Format <a name="H.2"></a>

An SPDX file tag consists of a single line, generally as part of a comment near the top of the file, in the following format:

```text
SPDX-tagname: <value>
```

where _tagname_ is replaced by the 'tag' defined for tag-value SPDX documents for that field, according to the [File Information](file-information.md) section of the SPDX specification. The meaning and semantics of any SPDX file tag are intended to be identical to those described in the File Information section of the SPDX specification.

Examples:

File type (see [8.3](file-information.md#8.3)):

```text
SPDX-FileType: SOURCE
SPDX-FileType: DOCUMENTATION
SPDX-FileType: TEXT
```

Copyright text (see [8.8](file-information.md#8.8)):

```text
SPDX-FileCopyrightText: 2019 Jane Doe <jane@example.com>
SPDX-FileCopyrightText: Copyright 2008-2010 John Smith
SPDX-FileCopyrightText: Copyright Example Company
SPDX-FileCopyrightText: Copyright contributors to the Foo project.
```

File contributors (see [8.14](file-information.md#8.14)):

```text
SPDX-FileContributor: Modified by Jane Doe
SPDX-FileContributor: The Regents of the University of California
```

SPDX file tags of a particular type may appear one or multiple times in a file, depending on the corresponding cardinality defined for that field in the File Information section of the SPDX specification.

Multiple-line values are not recommended, because doing so will make it harder for simple search tools to extract all data by looking only for lines beginning with the relevant tag.

Version 3.0 of the [REUSE Software guidelines](https://reuse.software/spec/) implements this format, via a recommendation to use the tag `SPDX-FileCopyrightText:` to include copyright notices as part of a file's comment headers.

## H.3 Caveats <a name="H.3"></a>

A creator of an SPDX document may elect to disregard any or all file tags in any file. SPDX document creators should determine for themselves the extent to which they will rely upon the information specified in a file tag.

Not all fields in the File Information section will be useful or relevant to use as file tags. For example, `SPDX-FileName` is unnecessary as it can be easily derived from the actual file name; `SPDX-SPDXID` is likely to be ignored by an SPDX document creator who may need to define their own SPDXRef- ID system for their document; etc.

The short-form license identifiers described in Annex [E](using-SPDX-short-identifiers-in-source-files.md) do not follow the file tag convention described above. The `SPDX-License-Identifier` emerged from the broader community prior to being defined in the SPDX specification, so it does not map to a `License-Identifier` field in the File Information section.
