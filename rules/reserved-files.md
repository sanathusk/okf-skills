# OKF Reserved Files

The following filenames have defined meaning at any level of the hierarchy and MUST NOT be used for concept documents:

## Reserved Filenames

| Filename   | Purpose                          | Has frontmatter? |
|------------|----------------------------------|-----------------|
| `index.md` | Directory listing for progressive disclosure | NO* |
| `log.md`   | Change history, newest first | NO |

*Exception: bundle-root `index.md` MAY have frontmatter with `okf_version: "0.2"`.

## Index Files (`index.md`)

An `index.md` file MAY appear in any directory, including the bundle root. It enumerates the directory's contents to support progressive disclosure.

**Structure:**
- No frontmatter (except bundle-root MAY have `okf_version`)
- Body uses one or more sections, each grouping concepts under a heading
- Entries SHOULD include the description from the linked concept's frontmatter

**Example:**
```markdown
# Section / Group Heading

* [Title 1](relative-url-1) - short description of item 1
* [Title 2](relative-url-2) - short description of item 2

# Another Section

* [Subdirectory](subdir/) - short description of the subdirectory
```

## Log Files (`log.md`)

A `log.md` file MAY appear at any level of the hierarchy to record the history of changes to that scope.

**Structure:**
- No frontmatter
- Flat list of date-grouped entries, newest first
- Date headings MUST use ISO 8601 `YYYY-MM-DD` form
- Log entries are prose; the leading bold word (`**Update**`, `**Creation**`, `**Deprecation**`) is a convention, not a requirement

**Example:**
```markdown
# Directory Update Log

## 2026-05-22
* **Update**: Added a BigQuery table reference for [Customer Metrics](/tables/customer-metrics.md).
* **Creation**: Established the [Dataplex Playbook](/playbooks/dataplex.md).

## 2026-05-15
* **Initialization**: Created foundational directory structure.
```