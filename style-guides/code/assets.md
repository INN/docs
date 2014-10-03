# Best Practices for Assets

**Note:** for now, this document only covers best practices for assets as they apply to the [INN app template](https://github.com/INN/app-template).

### General

* When using the INN app template, use the [assets rig](https://github.com/INN/app-template/blob/master/PROJECT_README.md#save-media-assets). Do **not** commit assets to the project repository.  

### Photos

* Images should be stored with the following path convention: `www/assets/img/$SECTION_NAME/$SLUG$VERSION.jpg`
* `$SECTION_NAME` can be whatever project specific section slug is appropriate (chapter, slide, page, etc.)
* `$SLUG` should follow URL conventions: all lowercase, no whitespace, dashes instead of underscores.
* `$VERSION` may be:

<table>
  <tr><th>$VERSION</th><th>aspect ratio</th><th>target</th><th>resolution</th></tr>
  <tr><td></td><td>original</td><td>archival</td><td>full</td></tr>
  <tr><td>-16x9</td><td>16x9</td><td>archival</td><td>full</td></tr>
  <tr><td>-sq</td><td>square</td><td>archival</td><td>full</td></tr>
  <tr><td>-16x9-d</td><td>16x9</td><td>desktop</td><td>1200x675</td></tr>
  <tr><td>-16x9-m</td><td>16x9</td><td>mobile</td><td>400x225</td></tr>
  <tr><td>-sq-m</td><td>square</td><td>mobile</td><td>420x420</td></tr>
</table>

* File extenions should always be lowercase.
