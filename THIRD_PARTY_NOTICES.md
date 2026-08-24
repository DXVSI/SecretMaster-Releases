# Third-party notices

SecretMaster application source remains proprietary. The binary dynamically
links to the third-party components below. Their licenses apply only to those
components and do not change the license of the proprietary application code.

This inventory is the direct-dependency baseline for the first beta. Before a
release is published, the packaged DLL and shared-library inventory must be
compared with this file. Any additional library or Qt plugin dependency must add
its copyright notice, license text and corresponding-source information. This is
a manual release gate, not a claim that a currently unbuilt artifact has already
been audited. It is not legal advice.

## Qt 6.11.2

SecretMaster uses the Qt Core, Gui, Widgets and Sql modules, the SQLite driver,
and platform plugins deployed for Linux or Windows. Qt libraries and plugins are
dynamically linked and are used under the GNU Lesser General Public License
version 3. The complete license terms are included as:

- `licenses/LGPL-3.0-only.txt`
- `licenses/GPL-3.0-only.txt`, incorporated by the LGPL

Copyright notices for individual Qt modules and bundled third-party code are in
the corresponding Qt source tree.

Exact corresponding source:

- <https://download.qt.io/official_releases/qt/6.11/6.11.2/single/qt-everywhere-src-6.11.2.tar.xz>
- SHA-256: `6dcfbca271d76a6502741a2c0dc6fc98ef7dd0b7b4cfd0abcebb285a86a26f33`
- Qt licensing overview: <https://doc.qt.io/qt-6/licensing.html>

The binary license does not restrict reverse engineering for debugging changes
to LGPL-covered Qt libraries. On Windows, compatible replacement Qt DLLs and
plugins can be placed beside `SecretMaster.exe`. On Linux, an AppImage can be
extracted and inspected without root:

```fish
chmod +x SecretMaster-x86_64.AppImage
./SecretMaster-x86_64.AppImage --appimage-extract
./squashfs-root/AppRun
```

Compatible Qt shared libraries under the extracted `squashfs-root` may be
replaced for debugging or modification. Repacking is optional; the extracted
AppDir is directly executable.

## libsodium 1.0.22

SecretMaster dynamically links to libsodium for authenticated encryption,
password derivation, random generation and constant-time comparisons.
Libsodium is distributed under the ISC license. Its complete notice is included
as `licenses/ISC-libsodium.txt`.

- Source release: <https://github.com/jedisct1/libsodium/releases/tag/1.0.22-RELEASE>
- Source archive: <https://github.com/jedisct1/libsodium/releases/download/1.0.22-RELEASE/libsodium-1.0.22.tar.bz2>
- Source SHA-256: `51b93737bf62e8549b0e94dce0fba92169e31c8ecc160883460a9bdaa6d2c298`
- Windows MSVC archive SHA-256: `3e03a726fac4bc09cb61d8f29d658ef7a5eca0811de59082130414f7ca2e4279`

## Microsoft Visual C++ runtime

The Windows ZIP may contain Microsoft Visual C++ runtime files copied by
`windeployqt --compiler-runtime`. Those files are Microsoft redistributables and
remain governed by the Microsoft Visual Studio licensing terms. They are not
covered by the SecretMaster Binary License.

## External tools not bundled

`gh`, `ssh-keygen` and the Linux `secret-tool` executable are invoked only when
installed separately by the user. They are not copied into the release packages
by the release scripts and are therefore not redistributed as part of
SecretMaster.
