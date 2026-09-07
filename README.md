# Signet Drive — public hash history

Append-only. Each entry records a build manifest exactly as production served it, plus the
manifest's SHA-256. The verification tooling in [signet-drive/verify](https://github.com/prsnex/signet-drive/tree/main/verify)
anchors a manifest here before rebuilding: a manifest whose hash is not in this history is
treated as unanchored and is not verified.

- `releases/<source_tag>/` — CLI build manifests (`*.manifest.json`) and their `.sha256`.
- `web/<build_commit_sha>/` — the web bundle manifest served at `/.well-known/signet-bundle-manifest.json` and its `.sha256`.
  The `.canonical.sha256` beside it is the SHA-256 of the manifest's RFC 8785 canonical form (compact, sorted keys), which is the hash `verify-web-bundle.sh` anchors; the plain `.sha256` is the served bytes.
- `HASHES.md` — the index, one line per entry, newest last.

Entries are appended per production deploy. History is never rewritten.
