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
application name and Windows file metadata identify the build as
`EzbaseViewer Host`.

This is the first HostOnly PoC boundary. Installation, code signing, server
pinning, EzbaseViewer session authorization, and removal of unused outgoing
code from the final binary remain separate release gates.

## License

The upstream RustDesk license and copyright notices remain in effect. This
fork and its modifications are distributed under AGPL-3.0. Keep the complete
corresponding source and build instructions available with every distributed
binary.
