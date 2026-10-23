# EzbaseViewer RustDesk fork

This branch contains the AGPL-3.0 RustDesk Client changes used by EzbaseViewer.
It is based on RustDesk Client `1.4.9` at commit
`6c578292e8ebbbec708b76986ba8c4bc7c509747`.

## Host profile

Build the Windows Host agent with:

```powershell
python build.py --portable --flutter --skip-portable-pack --hwcodec --ezbaseviewer-host
```

The `ezbaseviewer-host` Cargo feature forces RustDesk's existing incoming-only
policy. The Flutter home screen omits the remote target entry pane, and the
Rust connection core rejects attempts to start an outgoing connection. The
runtime application name is `EzbaseViewerHost` (service, install folder,
config folder `%APPDATA%\EzbaseViewerHost\config`); the Windows file metadata
shows the product name `EzbaseViewer Host`.

The runtime application name must not contain spaces. The Windows installer
interpolates it unquoted into `sc create/start/stop`, `reg add HKCR\.{ext}`
and the `{ext}://` URL scheme; with `EzbaseViewer Host` the install copied the
files but created no service, and still reported success.

Server pinning: `ezbaseviewer_apply_pinned_server()` (src/common.rs) sets the
Ezbase rendezvous/relay server and public key at startup.
`.github/workflows/ezbaseviewer-host.yml` builds this profile for Windows x64.

Code signing, EzbaseViewer session authorization, and removal of unused
outgoing code from the final binary remain separate release gates.

## License

The upstream RustDesk license and copyright notices remain in effect. This
fork and its modifications are distributed under AGPL-3.0. Keep the complete
corresponding source and build instructions available with every distributed
binary.
