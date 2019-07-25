# OBS Source Service `obs-service-go_modules`

An [OBS](https://build.opensuse.org)
[Source Service](https://openbuildservice.org/help/manuals/obs-user-guide/cha.obs.source_service.html)
to download, verify and vendor Go module dependency sources.

Using go.mod and go.sum present in a Go application, call
go tools in sequence:

```
go mod download
go mod verify
go mod vendor
```

`obs-service-go_modules` will create `vendor.tar.gz` containing the
`vendor/` directory populated by `go mod vendor`. `vendor.tar.gz`
is generated in the rpm package directory.

## Usage for packagers

Presently it is assumed the Go application is distributed as
a tarball `app-0.1.0.tar.gz` unpacking to `app-0.1.0/`

Create a `_services` file containing:

```
<services>
  <service name="go_modules" mode="disabled">
    <param name="archive">app-0.1.0.tar.gz</param>
  </service>
</services>
```

Run osc command locally:

```
osc service disabledrun
```

## Transition note

Until such time as `obs-service-go_modules` is available on
[OBS](https://build.opensuse.org), `vendor.tar.gz` should
be committed along with the Go application release tarball.

## License

GNU General Public License v2.0 or later
