# get-artist-title

Get the artist and title from a full song name, eg. a YouTube video title.

## Installation

```bash
npm install --save get-artist-title
```

## Usage

```js
const getArtistTitle = require('get-artist-title')
getArtistTitle('Taylor Swift - Out Of The Woods')
//→ ['Taylor Swift', 'Out Of The Woods']

let [ artist, title ] = getArtistTitle('FEMM - PoW! (Music Video)')
//→ ['FEMM', 'PoW!']
```

## API

### getArtistTitle(string, plugins=['base'])

Extract the artist and title from `string`. Returns `null` if no artist/title
can be found.

The second parameter is an array of plugins. These can be strings for [plugins
that come with `get-artist-title`](./lib/plugins), or plugin objects. You
shouldn't touch this unless you're noticing that you get really bad results :)

## Plugins

> **Note** Since `get-artist-title` is still new, the included/default set of
> plugins might change.

A specific use case can require different methods of detecting song names. If
you're mostly going to be dealing with Western music, the default behaviour
works pretty well. However if you're also going to be dealing with a lot of
k-pop song titles from YouTube, for example, things might get interesting…

 * [에프엑스_첫 사랑니(Rum Pum Pum Pum)_Music Video](https://www.youtube.com/watch?v=xnku4o3tRB4)
 * [[MV] Lim Kim(김예림) (Togeworl(투개월)) _ Awoo](https://www.youtube.com/watch?v=CXPADwU05OQ)

…and a custom parser might be useful.

By default getArtistTitle extracts the artist and title of a song similarly to
how the YouTube connector in the [Last.fm scrobbler for Chrome](https://github.com/david-sabata/web-scrobbler)
works.

A Plugin is a plain JavaScript object defining any of the below functions:

### plugin.splitArtistTitle(string)

Split the artist and title parts from a string. Return `[artist, title]` if
successful, or `null` if unsuccessful.

When using multiple plugins, their splitArtistTitle methods are run in order on
the original string. The first match is used.

### plugin.mapArtistTitle(array)

Do arbitrary things with the artist and title. `array` is a two-item array,
like the ones returned from `splitArtistTitle()`: `[artist, title]`.

Return the new `[artist, title]` pair when you're done.

This method could be used to swap the artist and title for an input like this,
where the song title precedes the artist name:
[WORLD OF FANTASY (MUSIC VIDEO) / capsule](https://www.youtube.com/watch?v=W4h8m74pyC8)
It's up to you to decide which cases need to be swapped, though :smile:

### plugin.cleanArtist(artist), plugin.cleanTitle(title)

Cleanup an artist or title part. Return the new artist or title part when you're
done.

## Licence

[MIT](./LICENSE)
