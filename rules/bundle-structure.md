# OKF Bundle Structure Rules

A bundle is a directory tree of markdown files. The directory structure is independent of the domain: producers organize concepts however makes sense for the knowledge being captured.

## Directory Layout

```
path/to/bundle/
  index.md                      # Optional. Directory listing for progressive disclosure.
  log.md                        # Optional. Chronological history of updates.
  <concept>.md                  # A concept at the bundle root.
  <subdirectory>/               # Subdirectories organize concepts into groups.
    index.md
    <concept>.md
    <subdirectory>/
      ...
```

## Distribution Methods

A bundle MAY be distributed as:

- A git repository (recommended, since it provides history, attribution, and diffs).
- A tarball or zip archive of the directory.
- A subdirectory within a larger repository.

## Directory Organization Principles

- Organize concepts into logical groups using subdirectories.
- Use descriptive directory names (e.g., `tables/`, `metrics/`, `playbooks/`).
- Include `index.md` files in subdirectories for progressive disclosure.
- Follow existing domain conventions when organizing.