# Best practices

## Content creation

###  The SWUMP criteria

All training material destined for CDS/ADS/CADS portals must satisfy the SWUMP criteria:

* **S**elf-explanatory: Steps are clearly, correctly and succinctly explained.
* **W**ell structured: Logical flow and aesthetically pleasing layout with a balanced mix of Markdown and code.
* **U**sable: Notebook runs to completion **without errors** and uses only outputs/widgets compatible with JupyterBook.
* **M**eaningful: Provides an authentic, value-adding use-case for CDS/ADS/CADS data.
* **P**roficient: Passes the code-standards tests (see [quality assurance](quality-assurance.md)).


### Filenames

Filenames should use human-readable *slugs* that capture the notebook’s key themes, particularly those that distinguish it from other notebooks in the repository.  

- **Do not** include contract numbers or version identifiers in filenames.  
- Contract numbers, where required, may be referenced in the Pull Request that introduces or modifies the notebook.  
- File versioning is managed automatically through GitHub and should not be duplicated in filenames.


### Scope

Focus on one topic / visualisation / processing routine. Consider separate notebooks if multiple parts or topics are included.

:::{note} User-centric approach
The [Diátaxis documentation framework](../explanation/diataxis.md) is there to help you structure your content in a user-centric way.
:::

#### Pedagogical ordering

Within a single notebook, present material in **increasing order of complexity**:

- Introduce context, prerequisites, and the workflow before the analysis.
- Place the simplest, most representative example first; build up to more advanced cases.
- Place caveats, edge cases, and advanced extensions **after** the core demonstration, not interleaved with it.

Diátaxis governs *which kind of notebook* you are writing; pedagogical ordering governs *the order of material within it*.


### Titles

When selecting titles for your notebooks, consider the needs of a broad and diverse audience.  

Training notebooks serve as entry points to the subject matter and should therefore be titled in a way that is clear, accurate, and accessible. Titles must be:  
- **Concise** – easy to read  and limited to fewer than 80 characters.
- **Accurate** – clearly reflect the notebook’s content and purpose.  
- **Accessible** – avoid acronyms, abbreviations, or technical jargon that may not be widely understood.  

### Section headings

- Keep headings in separate cells
- Use `#` for first level headings, `##` for second level, and so on. Do not skip a level (e.g. do not follow a 1st level heading with a third level, without a second level in between).


### TOC
Keep the table of contents (TOC) clear and intuitive, that is, avoid long lists that clutter the view. See the official [MyST Markdown documentation](https://mystmd.org/guide/table-of-contents) for details on how to structure the table of contents. 


### Scientific terminology

Define acronyms and domain-specific terminology **on first use** in the prose. Where a term has an authoritative definition elsewhere, link to that source instead of redefining it in the notebook.

- *Example:* "...the **climatology** (the long-term average of a variable over a 30-year reference period) of 2 m temperature..."
- For unfamiliar acronyms, write the expansion at first use: "**ECMWF** (European Centre for Medium-Range Weather Forecasts)".

A standalone `## Definitions` section is **optional** in the notebook template and should be used only when the notebook introduces several novel terms; otherwise, defining on first use is preferred.


### Figures and visualisation

Every figure in a notebook must be **self-interpretable** without reference to surrounding prose:

- **Title** that names what the figure shows.
- **Axis labels with units** on every axis (`Temperature [°C]`, `Time [UTC]`, etc.).
- **Legend** whenever more than one series, mask, or category is plotted.
- **Caption** stating the data source, the time/region covered, and the attribution string for any reused image. DOIs or stable URLs preferred.
- **Honest scaling.** Do not crop or truncate axes in ways that exaggerate or hide effects; if a non-linear scale (log, symlog) is used, label it as such.
- **Sufficient image quality.** Save raster outputs at a resolution that remains legible when the book is rendered (typically ≥ 150 dpi); prefer vector formats (`SVG`, `PDF`) where appropriate.

Storage and reuse:

- Store notebook-specific images in `./content/img/`.
- For images reused across repositories (e.g. logos), link to an external URL such as <https://climate.copernicus.eu/branding-guidelines#Logolines>. Images not already online can be uploaded to a dedicated repository for training. In that case, please contact <chris.stewart@ecmwf.int>.
- Refer to the [MyST documentation](https://mystmd.org/guide/figures) for how to include figures.

#### Visual style and ECMWF guidelines

For visual styling decisions in plots and figures, consult the **ECMWF visual style guide** *(link to be added by the maintainer once the canonical URL is confirmed)*. The guide governs plot-level rules: typography, colour usage, gridlines, and chart conventions.

You do **not** need to manually embed ECMWF or service logos in individual notebooks: the book-level branding (`branding/c3s.yml`, `cams.yml`, `ecmwf.yml`) and `myst.yml` configuration take care of logo placement at the rendered-book level.

#### Colour-vision-deficiency-safe palettes

Colour choice is the single most common visualisation issue flagged in expert review. ECMWF acknowledges the gap (Hewson, 2022) but has not yet published a normative palette specification, so the rules below cite community standards that meet or exceed any plausible future guideline.

**Universal rule.** *"If a colour palette is readable in black and white after being desaturated, it is universally accessible to all viewers."* (Crameri *et al.*, 2020) Authors should also simulate colour-vision deficiency (CVD) on every published figure using the [Coblis colour-blindness simulator](https://www.color-blindness.com/coblis-color-blindness-simulator/) — the same tool referenced in Hewson (2022).

**Choose the palette by data type.** Sequential, diverging, categorical, and cyclic data each require a different palette family; using the wrong family is as serious as using a CVD-unsafe one.

| Data type | Recommended palettes | Avoid |
|---|---|---|
| **Sequential** (e.g. temperature, precipitation, concentration) | matplotlib built-ins: `viridis`, `cividis`, `plasma`, `inferno`, `magma`. Richer set: `batlow`, `lajolla`, `lapaz` (`cmcrameri`). Oceanographic: `cmocean.thermal`, `cmocean.haline`. | `jet`, `rainbow`, `gist_rainbow`, `hsv` |
| **Diverging** (anomalies, biases, departures from a reference) | matplotlib: `RdBu_r`, `PuOr`, `BrBG`. Richer set: `vik`, `roma`, `bam` (`cmcrameri`). Oceanographic: `cmocean.balance`, `cmocean.curl`. | `seismic` (luminance non-monotonic); red–green diverging maps without a luminance change |
| **Categorical / qualitative** | matplotlib `tab10`; the Wong 8-colour palette (Okabe–Ito); `cmcrameri.cm.categorical`. Keep to **≤ 8** categories on a single map — split or facet otherwise. | More than ~8 categories; bespoke colour mixes that have not been CVD-tested |
| **Cyclic** (wind direction, phase, time of day) | matplotlib `twilight`, `twilight_shifted`. Richer set: `romaO`, `vikO`, `corkO` (`cmcrameri`). | Non-cyclic palettes with a visible seam |
| **Radar / weather domain** | `cmweather` colormaps (e.g. `ChaseSpectral`, `LangRainbow12`) — designed for CVD readers (Sherman *et al.*, 2024). | Legacy NWS rainbow-style radar palettes |

**Default Python recipe (zero install cost).** matplotlib built-ins are sufficient for most training notebooks:

```python
import matplotlib.pyplot as plt
plt.imshow(data, cmap="viridis")     # sequential
plt.imshow(anomaly, cmap="RdBu_r")   # diverging
```

For richer palettes, install on demand and add to `environment.yml`:

```bash
pip install cmcrameri    # Crameri scientific colour maps
pip install cmweather    # radar/meteorology, CVD-friendly (Sherman et al., 2024)
pip install cmocean      # oceanographic / atmospheric
```

```python
import cmcrameri.cm as cmc
plt.imshow(data, cmap=cmc.batlow)
```

**Authority references.** Cite at least one of these when a notebook applies a non-default palette, so reviewers can verify the choice against a stated source:

- Crameri F., Shephard G. E., Heron P. J. (2020). *The misuse of colour in science communication.* Nature Communications 11, 5444. <https://doi.org/10.1038/s41467-020-19160-7>
- Sherman Z. *et al.* (2024). *Effective Visualization of Radar Data for Users Impacted by Color Vision Deficiency.* BAMS 105(8). <https://doi.org/10.1175/BAMS-D-23-0056.1>
- Rocchini D. *et al.* (2023). *Scientific maps should reach everyone: The cblindplot R package to let colour blind people visualise spatial patterns.* Ecological Informatics 76, 102045. <https://doi.org/10.1016/j.ecoinf.2023.102045>
- Hewson, T. (2022). *Creative Use of Colour to Satisfy Different User Needs.* UEF 2022, ECMWF.


### Data files

Data files should not be stored in the GitHub repository, but hosted externally and linked to, or downloaded from the original source (e.g. CDS/ADS).

#### Trusted data sources

Cite each dataset using a **DOI, an equivalent persistent identifier, or a stable URL with named authoritative provenance**. Acceptable provenance includes:

- Copernicus services (CDS, ADS, CAMS, CADS) and their dataset DOIs.
- Peer-reviewed datasets accompanied by a DOI.
- Official agency products (ECMWF, NOAA, NASA, ESA, national meteorological services) accessed via their official URLs.
- Other authoritative sources where provenance can be unambiguously named.

DOI-only is *not* the only acceptable form: a stable, versioned URL from a recognised authority is also acceptable when no DOI exists.


## Code

### Code commenting and annotation

For code logic to remain clear to a non-technical audience:

- Add a **one-line inline comment** at the top of each non-trivial code block stating *what* it does and *why*.
- Provide a **docstring** for any custom function (purpose, arguments, return value).
- Worked example:

```python
# Compute the monthly climatology over the reference period
# (mean across years for each calendar month).
def monthly_climatology(da, period=("1991", "2020")):
    """Return the monthly climatology of a DataArray.

    Parameters
    ----------
    da : xarray.DataArray
        Time-indexed input data.
    period : tuple of str
        (start_year, end_year) reference period, inclusive.

    Returns
    -------
    xarray.DataArray
        12-element climatology indexed by month.
    """
    return da.sel(time=slice(*period)).groupby("time.month").mean("time")
```

:::{important} Comments and docstrings are *not* a substitute for prose
Inline comments and docstrings address code-level clarity. The separate requirement to **interleave markdown cells between logical code blocks** (so the reader sees the scientific narrative alongside the code) is satisfied by the notebook structure itself, not by inline comments alone. Make sure each logical code block in your notebook is preceded by a markdown cell that explains the step in plain language.
:::


## References and attribution

Every notebook must list its underlying datasets, publications, and reused figures in the `## References` section of the notebook template. Use the formats below.

### Datasets

Cite by DOI where available; otherwise by a stable URL plus the named authoritative provider.

- *Example (DOI):* Hersbach, H., Bell, B., Berrisford, P., et al. (2023). *ERA5 monthly averaged data on single levels from 1940 to present.* Copernicus Climate Change Service Climate Data Store. <https://doi.org/10.24381/cds.f17050d7>

### Publications

Use a consistent citation style (APA is the default for ECMWF training material). For reproducibility-sensitive material, also provide a BibTeX entry.

- *APA example:* Author, A. B., & Author, C. D. (Year). Title of the article. *Journal Name*, *vol*(issue), pages. <https://doi.org/...>
- *BibTeX:*

```bibtex
@article{author2024title,
  author  = {Author, A. B. and Author, C. D.},
  title   = {Title of the article},
  journal = {Journal Name},
  year    = {2024},
  volume  = {12},
  number  = {3},
  pages   = {45--67},
  doi     = {10.xxxx/xxxxx}
}
```

### Reused figures

State the source URL and the licence string under which the figure is reused (e.g. `CC-BY-4.0`, `Crown Copyright`, `© ECMWF`). Match the licence to the original publication.


## Tools


### MyST markdown
Use enhanced markdown features (e.g. colored cells, icons) provided by [MyST markdown](https://mystmd.org/) to enhance your notebooks.


### Cross-references & placeholder links
Avoid HTML `<a>` tags without `href` and notebook cross-references built with plain HTML; they render poorly and flood the build with warnings.


:::{warning} HTML tags
Refrain from using raw HTML—JupyterBook’s config may override or mis-render it. Markdown covers all required formatting.
:::


## Metadata

Apply metadata at the notebook level and at the cell level according to a metadata-schema described here: https://github.com/ecmwf-training/jn-metadata-schema.
