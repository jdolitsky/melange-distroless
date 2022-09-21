# melange

<!---
Note: Do NOT edit directly, this file was generated using https://github.com/chainguard-images/readme-generator
-->

[![CI status](https://github.com/chainguard-images/melange/actions/workflows/release.yaml/badge.svg)](https://github.com/chainguard-images/melange/actions/workflows/release.yaml)

Container image for running [melange](https://github.com/chainguard-dev/melange) workflows to build APK packages.

## Get It!

The image is available on `cgr.dev`:

```
docker pull cgr.dev/chainguard/melange:latest
```

## Supported tags

| Tag | Digest | Arch |
| --- | ------ | ---- |
| `latest` `v0.1.0` | `sha256:7a992145f90583d41fe5b9f0236eac716c8ed14728f6bcdcf0c7caffa671595e`<br/>[View entry in Rekor](https://rekor.tlog.dev/?hash=sha256:7a992145f90583d41fe5b9f0236eac716c8ed14728f6bcdcf0c7caffa671595e) | `amd64` `arm64` `armv7` |


## Usage

To build the melange workflow in [examples](examples/gnu-hello.yaml):

```
docker run --privileged -v "$PWD":/work cgr.dev/chainguard/melange build /work/examples/gnu-hello.yaml
```

Output will be in the `packages` directory.

To build the melange package for the host architecture:

```
docker run --privileged -v "$PWD":/work cgr.dev/chainguard/melange build --empty-workspace --arch $(uname -m) /work/melange.yaml
```

To get a shell, you can change the entrypoint:

```
docker run --privileged -v "$PWD":/work -it --entrypoint /bin/sh cgr.dev/chainguard/melange

/ # melange version
...
```
Note that melange uses bubblewrap internally, which requires various Linux capabilities, hence the
use of `--privileged`. Because of this requirement, we recommend this image is used only for local
development and testing.


## Signing

All Chainguard Images are signed using [Sigstore](https://sigstore.dev)!

<details>
<br/>
To verify the image, download <a href="https://github.com/sigstore/cosign">cosign</a> and run:

```
COSIGN_EXPERIMENTAL=1 cosign verify cgr.dev/chainguard/melange:latest | jq
```

Output:
```
Verification for cgr.dev/chainguard/melange:latest --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - Any certificates were verified against the Fulcio roots.
[
  {
    "critical": {
      "identity": {
        "docker-reference": "ghcr.io/chainguard-images/melange"
      },
      "image": {
        "docker-manifest-digest": "sha256:7a992145f90583d41fe5b9f0236eac716c8ed14728f6bcdcf0c7caffa671595e"
      },
      "type": "cosign container image signature"
    },
    "optional": {
      "1.3.6.1.4.1.57264.1.2": "schedule",
      "1.3.6.1.4.1.57264.1.3": "23b51a1373085239002f869d68a5778e4c59172e",
      "1.3.6.1.4.1.57264.1.4": "Create Release",
      "1.3.6.1.4.1.57264.1.5": "chainguard-images/melange",
      "1.3.6.1.4.1.57264.1.6": "refs/heads/main",
      "Bundle": {
        "SignedEntryTimestamp": "MEYCIQCGvUlhWdJGJjahToDhBs7hOXpIFPRkr0x4UTMFaefnVAIhALrihAJMlPxEd6qN8vdAFgzQuLNGoFZiheIYfqx7KSBm",
        "Payload": {
          "body": "eyJhcGlWZXJzaW9uIjoiMC4wLjEiLCJraW5kIjoiaGFzaGVkcmVrb3JkIiwic3BlYyI6eyJkYXRhIjp7Imhhc2giOnsiYWxnb3JpdGhtIjoic2hhMjU2IiwidmFsdWUiOiIxNjcxODMzZDQyYWQwYjUyNGIxN2I3YmE4YjBlNDA3MzhkNzQ0MGRlMWJmYjQ0Y2UzMWM3MDJhY2U5NGViNzk4In19LCJzaWduYXR1cmUiOnsiY29udGVudCI6Ik1FWUNJUURKQlExVVJNT1FSVzBYMnR4Q2VNZkQ1bk1wU1RFdHJ2RnVFRXpsbzBJekJBSWhBTVdqTGU4SHlacXgrdUNuRnp4SmVQc2ZxbjhnMy9XZEJ2V1hSbmZCR0x5RCIsInB1YmxpY0tleSI6eyJjb250ZW50IjoiTFMwdExTMUNSVWRKVGlCRFJWSlVTVVpKUTBGVVJTMHRMUzB0Q2sxSlNVUnlSRU5EUVhwUFowRjNTVUpCWjBsVlRWTlBUazV0WkRjeVJFWTNZVXRLUzFobWNFUXdVMHRJTW14bmQwTm5XVWxMYjFwSmVtb3dSVUYzVFhjS1RucEZWazFDVFVkQk1WVkZRMmhOVFdNeWJHNWpNMUoyWTIxVmRWcEhWakpOVWpSM1NFRlpSRlpSVVVSRmVGWjZZVmRrZW1SSE9YbGFVekZ3WW01U2JBcGpiVEZzV2tkc2FHUkhWWGRJYUdOT1RXcEpkMDlVU1hoTlJFVjNUVVJSZDFkb1kwNU5ha2wzVDFSSmVFMUVSWGhOUkZGM1YycEJRVTFHYTNkRmQxbElDa3R2V2tsNmFqQkRRVkZaU1V0dldrbDZhakJFUVZGalJGRm5RVVZEY2pscVNrVnZUM2xCWVVoMFVHaFplblF3UW14UWQwaFlaVUpVV1dsNmNFcE9aRUVLZW1aclZHc3ZhWGhuWlVSU1QyTlFkMk5WTTFneGNscFpNR3QwU1dkWWVqUkxaUzlVVTBWWU1VbFVWeTlvUTA1SU1uRlBRMEZzU1hkblowcFBUVUUwUndwQk1WVmtSSGRGUWk5M1VVVkJkMGxJWjBSQlZFSm5UbFpJVTFWRlJFUkJTMEpuWjNKQ1owVkdRbEZqUkVGNlFXUkNaMDVXU0ZFMFJVWm5VVlZJZEdrNENtcHhiM00yZWxsclptcG9iRkI2UkhGYVRYUm5lV2RWZDBoM1dVUldVakJxUWtKbmQwWnZRVlV6T1ZCd2VqRlphMFZhWWpWeFRtcHdTMFpYYVhocE5Ga0tXa1E0ZDJGUldVUldVakJTUVZGSUwwSkdPSGRZV1ZwaVlVaFNNR05JVFRaTWVUbHVZVmhTYjJSWFNYVlpNamwwVERKT2IxbFhiSFZhTTFab1kyMVJkQXBoVnpGb1dqSldla3d5TVd4aVIwWjFXakpWZGt4dFpIQmtSMmd4V1drNU0ySXpTbkphYlhoMlpETk5kbU50Vm5OYVYwWjZXbE0xTlZsWE1YTlJTRXBzQ2xwdVRYWmhSMVpvV2toTmRtSlhSbkJpYWtFMVFtZHZja0puUlVWQldVOHZUVUZGUWtKRGRHOWtTRkozWTNwdmRrd3pVblpoTWxaMVRHMUdhbVJIYkhZS1ltNU5kVm95YkRCaFNGWnBaRmhPYkdOdFRuWmlibEpzWW01UmRWa3lPWFJOUWxsSFEybHpSMEZSVVVKbk56aDNRVkZKUlVOSVRtcGhSMVpyWkZkNGJBcE5SRmxIUTJselIwRlJVVUpuTnpoM1FWRk5SVXRFU1hwWmFsVjRXVlJGZWs1NlRYZFBSRlY1VFhwcmQwMUVTbTFQUkZrMVdrUlpORmxVVlROT2VtaHNDazVIVFRGUFZFVXpUVzFWZDBoQldVdExkMWxDUWtGSFJIWjZRVUpDUVZGUFVUTktiRmxZVW14SlJrcHNZa2RXYUdNeVZYZEtkMWxMUzNkWlFrSkJSMFFLZG5wQlFrSlJVVnBaTW1ob1lWYzFibVJYUm5sYVF6RndZbGRHYmxwWVRYWmlWMVp6V1ZjMWJscFVRV1JDWjI5eVFtZEZSVUZaVHk5TlFVVkhRa0U1ZVFwYVYxcDZUREpvYkZsWFVucE1NakZvWVZjMGQyZFpiMGREYVhOSFFWRlJRakZ1YTBOQ1FVbEZaa0ZTTmtGSVowRmtaMEZKV1VwTWQwdEdUQzloUlZoU0NqQlhjMjVvU25oR1duaHBjMFpxTTBSUFRrcDBOWEozYVVKcVduWmpaMEZCUVZsT1pHbzJORlZCUVVGRlFYZENTRTFGVlVOSlFuQlFRMk5uYnpOdFZsSUtjVkpLTmtJclFsRmhlWGxtUm01MFRYaE1NbFJhWkRGRFpuWllaME5EUjFOQmFVVkJaMUpQTW1VeVVYTmhZVzlPWW5kT2JDdDRiQzlrY1RGWE1sZHhhQXBOWTBscmRGcFlPSGRsVVdoVWFrRjNRMmRaU1V0dldrbDZhakJGUVhkTlJGcDNRWGRhUVVsM1lrRlFTVU5vUVV4NldrbHVUMjFIU1dWWFdXNTFjQzltQ2paS2VqZGtUVmw1ZFVaeFFqVlpjM2hYZWtKR1ZFSkhZVWN2VGsxVEt6ZERObkJ4U1ZKUmFuSkJha0ZwVDBaRmFESXlXa0oyZDFKamVXRkhhREZUYTB3S0x6bFpVa0Y2Vm13cldFdGhUbVZqTjFaTmNXZEJTVWhoYUZKSFYzZFRaVzAyTTBaWE0zcFdjSFJOVlQwS0xTMHRMUzFGVGtRZ1EwVlNWRWxHU1VOQlZFVXRMUzB0TFFvPSJ9fX19",
          "integratedTime": 1663722050,
          "logIndex": 3641768,
          "logID": "c0d23d6ad406973f9559f3ba2d1ca01f84147d8ffc5b8445c224f98b9591801d"
        }
      },
      "Issuer": "https://token.actions.githubusercontent.com",
      "Subject": "https://github.com/chainguard-images/melange/.github/workflows/release.yaml@refs/heads/main",
      "run_attempt": "1",
      "run_id": "3094421856",
      "sha": "23b51a1373085239002f869d68a5778e4c59172e"
    }
  }
]
```

You can verify that the image was built in Github Actions in this repository from the `Issuer` and `Subject` fields.
</details>

## Build

This image is built with [melange](https://github.com/chainguard-dev/melange) and [apko](https://github.com/chainguard-dev/apko).

