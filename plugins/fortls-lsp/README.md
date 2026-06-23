# fortls-lsp

Fortran language server ([fortls](https://fortls.fortran-lang.org/)) for Claude Code, providing
code intelligence and analysis across free-form and fixed-form Fortran. Once installed, Claude's
built-in LSP tool gains go-to-definition, find-references, symbol search, hover, and diagnostics
over your `.f90` modules — useful for navigating large scientific/HPC codebases.

## Supported Extensions

- **Free-form:** `.f90` `.F90` `.f95` `.f03` `.F03` `.f08` `.F08`
- **Fixed-form:** `.f` `.F` `.for` `.FOR` `.f77` `.F77` `.fpp` `.FPP`

## Installation

`fortls` is distributed on PyPI.

### Via pip (recommended)
```bash
pip install fortls
```

### Via pipx (isolated environment)
```bash
pipx install fortls
```

### Verify
```bash
fortls --version
```

The plugin invokes `fortls` over stdio; no extra configuration is required. Drop a
[`.fortls`](https://fortls.fortran-lang.org/options.html) JSON file at a project root to set
include/source directories or preprocessor definitions for that project.

## More Information
- [fortls documentation](https://fortls.fortran-lang.org/)
- [GitHub Repository](https://github.com/fortran-lang/fortls)
