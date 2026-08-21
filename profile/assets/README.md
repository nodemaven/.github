# Images used by the organization landing page

Only `profile/README.md` renders at github.com/nodemaven, and it is the only file that
reads anything from here. Two of the four assets the designer delivered are not files in
this repository at all, and they are listed below so nobody looks for them here.

## nodemaven-header.png

**Referenced by `profile/README.md` and not committed yet.** Until the file is at this
exact path on `main`, the organization page shows a broken-image icon where the header
should be. That is the one failure mode the previous version of this file was written to
avoid, so either commit the asset or put the `<img>` back inside comment markers.

| | |
|---|---|
| Path | `profile/assets/nodemaven-header.png` exactly - the tag is absolute against `raw.githubusercontent.com` and will not find a renamed file |
| Size | 1600x400, rendered at `width="100%"` into a column about 1012 px wide, so it is a 2x asset there |
| Carries | the wordmark and `Next-Gen Web Operator - the only operator you need` |
| Colour | it has to be legible on both GitHub themes. A header that is dark on white disappears in dark mode, which is the default for most of the people reading this page |

The name and the slogan are pixels in this image, so `profile/README.md` no longer
carries them as text. Changing the slogan means re-cutting the asset, and the `alt`
attribute has to change with it - that string is what a reader with images off gets, and
it is what a search engine indexes.

If the header is only legible on one background, GitHub honours `<picture>` with
`prefers-color-scheme`, so ship two files rather than compromising on one.

## nodemaven-mark.svg

The standalone mark, no wordmark, 133x160 viewBox, gradient `#4783F2` to `#23E6A8` on a
transparent ground. It is deliberately **not** used on this page: the header already
carries the identity, and a second logo above it is duplication.

It is here so that repositories can link one canonical copy rather than each carrying its
own. A repository README is better off with a relative path to its own copy, because a
fork of that repository keeps working and this organization repository may be private.

## Avatar

**Not a file in this repository, and not settable from this account.** The organization
avatar lives under organization Settings, and that page is owner-only. `aleekaz` is a
member. The 500x500 asset has to go to an owner.

Until it is set, the avatar is the generated identicon, and it is what renders beside
every commit, every issue comment and every pasted organization link.

## Social preview

**Not a file in this repository either.** It is set per repository under Settings,
General, Social preview, at 1280x640, and it is what renders when a repository link is
pasted into Slack, Telegram or X. An unset one falls back to the owner avatar and a wall
of text.

Per repository means per repository: uploading it to one does nothing for the others, so
it is one upload for each of `proxy-benchmark`, `nodemaven-python`, `.github` and every
SDK added later.
