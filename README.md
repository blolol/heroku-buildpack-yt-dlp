# heroku-buildpack-yt-dlp

A [Heroku buildpack](https://devcenter.heroku.com/articles/buildpacks) that installs the latest stable release of [yt-dlp](https://github.com/yt-dlp/yt-dlp).

## Usage

Because yt-dlp depends on [ffmpeg](https://www.ffmpeg.org/), you'll need to add both this buildpack and Heroku's first-party [heroku-buildpack-activestorage-preview](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-activestorage-preview), which installs ffmpeg. You can use the Heroku CLI's `buildpacks:add` command to do so:

```sh
heroku buildpacks:add https://github.com/heroku/heroku-buildpack-activestorage-preview
heroku buildpacks:add https://github.com/blolol/heroku-buildpack-yt-dlp
```

See Heroku's ["Managing Buildpacks"](https://devcenter.heroku.com/articles/managing-buildpacks) documentation for more details.

The next time you deploy your app, yt-dlp will be downloaded and added to your app's `$PATH`. The installed version and the path to the binary are shown during slug compilation.
