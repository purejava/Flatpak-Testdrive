# Flatpak-Testdrive
![latpak-Testdrive](flatpak.png)

Flatpak hub for testing features of Flatpak apps

## How to use this?

- clone the repo using `--recurse-submodules`
- the Cryptomator app lives in `build-aux/flatpak`
- install `integrations-api`, `integrations-linux` and `flatpak-update-portal` in the versions that should be tested to the local maven repo
- copy them from there to the project directory to `build-aux/flatpak/`
- download `cryptomator-1.xx.x.tar.gz` and place the file in the project directory
- expand it locally and change the versions of `integrations-api`, `integrations-linux` and `flatpak-update-portal` in the pom to the versions that were installed before
- change the version of Cryptomator in the pom to a version that is below the current latest Cryptomator version published
- create `cryptomator-1.xx.x.tar.gz` from the expanded directory with a version that is below the current latest Cryptomator version published (so that the update mechanism can find an update). Use the same version as in the step before.
- change the version setting for Cryptomator in `org.cryptomator.Cryptomator.yaml` to the same version as in the step before
- update the maven dependencies with `update-maven-dependencies.sh`
- edit `maven-dependencies.yaml` and remove entried for `integrations-api`, `integrations-linux` and `flatpak-update-portal` as they won't get downloaded
- run `flatpak-builder build --force-clean --install-deps-from=flathub org.cryptomator.Cryptomator.yaml` a couple of times to get the sha256 checksums right and adjust them in `org.cryptomator.Cryptomator.yaml`
- install Cryptomator to Flatpak and run it, so see, that everything is fine

Now you have a version of Cryptomator, that can be pushed to `main`. After being pushed, running the `Flatter` action manually creates the Flapak Hub, that has the Cryptomator version for testing purposes. The Flapak Hub is available via https://flatter.purejava.org.

You can then push another Cryptomator version (with a different version number) to the Flapak Hub to test the update mechanism.

To clear the Flatpak Hub, delete the caches in the Flatpak-Testdrive repo under Actions > Caches.

Further hints can be found [here](https://github.com/cryptomator/cryptomator/pull/3948).

## Thank you
Thanks to [Andy Holmes](https://github.com/andyholmes) for providing [Flatter](https://github.com/andyholmes/flatter), the base for this hub.

## Copyright
Copyright (C) 2025 Ralph Plawetzki

The Flatpak-Testdrive logo is borrowed from the [Flatpak community](https://flatpak.org/).
