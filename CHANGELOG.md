# Changelog

What changed in Document Template XRay, newest first. A top-level bullet whose lead sentence is
bolded is something you will notice in the tool, and that sentence is what goes on the NuGet
page and in the XrmToolBox Tool Library; a bullet without one is about how the tool is built
and tested, and stays here.

## 1.2.21 — 22 October 2026

- **Nothing in the tool can be pressed while an answer from the environment is still on its
  way.** The panel XrmToolBox draws while a tool waits is a small box in the middle of it that
  disables nothing, so on a slow connection every button stayed live for the seconds an answer
  took. Now **Fetch from Dynamics** is dead while it is fetching, **Add Local File** while a
  template is being read, and the field pane empties when you open another template rather
  than describing the last one until the new one arrives. A refresh of the list keeps the
  template you had selected, instead of losing it and leaving the pane describing a template
  nothing in the list pointed at.

  ![Fetch from Dynamics, greyed out while it fetches](docs/changelog/fetch-dead-while-fetching.png)

- **An answer that arrives late is dropped, so closing the tab or opening another template
  mid-fetch is safe.** A tab closed while a fetch was out could put an error dialog up over
  whatever you had moved on to, and opening a second template left the first one still
  resolving its names into the pane. Each answer is now checked on arrival against what you
  are looking at, and the name lookups of a template you have left stop going out.

- **Switching to another environment clears the last one's templates, so one org's list is
  never shown as another's.** The list, and a field pane showing one of its templates, used to
  stay behind after the connection changed, and a fetch still out when you switched landed
  under the new environment's name. Files you added from disk stay. And pressing **Fetch from
  Dynamics** with no connection now asks for one and then fetches, instead of saying "not
  connected" and forgetting it was asked.

- **An environment that could not be reached says so, instead of looking like one with no
  templates in it.** The reason stays in the pane after the dialog is closed. In the same
  spirit, a blank Table or Column cell now only ever means the environment says there is no
  such table or column: when the names could not be read, a note beside the field count names
  the tables it could not ask about, rather than leaving you to guess which of the two it was.

  ![The reason a fetch failed, left in the pane](docs/changelog/fetch-could-not-be-reached.png)

- **Templates are read in the background, so opening a large .docx no longer freezes the
  window while it loads.** Decoding, unzipping and scanning a template all happened on the
  thread that draws the window: a 24 MB letterhead froze it for nearly half a second, and a
  template on a slow share froze it for as long as the share took. Each template is also read
  once rather than twice, and a table's metadata is fetched once rather than again for every
  template that uses it.

- The package's project page is now
  [comentality.com/tools](https://comentality.com/tools/#document-template-xray); the
  repository link stays on GitHub. Its description, in XrmToolBox and on NuGet, now says what
  the tool shows you: "See every field, relationship and repeating section a Word document
  template uses, as a flat list or a tree."
- `tests/slow.ps1` hosts the real control against a fake Dataverse with per-call latency and
  scripted failures, and plays twelve scenarios of ordinary gestures through it, with a
  screenshot per gesture. Every fix above is one of its scenarios, each red against the code
  it replaced.
- `/xtb` is a project skill that opens the tool in a private XrmToolBox; `xtb.ps1` finds the
  XtbSandbox module whichever edition of PowerShell installed it.
- `publish.ps1` refuses to publish when the nuspec release notes do not mention the version
  being shipped, or when this file has no section for it.

## 1.2.20

- **Renamed to "Document Template XRay", so a search for "xray" in the XrmToolBox Tool Library
  finds it.** The hyphen in "X-Ray" meant that search did not match the tool.
