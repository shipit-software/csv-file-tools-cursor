# CSV File Tools for Cursor

Connect Cursor to [CSV File Tools](https://csvfile.tools/mcp) to inspect and transform explicitly supplied CSV text. This plugin contains remote MCP configuration and documentation only.

The remote endpoint is `https://csvfile.tools/api/csv/mcp`. It requires no account, API key, or authorization header. A compatible Cursor client and internet connection are required.

## Tools

- `inspect_csv`: record, column and cell counts; up to 20 preview records.
- `filter_csv_rows`: exact string equality in a selected zero-based column.
- `sort_csv_rows`: stable literal string ordering; no number/date inference.
- `edit_csv_cells`: replace existing cells using zero-based row/column indices; row zero includes the header.

Each call accepts CSV text, not a file path or URL, with a 256 KiB UTF-8 input/output limit, 50,000 cells and 200 columns. At most 1,000 edits are accepted per call. Choose comma, tab, semicolon or pipe explicitly; comma is the default. Sort/filter preserve the first record as a header unless `hasHeader` is false. Values remain strings; formulas are never evaluated.

## Use

After installing and enabling the plugin in Cursor, try pasted data first:

> Inspect this CSV: `Name,Status\nBea,Active\nAda,Inactive\nCal,Active` (replace the literal `\n` sequences with newlines). Keep Status exactly Active, sort Name ascending, then change Bea to Beth. Show the result.

Expected final CSV:

```csv
Name,Status
Beth,Active
Cal,Active
```

For a local file, explicitly ask Cursor to read your selected file, call the tools and show returned CSV. Ask it to save a separate output only after you approve. File access and saves use Cursor's own permissions; this server has no filesystem authority.

For manual setup without the plugin, copy the `mcpServers` object in `mcp.json` into your Cursor MCP configuration, avoiding duplicate registrations.

## Data and support

CSV text and requested changes are sent to CSV File Tools for server-side processing. The tools process one request in memory without persisting CSV contents, fetching URLs or reading local paths. Hosting infrastructure receives ordinary network request data; your AI client may retain conversations and tool results under its own policy. Review the [privacy policy](https://csvfile.tools/privacy), [terms](https://csvfile.tools/terms) and [support page](https://csvfile.tools/support).

This connector does not open an embedded editor or access Loam accounts, governed tables or browser-editor documents.

## License

The following MIT license applies only to this repository's connector configuration and documentation. The hosted CSV service, website and product implementation are separate and are not licensed by this repository.

Copyright (c) 2026 Shipit Software

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
