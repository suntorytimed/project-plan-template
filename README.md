# Project Plan Template
An ASCIIdoc template for a project plan following IPMA standards, which can be released on Confluence by using the `confluencepublisher/confluence-publisher:0.0.0-SNAPSHOT` container.

## Build PDF
```bash
cd docs/project-plan
asciidoctor -a pdf-theme=../stylesheets/theme.yml -a pdf-fontsdir=../fonts/static -r asciidoctor-diagram -r asciidoctor-pdf -b pdf project-plan.adoc
```

## Build HTML
```bash
cd docs/project-plan
asciidoctor -a stylesheet=../stylesheets/style.css -r asciidoctor-diagram project-plan.adoc
```

## Release via Confluence Publisher Docker image to Confluence
PAGE_TITLE_PREFIX, PAGE_TITLE_SUFFIX, VERSION_MESSAGE and MINOR_EDIT are optional. Be very careful with the SPACE_KEY and ANCESTOR_ID, as it will delete everything below the ANCESTOR_ID => don't use the Space homepage!
```bash
docker run --rm -e ROOT_CONFLUENCE_URL=https://confluence.example.com \
   -e USERNAME=username \
   -e PASSWORD=1234 \
   -e SPACE_KEY=XYZ \
   -e ANCESTOR_ID=012345 \
   -e PAGE_TITLE_PREFIX="Draft - " \
   -e PAGE_TITLE_SUFFIX=" (V 1.0)" \
   -e VERSION_MESSAGE="Docker deploy" \
   -e MINOR_EDIT: "true" \
   -v /absolute/path/to/asciidoc-root-folder:/var/asciidoc-root-folder \
   confluencepublisher/confluence-publisher:0.0.0-SNAPSHOT
```
