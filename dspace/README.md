# DSpace files

These files add GeoCCMM to **CLARIN-DSpace 2026.2** (DSpace 7.6.5).

1. **Metadata schema.** Load `geoccmm-metadata.xml` with `dspace registry-loader -metadata geoccmm-metadata.xml`.
2. **Forms.** Add the three sections of `submission-forms.geoccmm.xml` to `config/submission-forms.xml`: `form-definitions`, `form-value-pairs` and `form-complex-definitions`. Add the same sections of `submission-forms_cs.geoccmm.xml` to `config/submission-forms_cs.xml`.
3. **Submission process.** Add the step definitions from `item-submission.geoccmm.xml` to `config/item-submission.xml`. Make a `geoccmm` process from a copy of CLARIN's `traditional` process, replacing its form pages (`traditionalpageone`, `traditionalpagetwo`) with the GeoCCMM steps: collection, identifiers, geoccmm-describe, geoccmm-where, geoccmm-access, geoccmm-curator, upload, license, clarin-license, specialFields. Then map the collection's handle to `geoccmm` in `submission-map`.
4. **DataCite.** Add `local.cfg.geoccmm` to `config/local.cfg`, and copy `crosswalks/DIM2DataCite-geoccmm.xsl` to `config/crosswalks/`. The stylesheet replaces DSpace's DataCite output for the whole repository. To register DOIs, also:
   - enable the `VersionedDOIIdentifierProvider` and `DataCiteConnector` beans in `config/spring/api/identifier-service.xml`;
   - schedule `dspace doi-organiser`.
5. **Publication date.** Give each GeoCCMM collection a template item with `dc.date.issued` set to `today`. DSpace replaces it with the date the item is approved.
6. **Interface.** Add the entries of `i18n/en.json5` and `i18n/cs.json5` to the user interface's `src/assets/i18n/en.json5` and `cs.json5`, or the same files in your theme, then rebuild the interface.

Before using the files, replace:
- `Your institution` (the publisher, in the stylesheet and in `local.cfg.geoccmm`);
- `10.XXXX` (your DOI prefix);
- `YOUR-DATACITE-REPOSITORY-ID` and `YOUR-DATACITE-PASSWORD` (in `local.cfg.geoccmm`).

The default metadata language is `ces` (Czech), in the forms and the stylesheet. Restart DSpace after you change its configuration.
