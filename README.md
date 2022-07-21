# BloomFlatpak
flatpak configuration files for BloomDesktop

This directory holds flatpak packaging specification files and tools.

## Building

### Dependencies

Flathub repo, FW flatpak manifest, tools:

```bash
sudo add-apt-repository ppa:flatpak/stable
sudo apt install flatpak-builder flatpak
flatpak --user remote-add --if-not-exists flathub \
  https://flathub.org/repo/flathub.flatpakrepo
flatpak --user install flathub org.gnome.Sdk//41
flatpak --user install flathub org.gnome.Platform//41
flatpak --user install flathub org.freedesktop.Sdk.Extension.mono6//21.08
flatpak --user install flathub org.freedesktop.Sdk.Extension.node16//21.08
flatpak update
```

#### Optional dependencies

Install xonsh to run some dependency-url-generating scripts.
```bash
sudo apt install xonsh
```

### Build

Build and install the flatpak package:

```bash
./build
```

Note that your first build will take time to download and build all
dependencies. Subsequent builds benefit from caching.

## Testing

Run Bloom in the flatpak package:

```bash
flatpak run org.sil.Bloom
```

Open a shell inside the Bloom flatpak instead of running Bloom:

```bash
./shell
```

## Validate appdata [what is this -- check with Mark]

```bash
flatpak install flathub org.freedesktop.appstream-glib
flatpak run org.freedesktop.appstream-glib validate \
  ../DistFiles/Linux/org.sil.Bloom.metainfo.xml
```

## Clean up

You can safely delete the following directories, although it will make the next
package-build take longer:

```
node_modules
local-repo
.flatpak-builder
build-dir
~/.cache/flatpak-build-logs
```

## Search github for flatpak build using msbuild (or any other item by changing "msbuild")
```
https://github.com/search?q=org%3Aflathub+msbuild&type=code
```
