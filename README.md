# meza-niri-dev

MezaOS niri Wayland workstation — tiling compositor, material shell, dev tools.

## Build

This distro is built by [BlueBuild](https://blue-build.org/).
Trigger a build with:

    gh workflow run build.yml --repo JhonMA82/meza-niri-dev

## Verify

    cosign verify --key cosign.pub ghcr.io/JhonMA82/meza-niri-dev:latest

---

> The upstream template README follows below.

# BlueBuild Template &nbsp; [![bluebuild build badge](https://github.com/blue-build/template/actions/workflows/build.yml/badge.svg)](https://github.com/blue-build/template/actions/workflows/build.yml)

See the [BlueBuild docs](https://blue-build.org/how-to/setup/) for quick setup instructions for setting up your own repository based on this template.

After setup, it is recommended you update this README to describe your custom image.

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/JhonMA82/meza-niri-dev:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/JhonMA82/meza-niri-dev:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## Generate an ISO

Once the image is published, generate an installable ISO with the BlueBuild CLI:

```bash
sudo bluebuild generate-iso --iso-name meza-niri-dev.iso image ghcr.io/jhonma82/meza-niri-dev
```

Or using the BlueBuild container image if you don't have the CLI installed locally:

```bash
docker run --rm -it --privileged -v "$PWD:/workspace" -w /workspace \
  ghcr.io/blue-build/cli:v0.9 \
  generate-iso --iso-name meza-niri-dev.iso image ghcr.io/jhonma82/meza-niri-dev
```

Flash the resulting `meza-niri-dev.iso` to a USB drive (e.g., with Fedora Media Writer) and boot from it.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/JhonMA82/meza-niri-dev
```
