# Images used by the organization landing page

Only `profile/README.md` renders at github.com/nodemaven, and it is the only file that
reads anything from here. Two of the assets the designer delivered are not files in this
repository at all, and they are listed below so nobody looks for them here.

Everything in this file was re-checked against the live page on **2026-08-25**, the day
the `.github` repository became public and any of it could be checked at all. Two of the
three claims the previous version made did not survive that, and they are kept below with
the correction, because the shape of the mistake is worth more than the correction.

## nodemaven-head.png

Committed, referenced, and rendering. 1600x400 on its own dark plate, 523 KB.

| | |
|---|---|
| Path | `profile/assets/nodemaven-head.png` |
| Referenced as | `./assets/nodemaven-head.png`, relative |
| Carries | the mark, the wordmark, `NEXT-GEN WEB OPERATOR` and `the only operator you need` |
| Rendered at | `width="100%"`, so about 1012 px into the README column - a 1.6x asset there |

**The relative path is correct, and the previous version of this file said it had to be
absolute.** Read off the rendered organization page on 2026-08-25, GitHub rewrites the src
to `/nodemaven/.github/raw/main/profile/assets/nodemaven-head.png` and serves it 200. It
resolves against `profile/`, not against the repository root, which is the thing that was
guessed wrong. Relative is also the better of the two once it works, because it survives a
fork and an absolute `raw.githubusercontent.com` URL does not.

How the wrong version got written is the part to keep. The file was unrenderable at the
time - the repository was private, so the org page did not exist and the raw URLs 404'd
anonymously - and an absolute URL was written down as the safe choice because it could not
be tested either way. A claim that cannot be checked is not made safe by picking the
cautious-sounding branch; it is still a guess, and it should have been labelled one.

**The theme worry was also unfounded.** The previous version said the header had to be
legible on both GitHub themes and suggested shipping two files behind `<picture>` and
`prefers-color-scheme`. This asset does not need it: the plate is opaque, so it carries its
own background onto a white page and a dark one alike. That advice stays true for any
future asset with a transparent ground, and it does not apply to this one.

The name and the slogan are pixels in this image, so `profile/README.md` does not carry
them as text. Changing the slogan means re-cutting the asset, and the `alt` attribute has
to change in the same commit - that string is what a reader with images off gets, and it
is what a search engine indexes.

## The five badge SVGs

`website-badge.svg`, `docs-badge.svg`, `telegram-badge.svg`, `x-badge.svg` and
`linkedin-badge.svg`. One style, one row, all five relative, all five verified rendering on
2026-08-25.

They are hand-cut rather than shields.io because the row directly under a hand-cut header
is the one place on the page where a generated badge would read as a different design.
Repository-status badges - a CI gate, a licence, a row count - are deliberately **not** in
this row: those belong to a repository rather than to the organization, so they sit beside
that repository further down the page, in shields.io style, which is the style a reader
expects for a build badge.

## nodemaven-mark.svg

The standalone mark, no wordmark, 133x160 viewBox, gradient `#4783F2` to `#23E6A8` on a
transparent ground. It is deliberately **not** used on this page: the header already
carries the identity, and a second logo above it is duplication.

It is here so that repositories can link one canonical copy rather than each carrying its
own. A repository README is still better off with a relative path to its own copy, because
a fork of that repository keeps working either way - and because a README that is shipped
to a package index, the way `nodemaven-python`'s is, reaches PyPI with no repository around
it at all and needs an absolute URL to a **public** host. Neither condition is met by a
relative path into this repository, so that one copy does not serve the SDK.

## Avatar

**Not a file in this repository, and not settable from this account.** The organization
avatar lives under organization Settings, and that page is owner-only. `aleekaz` is a
member. The 500x500 asset has to go to an owner.

Until it is set, the avatar is the generated identicon, and it is what renders beside every
commit, every issue comment and every pasted organization link.

## Social preview

**Not a file in this repository either.** It is set per repository under Settings, General,
Social preview, at 1280x640, and it is what renders when a repository link is pasted into
Slack, Telegram or X. An unset one falls back to the owner avatar and a wall of text.

Per repository means per repository: uploading it to one does nothing for the others, so it
is one upload for each of `.github`, `devrel-metrics`, `nodemaven-python`, the
`proxy-benchmark` repository when it exists, and every SDK added later.
