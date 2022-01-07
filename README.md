# Issue

when using yarn with this framework with a dependency on openlayers, the static and node adaptors are not resolving the os references correctly.

Created this project as a quick demonstration of the build issue. 

yarn dev : works fine (at least as far as I took it)
yarn build:
```bash
Error [ERR_MODULE_NOT_FOUND]: Cannot find module '/projects/ksgolding/playground/my-app/node_modules/ol/layer/Tile' imported from /projects/ksgolding/playground/my-app/.svelte-kit/output/server/entries/pages/index.svelte.js
Did you mean to import sgolding/playground/my-app/node_modules/ol/layer/Tile.js? # !!! MIGHT BE NOTHING, BUT NOTE sgolding/ instead of ksgolding !!!
    at finalizeResolution (internal/modules/esm/resolve.js:276:11)
    at moduleResolve (internal/modules/esm/resolve.js:699:10)
```
# Reproduce
```
yarn install
yarn build
```
Issue can be reproduced with either the node or static-adaptor.

# Environment
* node v14.17.0
* yarn 1.22.17
* Redhat Linux 8
  * NAME="Red Hat Enterprise Linux"
  * VERSION="8.5 (Ootpa)"
  * ID="rhel"
  * ID_LIKE="fedora"
  * VERSION_ID="8.5"
  * PLATFORM_ID="platform:el8"
  * PRETTY_NAME="Red Hat Enterprise Linux 8.5 (Ootpa)"
  * ANSI_COLOR="0;31"
  * CPE_NAME="cpe:/o:redhat:enterprise_linux:8::baseos"
  * HOME_URL="https://www.redhat.com/"
  * DOCUMENTATION_URL="https://access.redhat.com/documentation/red_hat_enterprise_linux/8/"
  * BUG_REPORT_URL="https://bugzilla.redhat.com/"
  * REDHAT_BUGZILLA_PRODUCT="Red Hat Enterprise Linux 8"
  * REDHAT_BUGZILLA_PRODUCT_VERSION=8.5
  * REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux"
  * REDHAT_SUPPORT_PRODUCT_VERSION="8.5"

