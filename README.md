# Printable

Barebones printable hugo theme for technical writing. Intended to be
complementary to [docdock](https://github.com/vjeantet/hugo-theme-docdock) and
other unprintable documentation themes.

## Notes

- "/" is meant to be used as cover page with wkhtmltopdf.
- `_footer.md` is used for footer customization much like in docdock
- `.no-print` elements are hidden when printing
- font-awesome is included for convenience
- slightly modified [example breadcrumb partial](https://gohugo.io/content-management/sections/#example-breadcrumb-navigation) included in header for basic navigation. 

## PDF Generation Example

This produces a PDF with a cover page, table of contents, and numbered pages.

```bash
docker run -d --volume "$PWD:/tmp/wkhtmltopdf" \
    --name wkhtmltopdf cs2ag/docker-wkhtmltopdf
docker container exec wkhtmltopdf \
    wkhtmltopdf --footer-right [page] --header-right [page] \
        --print-media-type --keep-relative-links --disable-external-links \
        --disable-internal-links cover host.docker.internal:1313/ \
        toc --toc-text-size-shrink 1 \
        page host.docker.internal:1313/overview/ \
        page host.docker.internal:1313/security/ \
        page host.docker.internal:1313/config/ \
        /tmp/wkhtmltopdf/out.pdf
```
