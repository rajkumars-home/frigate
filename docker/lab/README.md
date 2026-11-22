# Lab image: Frigate 0.18.3 with recording decode-error recovery

Branch `lab/0.18.3-decode-recovery` = tag `v0.18.3` + the fix commit from
`fix/recording-decode-error-recovery` + this folder. Not for upstream.

The image is the official `ghcr.io/blakeblackshear/frigate:0.18.3` (pinned by digest) with
`/opt/frigate/web` replaced by the web build of this branch. The web build uses the same
commands as `docker/main/Dockerfile` (`web-build` stage).

Build on the Frigate host, from a clean checkout of this branch with `web/dist` built:

    docker build -f docker/lab/Dockerfile -t frigate-lab:0.18.3-decode-recovery-<short commit> .

Roll back by pointing compose at the official `0.18.3` image again.
