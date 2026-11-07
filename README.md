<!-- SPDX-License-Identifier: GPL-2.0-only -->

This platform builds Xiaomi SM8450 and SM8475 with kernel 6.6. Zeus is the
first runtime validation target. Cupid and Cape outputs are also built;
their runtime behavior remains unverified. Provenance, supported SoC
revisions and hardware results are in the devicetree repository's
`Documentation` directory.

On an existing LineageOS Xiaomi SM8450 checkout, use `zeus-manifest.xml` as
`.repo/local_manifests/xiaomi_sm8450_6.6.xml`, replacing the older kernel-only
manifest. It selects the published kernel, device and display-HAL branches.
The display fork supplies the Waipio SnapAlloc initialization needed by
the current graphics userspace. Retain the existing Xiaomi vendor and
MIUI-camera projects; the latter uses `cupid-development`'s `lineage-24.0`
branch. Do not declare the same project paths in another local manifest.

Configure and build from the Android checkout root:

```sh
source build/envsetup.sh
breakfast zeus
m bacon
```

In the maintainer's checkout, `source ./g.sh` followed by `build zeus` uses
the existing ccache setup. Configuring with `breakfast` alone does not build
images. Keep the audio `target_product` flag in `BoardConfigCommon.mk`;
it selects the board's machine-driver configuration.
