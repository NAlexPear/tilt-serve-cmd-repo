# `cmd` vs `serve_cmd` working directory behavior

There are two Tiltfiles in this repo: `./Tiltfile` and `./example/Tiltfile`. The latter is `include`-ed into the former, and contains two `local_resource` commands: one that invokes `npm install` as a `cmd`, and another that invokes `npm run watch` (which starts up a local dev server) as a `serve_cmd`.

## Expected Behavior:

Both commands in `./example/Tiltfile` should succeed on `tilt up`, whether `tilt up` is called from '.' or from './example'.

## Actual Behavior:

The `cmd`-based `npm install` `local_resource` always succeeds, while the `serve_cmd`-based `npm run watch` only works when the working directory is `./example`. Looking at the errors, you'll see that `serve_cmd` is invoked from the location of `tilt up`, while `cmd` is invoked from the location of the `include`-ed `Tiltfile` (`./example` in this case).
