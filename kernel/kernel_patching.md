# Kernel Patching

This document describes the procedures and policies regarding pulling in changes that are currently not merged in the upstream stable kernel. The intention of this document is to reduce the burden of maintaining the kernel when updating major revisions by making it easier to tack the status of additions to the previous version. When creating a new Pull Request, review this document to ensure that your changes are adhering to these standards.

## Cover letter

The Pull request summary has the same purpose as the cover letter in upstream kernel mailing lists - to outline the purpose of the changes, describe the thought process behind them, and outline any considerations for other developers. It should also accurately track the history and source of the original patches as well as the reasons for dropping the patch(es) or maintaining them during the next major version.

### Example

```
input: hid: Add driver for device

Adds driver for some device. This device is designed with such and such endpoints
and those each do a thing or whatever. We're currently attaching to the first
endpoint and forwarding the remaining events so that some other stuff doesn't
break. Yada Yada yada. Patch 1 creates the baseline driver to conenct to the
device, patch 2 as the first logical group of attributes... and so on.

This patch series was accepted into kernel 7.0. Drop after 6.19.

link:
https://lore.kernel.org/some/url

Signed-off-by: Person A. Ding <dev-email@email.dev>

```

## Patches

Individual patches should retain their original authorship. The message and title should be modified to make searching for the patches easier during review for a major revision update and the submitter must re-sign the patch. Upstream backports should be cherry-picked.

### Patch Title Prefixes

Valid patch title prefixes are as follows:

`[FROM-ML]`- Patch has been submitted upstream but has not yet been pulled into the subsystem next branch

`[FROM-UPSTREAM]` - Patch is being backported from linux-next or a later stable kernel.

`[FOR-UPSTREAM]` - Patch has not yet been submitted to the kernel mailing list, but will be. As our policy defaults to upstream first, this tag must have a reasonable justification for inclusion prior to being accepted in the OGC kernel.

`[NOT-FOR-UPSTREAM]` - Patch is not acceptable in its current form for submitting upstream, but fills a need temporarily. NOT-FOR-UPSTREAM patches must be re-justified during every major revision and should identify the plan for replacement.

`[EXTERNALLY-MAINTAINED]` - Patch is not from upstream and fixes a valid need, but is maintained by an organization outside of the OGC and therefore they are the responsible party for upstreaming.

### Example

```
[FROM-UPSTREAM] [Patch 1/8] input: hid: Add discovery for device

Adds discovery driver for a specific HID device. This part is verbatim the original commit message.

Signed-off-by: Original D. Veloper <original@signature.com>

cherry-picked from commit 123acb345def
Signed-off-by: Person A. Ding <dev-email@email.dev>
```
