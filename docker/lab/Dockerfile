# Official Frigate 0.18.3 image with only the web UI replaced by this branch's build.
# Everything else (Python, ffmpeg, go2rtc, nginx, models) stays byte-for-byte the official image.
#
# Build: see README.md next to this file.
FROM ghcr.io/blakeblackshear/frigate:0.18.3@sha256:d1a3e0008557bb3f3314d442ecd4ba68e9b16ab7872d64612649f7a6e5156635

RUN rm -rf /opt/frigate/web
COPY web/dist/ /opt/frigate/web/
