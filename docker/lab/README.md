# Lab image: Frigate 0.18.3 with recording decode-error recovery

Branch `lab/0.18.3-decode-recovery` = tag `v0.18.3` + the fix commit from
`fix/recording-decode-error-recovery` + this folder. Not for upstream.

The image is the official `ghcr.io/blakeblackshear/frigate:0.18.3` (pinned by digest) with
`/opt/frigate/web` replaced by the web build of this branch. The web build uses the same
commands as `docker/main/Dockerfile` (`web-build` stage).

Build on the Frigate host, from a clean `git archive` of this branch. The web build runs in
`node:20` with the same commands as the upstream `web-build` stage, capped so it cannot starve
Frigate (it peaks at about 3.6 GB):

    cd web && docker run --rm --memory=6g --memory-swap=6g --cpus=3 \
      -e NODE_OPTIONS=--max-old-space-size=4608 -v "$PWD":/work -w /work node:20 sh -c \
      'npm install && npm run build && mv dist/BASE_PATH/monacoeditorwork/* dist/assets/ && rm -rf dist/BASE_PATH'
    cd .. && docker build -f docker/lab/Dockerfile -t frigate-lab:0.18.3-decode-recovery-<fix commit> .

Built this way, the web folder differs from a rebuild of unmodified `v0.18.3` only in the
`HlsVideoPlayer` chunk.

Roll back by pointing compose at the official `0.18.3` image again.
