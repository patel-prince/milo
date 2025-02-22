# PDF Viewer

## Feature Branch Testing
The client ids are specific to the origin (no wildcards), so the stage **pdfViewerClientId** only works for **main--milo--adobecom.aem.page**. If you want to test the pdf on a feature branch, you need to create a new temporary client id. Alternatively, you can name your branch **pdf-viewsdk** and use the existing client id that's set up for **pdf-viewsdk--milo--adobecom.aem.page**. You can find it in the [developer console](https://developer.adobe.com/console/) under "Milo PDF Viewer Branch".

How to create a new client id:
1. Got to https://acrobatservices.adobe.com/dc-integration-creation-app-cdn/main.html?api=pdf-embed-api.
2. It will prompt you to log in if you're not already.
3. Add a name and the domain of your feature branch to create the credential.
4. Copy client id and temporarily add it to the pdf-viewer code in place of the permanent credentials.
5. Push up to your feature branch to verify.
6. Once you're done, remove the temporary client id from the code and delete it from the [developer console](https://developer.adobe.com/console/).

## Using in a Consumer Repo
You'll need to create client IDs for your consumer domains and add them to your config.

```
// scripts.js
const CONFIG = {
  stage: {
    ...
    pdfViewerClientId: '<CLIENT_ID>',
    pdfViewerReportSuite: '<REPORT_SUITE_ID>',
  },
  prod: {
    pdfViewerClientId: '<CLIENT_ID>',
    pdfViewerReportSuite: '<REPORT_SUITE_ID>',
  },
  // The following envs are non-standard and used specifically for this block
  page: {
    pdfViewerClientId: '<CLIENT_ID>', // client id for aem.page domain
    pdfViewerReportSuite: '<REPORT_SUITE_ID>',
  },
  live: {
    pdfViewerClientId: '<CLIENT_ID>', // client id for aem.live domain
    pdfViewerReportSuite: '<REPORT_SUITE_ID>',
  },
  hlxPage: {
    pdfViewerClientId: '<CLIENT_ID>',
    pdfViewerReportSuite: '<REPORT_SUITE_ID>',
  },
  hlxLive: {
    pdfViewerClientId: '<CLIENT_ID>',
    pdfViewerReportSuite: '<REPORT_SUITE_ID>',
  },
  ...
};

(async function loadPage() {
  const { loadArea, setConfig } = await import(`${LIBS}/utils/utils.js`);
  setConfig({ ...CONFIG, miloLibs: LIBS });
  await loadArea();
}());
```

## Resources
- Product Documentation: https://developer.adobe.com/document-services/docs/overview/pdf-embed-api
- Inline Mode demo: https://acrobatservices.adobe.com/view-sdk-demo/index.html#/view/IN_LINE/Bodea%20Brochure.pdf
