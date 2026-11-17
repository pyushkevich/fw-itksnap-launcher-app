# fw-itksnap-launcher-app

Minimal [Flywheel extension apps](https://docs.flywheel.io/Developer_Guides/extension_apps/)
that open images and workspaces in [ITK-SNAP](http://www.itksnap.org) via its
`itksnap-fw://` URL handler:

- `index.html` — a **file** viewer app that opens the selected file directly.
- `container.html` — a **container** app that lists the ITK-SNAP workspaces
  (`.itksnap`) and images in an acquisition, analysis, session, subject or
  project, in separate sections, and opens the one you click.

## File app (`index.html`)

When invoked on a file, the app builds a URL of the form

```
itksnap-fw://<flywheel-host>/acquisitions|analyses/<container-id>/files/<filename>
```

and asks the browser to open it. The app's frame then closes itself; it stays open
only to show an error message.

## Container app (`container.html`)

When invoked on a container, the app lists the container's files in two
sections, **ITK-SNAP workspaces** and **Images** (NIfTI, NRRD, MetaImage,
Analyze, MINC, GIPL, VTK, DICOM and the other formats ITK-SNAP reads, matched
by file extension). Clicking an entry opens

```
itksnap-fw://<flywheel-host>/<container-type>/<container-id>/files/<filename>
```

and closes the frame. On a session, the list also includes the files of the
session's acquisitions and analyses, under a heading for each container. Other
containers list only their own files. Analysis files listed are the analysis
outputs.
Opening a file attached to a session, subject or project needs ITK-SNAP 4.6
or later with support for those container types in `fw://` URLs.

## Requirements

- ITK-SNAP 4.6 or later, installed so that the `itksnap-fw://` scheme is registered
- A Flywheel API key that ITK-SNAP can use (run `fw login`, or enter the key when ITK-SNAP prompts)
- For the file app, the file must be attached to an acquisition or an analysis

## Installation

1. Host `index.html` on an HTTPS server that all Flywheel users can reach.
2. In Flywheel, register a new **Viewer** application (site or project level),
   using the hosted URL and matching the file types you want (e.g. `nifti`, `dicom`).
   For the container app, host `container.html` the same way and register it as
   an application on the container types you want (acquisition, analysis,
   session, …).
3. Optionally, set the Application Options to `{"server": "<host>"}` if the
   Flywheel API host differs from the host serving the Flywheel web UI.
