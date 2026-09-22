# Changelog

User-visible changes, reconstructed from repository history. Historical entries
use Git tags and release-preparation commits; they have not been checked against
the published Hex archives. Some tags precede their matching `gleam.toml` version
bump. In particular, the `v2.0.0` tag points to `06ee23f`; the 2.0.0 entry below
also includes the subsequent release commits `0036585` and `34dd8c6`.

## 2.0.1 — Unreleased

- Fix JSX output to preserve valid named and numeric HTML entities in text and
  quoted attributes, matching HTML output. For example, `&#8288;` now remains
  `&#8288;` rather than becoming `&amp;#8288;` and displaying literally.
- Continue escaping bare ampersands, unknown entity-like strings, and JSX syntax
  characters. XML output is unchanged.
- Add regression tests for HTML/JSX entity parity, decimal and hexadecimal
  references, literal entity spellings, and quoted attributes.

**Compatibility:** To display the literal text `&nbsp;` in JSX, supply
`&amp;nbsp;`. Previously, supplying `&nbsp;` displayed it literally; it now
produces a nonbreaking space. Public function signatures are unchanged.

## 2.0.0

- **Breaking:** Replace `parse_input_lines`, `parse_string`, and `parse_file`
  with explicit single-root and multiple-root APIs: `input_lines_to_vxml(s)`,
  `string_to_vxml(s)`, and `path_to_vxml(s)`. Single-root parsing rejects missing
  or multiple roots.
- **Breaking:** Replace `parse_xml` and `parse_xml_input_lines` with
  `xml_to_vxml` and `xml_input_lines_to_vxml`; introduce `XMLParseError` and
  revise VXML parsing and validation error types.
- Expand serialized VXML tag names to XML's `Name` grammar, including hyphens,
  namespace colons, and supported non-ASCII characters. Tighten indentation
  validation and preserve non-indentation whitespace in input-line conversion.
- Refine XML parsing, including character references, comments, doctype
  declarations, and malformed-input diagnostics. XML parsing decodes
  supported references into character data; XML output escapes character data.
- Add `html_to_vxml`, combining HTML repairs with parsing that accepts unquoted
  attribute values and preserves recognized HTML entity spellings.
- Preserve recognized named and numeric entities in HTML output while escaping
  bare ampersands and unknown entity-like strings. Add `vxml_to_html` and
  `vxmls_to_html` string-output helpers.
- Add `html_entities_to_unicode` and `unicode_to_named_html_entities`, with
  configurable exceptions and syntax, spacing, invisible, and layout presets.
- Define JSX escaping for text and quoted attributes, and exact boolean/integer
  attribute emission. Entity preservation is corrected in 2.0.1 above.

## 1.0.9

- Preserve leading spaces and tabs in serialized VXML attribute values during
  parsing and round trips.
- Reject trailing spaces and tabs in attribute values during parsing,
  validation, and serialization; document the whitespace contract.

## 1.0.8

- Move the helper modules `xml_streamer` and `vxml_html_repair` into the
  `vxml/xml_streamer` and `vxml/html_repair` namespaces. Direct importers need to
  update their module paths.
- Update README documentation.

## 1.0.7

- Update README documentation and package badges; no runtime changes.

## 1.0.6

- Add `validate` and `VXMLValidationError` for recursively checking a tree's
  tags, attributes, text lines, and nonempty text-node line collections.
- Document validation and the distinction between constructing a tree and
  ensuring it can be serialized as VXML.

## 1.0.5

- Add XML serialization through `vxml_to_xml`, `vxmls_to_xml`, and their
  output-line variants. Preserve mixed-content whitespace, escape XML text and
  attributes, and emit empty elements as self-closing tags.
- Allow blame-table margin columns to be hidden by setting their maximum width
  to zero.
- Recognize complete named, decimal, and hexadecimal entity-reference syntax
  when deciding which ampersands to escape.

## 1.0.4

- **API change:** Make VXML serialization and `vxml_table` fallible, returning
  `Result` with a `VXMLSerializationError` on invalid input. Errors retain the
  offending value's blame and the valid output produced before the error.
- Reject malformed tags, attribute keys and values, empty text nodes, and text
  lines containing carriage returns or newlines during VXML serialization.
- Update package metadata and remove tracked build artifacts.

## 1.0.3

- Correct attribute-key validation: reject `=`, spaces, tabs, carriage returns,
  and newlines rather than the previous punctuation-based restrictions.
- Add `validate_value` and `BadValue` to reject carriage returns and newlines
  in attribute values.

## 1.0.2

- Bump the package version; no source-code changes relative to the preceding
  tag.

## 1.0.1

- Update README documentation; no library source-code changes relative to
  1.0.0.

## 1.0.0

- Initial tagged package release: the `V`/`T` tree model, attributes and text
  lines with source provenance, serialized VXML parsing and output, HTML and
  JSX output, XML-like input parsing, HTML repair helpers, and blame-aware
  line/table utilities.
