# blog.pleb.one

Source for [blog.pleb.one](https://blog.pleb.one), the PlebOne blog: posts about Nostr,
Bitcoin and freedom tech from PlebOne and Nine Point Labs. Built with
[folderblog](https://github.com/ninepointlabs/folderblog). This branch (`main`) is the
source; the built site is on `gh-pages`, served by GitHub Pages.

## Where the posts come from

Nothing is written here twice. Posts are written once, on
[blog.ninepointlabs.com](https://blog.ninepointlabs.com) (`~/Blogs/ninepointlabs-blog`),
and `bin/sync-from-ninepointlabs` copies the matching ones into `posts/ninepointlabs/`
(generated, gitignored). It runs as a `build.pre` hook in both blogs, so the folderblog
watcher publishes a matching post here as soon as it is saved there.

A post is copied when **either**

- one of its tags is `nostr`, `bitcoin`, `lightning` or `freedom-tech` (any case;
  "Freedom Tech" counts), **or**
- its front matter has `pleb: true`.

`pleb: false` keeps a post off this blog even when it has one of those tags. Drafts are
never copied. If a post stops matching (tag removed, `pleb: false`, deleted), its copy
is removed on the next build.

Each copy keeps the original front matter and Markdown, gets `canonical:` pointing at
the blog.ninepointlabs.com original (which stays the canonical URL) and has relative
links rewritten to absolute blog.ninepointlabs.com URLs. The script writes a file only
when its content changes, so it never causes a rebuild loop.

## Checking

```sh
bin/sync-from-ninepointlabs   # refresh the copies
folderblog check
folderblog preview
```
