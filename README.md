# heroku-buildpack-yt-dlp

A [Heroku buildpack](https://devcenter.heroku.com/articles/buildpacks) that installs the latest stable release of [yt-dlp](https://github.com/yt-dlp/yt-dlp).

## Do I need this?

You'll only need this buildpack if, for some reason, you can't add [Heroku's official Python buildpack](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-python) to your app. Otherwise, you can follow yt-dlp's [pip installation instructions](https://github.com/yt-dlp/yt-dlp/wiki/Installation#with-pip) and specify the `yt-dlp` package as a dependency using `requirements.txt`:

```txt
yt-dlp[default]
```

And add the buildpack to your app:

```sh
heroku buildpacks:add -i 1 heroku/python
```

This will work even if you're using a different buildpack, like `heroku/ruby`. The Python buildpack will install the dependencies listed in `requirements.txt` and add the installed binaries to your app's `$PATH`.

> [!IMPORTANT]
> If you need ffmpeg alongside yt-dlp, see "Usage", below, to install it by adding the first-party `heroku-buildpack-activestorage-preview` buildpack.

## Usage

Because yt-dlp depends on [ffmpeg](https://www.ffmpeg.org/), you'll need to add both this buildpack and Heroku's first-party [heroku-buildpack-activestorage-preview](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-activestorage-preview), which installs ffmpeg. You can use the Heroku CLI's `buildpacks:add` command to do so:

```sh
heroku buildpacks:add -i 1 https://github.com/heroku/heroku-buildpack-activestorage-preview
heroku buildpacks:add -i 2 https://github.com/blolol/heroku-buildpack-yt-dlp
```

See Heroku's ["Managing Buildpacks"](https://devcenter.heroku.com/articles/managing-buildpacks) documentation for more details.

The next time you deploy your app, yt-dlp will be downloaded and added to your app's `$PATH`. The installed version and the path to the binary are shown during slug compilation.
