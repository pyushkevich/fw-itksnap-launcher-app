# fw-itksnap-launcher-app

A minimal [Flywheel viewer extension app](https://docs.flywheel.io/Developer_Guides/extension_apps/)
that opens the selected image in [ITK-SNAP](http://www.itksnap.org) via its
`itksnap-fw://` URL handler.

When invoked on a file, the app builds a URL of the form

```
itksnap-fw://<flywheel-host>/acquisitions|analyses/<container-id>/files/<filename>
```

and asks the browser to open it. If the browser blocks the automatic launch, click
the **Open in ITK-SNAP** button.

## Requirements

- ITK-SNAP 4.6 or later, installed so that the `itksnap-fw://` scheme is registered
- A Flywheel API key that ITK-SNAP can use (run `fw login`, or enter the key when ITK-SNAP prompts)
- The file must be attached to an acquisition or an analysis

## Installation

1. Host `index.html` on an HTTPS server that all Flywheel users can reach.
2. In Flywheel, register a new **Viewer** application (site or project level),
   using the hosted URL and matching the file types you want (e.g. `nifti`, `dicom`).
3. Optionally, set the Application Options to `{"server": "<host>"}` if the
   Flywheel API host differs from the host serving the Flywheel web UI.
