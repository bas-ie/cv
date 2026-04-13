# cv

## Prerequisites

- [mise](https://mise.jdx.dev/) for task running and tool management
- TeX Live 2023 at `/usr/local/texlive/2023` (already installed from the `install-tl` bundle)

If the system TeX Live is unavailable, uncomment `tinytex = "latest"` in `.mise.toml` for a mise-managed fallback. The first build will fetch missing packages via `tlmgr` on demand.

## Setup

```sh
mise trust
```

This activates `.mise.toml`, which puts `/usr/local/texlive/2023/bin/x86_64-linux` on PATH for the project directory.

## Tasks

| Task | Description |
| --- | --- |
| `mise run build` | Build `main.pdf` with pdflatex via latexmk (default; matches Overleaf's pdftex branch) |
| `mise run build-xe` | Build with XeLaTeX (fontspec branch of `main.tex`) |
| `mise run watch` | Continuous rebuild on save (`latexmk -pvc`) |
| `mise run clean` | Remove build artefacts, keep `main.pdf` |
| `mise run clean-all` | Remove all build artefacts including `main.pdf` |
| `mise run publish` | Build and copy to `Rich_Churcher_<year>_CV.pdf` |

## Editing in Neovim

Pair with [VimTeX](https://github.com/lervag/vimtex):

```lua
-- lazy.nvim example
{
  "lervag/vimtex",
  init = function()
    vim.g.vimtex_compiler_method = "latexmk"
    vim.g.vimtex_view_method = "zathura"
  end,
}
```

VimTeX picks up `latexmk` from the mise-activated PATH automatically.

## Notes

- The `main.tex` has an `\ifxetex` branch. The pdftex path is the default and currently the only one that renders `fontawesome` icons correctly.
- The stray `latexmk` file in the repo root is a legacy Overleaf `.latexmkrc` with broken smart-quote characters — not used by the system `latexmk` binary.
