# Best practices

## Content creation

###  The SWUMP criteria

All training material destined for CDS/ADS/CADS portals must satisfy the SWUMP criteria:

* **S**elf-explanatory: Steps are clearly, correctly and succinctly explained.
* **W**ell structured: Logical flow and aesthetically pleasing layout with a balanced mix of Markdown and code.
* **U**sable: Notebook runs to completion **without errors** and uses only outputs/widgets compatible with JupyterBook.
* **M**eaningful: Provides an authentic, value-adding use-case for CDS/ADS/CADS data.
* **P**roficient: Passes the code-standards tests (see [Run code standards tests](../howto/run-code-standards-tests.md)).


### Filenames

Filenames should use human-readable *slugs* that capture the notebook’s key themes, particularly those that distinguish it from other notebooks in the repository.  

- **Do not** include contract numbers or version identifiers in filenames.  
- Contract numbers, where required, may be referenced in the Pull Request that introduces or modifies the notebook.  
- File versioning is managed automatically through GitHub and should not be duplicated in filenames.


### Scope

Focus on one topic / visualisation / processing routine. Consider separate notebooks if multiple parts or topics are included.

:::{note} User-centric approach
The [Diátaxis documentation framework ](../explanation/diataxis.md)is there to help you structure your content in a user-centric way.
:::


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


### Images
- Store notebook-specific images in `./content/img/.`
- For images reused across repositories (e.g. logos) link to an external URL such as https://climate.copernicus.eu/branding-guidelines#Logolines. Images not already online can be uploaded to a dedicated repository for training hosted at https://sites.ecmwf.int/training/ (please contact [chris.stewart@ecmwf.int](mailto:chris.stewart@ecmwf.int)).
- Refer to the [MyST documentation](https://mystmd.org/guide/figures) for how to include figures.

### Data files

Data files should not be stored in the Github repository, but hosted externally and linked to, or downloaded from original source (e.g. CDS/ADS).



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

