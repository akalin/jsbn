This repository contains a reconstruction of the history of [Tom Wu's
jsbn library](http://www-cs-students.stanford.edu/~tjw/jsbn/). This is
the only file not part of the reconstruction.

I retrieved the snapshots from the [Wayback
Machine](https://web.archive.org/) using the [Wayback Machine
Downloader](https://github.com/hartator/wayback-machine-downloader).

I ran:

```bash
wayback_machine_downloader --all-timestamps --concurrency 2 --directory ./snapshots 'http://www-cs-students.stanford.edu/~tjw/jsbn*'
```

Then I combined the snapshots by day:

```bash
for date in $(ls | sed 's/^\(.\{8\}\).*/\1/' | uniq); do
  mkdir day-$date
  for d in $date*; do
    cp -r $d/~tjw/jsbn/* day-$date
    rm -rf $d
  done
done
```

I then renamed `LICENSE/index.html` to `LICENSE`.

Finally, I made a git revision for each change (sometimes spanning
multiple snapshots) and added version tags. I also had to reconstruct
the change for version 1.3, since the Wayback Machine only has
snapshots after version 1.4.

## Similar projects

https://github.com/andyperlitch/jsbn

## Using in your own project

The most convenient way is to use [RawGit](https://rawgit.com/). For
example,

```html
<script src="https://cdn.rawgit.com/akalin/jsbn/v1.4/jsbn.js"></script>
<script src="https://cdn.rawgit.com/akalin/jsbn/v1.4/jsbn2.js"></script>
```

I make no guarantees about supporting this method, although it's what
I use for my own personal projects. You can also copy the files
directly to your own web server or CDN.

## License

Use of this source code is governed by a BSD-style license that can be
found in the LICENSE file.
