# Planet Worcester

This repository contains the list of feeds and the configuration required to generate the contents of [blogs.worcestersource.club](https://blogs.worcestersource.club/), kindly forked from the [OpenStreetMap Blogs aggregator](https://github.com/gravitystorm/blogs.osm.org).

## Requirements

The system is built using the [pluto](http://feedreader.github.io/) feed aggregation software. You can install the requirements using [bundler](http://bundler.io/) with:
```
bundle install
```

## Initial build

Run the following command to build the site for the first time:
```
bundle exec pluto build -t theme -o build
```

The contents of the feeds is stored in an SQLite database in the file `planet.db`, which is kept out of git. The site will be built into the `build` folder using the `template` template. These static pages can then be easily served using e.g. apache, nginx or similar.

## Subsequent updates

You can run the smaller update command, for example once per hour:
```
bundle exec pluto update
```
You need to run the `build` command each time there is an update of theme, or list of planet feeds.

## Theme

The theme is available in the theme folder, thus is available by default. You can check this by running
```
bundle exec pluto list
```

The theme was started by taking the [blank template](https://github.com/feedreader/pluto.blank), and also merging in the [feeds template](https://github.com/feedreader/pluto.feeds)

To update the CSS in the theme, update the Sass, as documented at the start of the relevant file.

## Feed Policy

The policy of what feeds are suitable for inclusion, along with guidance on how to propose changes to the feeds list, is available in [FEEDS.md](FEEDS.md).

## Deployment

The site is hosted by [Netlify](https://app.netlify.com/), and configured to automatically deploy upon every commit on the `master` branch which is pushed to GitHub.

Additionally, because of the dynamic content pulled in from multiple RSS feeds, we're using [cron-job.org](https://cron-job.org/) to trigger a built of the site once a day.
