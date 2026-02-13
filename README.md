# Lab: Youtube Download

<img src=img/discover.jpg width=300px align=right />

One of the benefits of python is that it is easy to download and run programs (called scripts) that other people have written.
In your next project you will write one of these scripts.
The purpose of this lab is to give you practice using other people's scripts.
As an example, we will use a script for downloading videos from youtube.

## Download the Repo

There are many github repos that have code for downloading video from youtube.
Here are two examples:

1. <https://github.com/ytdl-org/youtube-dl>
1. <https://github.com/yt-dlp/yt-dlp>

Your first task is to figure out which one of these repos contains "working code".

*Problem:*
You're all obviously not yet qualified to actually read the code and understand what it does.
So how do you figure out which project has good code?

*Solution:*
Github Actions.

<img src=img/build-passing.png />

Click each of the links above and look for a test case badge.
One of the repos has failing test cases, and one has passing test cases.

Download the repo with passing test cases using the command
```
$ git clone <url>
$ cd <repo_dir>
```

## Running the Code

Recall that you can always use the program `ls` to list the files in the current directory.
If you've successfully downloaded the right url,
you should see output that looks like
```
$ ls
bundle           LICENSE         README.md                 yt-dlp.cmd
Changelog.md     Maintainers.md  supportedsites.md         yt-dlp.sh
CONTRIBUTING.md  Makefile        test
CONTRIBUTORS     public.key      THIRD_PARTY_LICENSES.txt
devscripts       pyproject.toml  yt_dlp
```
> **NOTE:**
> Everyone's output of `ls` will look a little bit different.
> Some people will have different colors, some people a different number of columns, and some people a different sorting order.
> Everyone should have the same files listed though.

This is a big project that has had 1000s of people contribute to it from around the world.

> **NOTE**:
> You can find the fill list using [the github insights tab](https://github.com/yt-dlp/yt-dlp/graphs/contributors).
> Later in this course, we will see how to contribute to other people's repos like this.
> Employers *love* to hire students who contribute to open source,
> and one of the big purposes of this class is to help contribute to your "github profile" so that employers will *love* to hire you!

How do we know where to start looking at such a big project?

In python, it is customary for the most important file in a repo to be called `__main__.py` and to be located in a *subfolder*.
The subfolder will be different for every project, but in this case it is `yt_dlp`.
You can run the program in the terminal with the command
```
$ python3 yt_dlp/__main__.py

Usage: yt-dlp [OPTIONS] URL [URL...]

yt-dlp: error: You must provide at least one URL.
Type yt-dlp --help to see a list of all options.
```

Notice that:
1. I am providing the *relative path* to the `__main__.py` file in the command above.
    A relative path is the name of a file along with whatever subdirectories it is contained inside of.

    If you do not put a relative path and only put `__main__.py`,
    you will get an error like
    ```
    $ python3 __main__.py
    python3: can't open file '__main__.py': [Errno 2] No such file or directory
    ```
2. Even when we called the program correctly, the program still gives us an error message.
    Python scripts do not normally use *graphical user interfaces* (GUIs) like most programs you are used to.
    Instead, they use *command line interfaces* (CLIs).

In order to download a youtube video, we need to provide a url to the script so it knows what video to download.
simply paste the URL at the end of the command.
As our working example, we will use one of the most famous videos of all time: <https://www.youtube.com/watch?v=dQw4w9WgXcQ>.

Run the download with the command
```
$ python3 yt_dlp/__main__.py 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
```
> **IMPORTANT:**
> Depending on your computer's configuration, you may get some error messages with the above command.
> If you get an error about a failed SSL certificate, then add the `--no-check-certificate` option to the command above to get
> ```
> $ python3 yt_dlp/__main__.py --no-check-certificate 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
> ```
> SSL stands for the *secure socket layer* and is responsible for encrypting web traffic.
> Youtube and all other major websites use SSL.
> This error means that something about your python configuration is insecure and the encryption can't be trusted.
> That would be a problem if we were accessing an important website like your bank,
> but for downloading a video,
> it's not really a big deal.

> **Aside:**
> Is using `yt_dlp` legal?
> Yes.
>
> Why would a tool for pirating be legal?
> It has many legitimate uses besides pirating.
> For example:
> 1. The [Aleph with Beth youtube channel]() develops videos for teaching Hebrew.
>   They have [explicit instructions about how to use `yt-dlp` to download their videos in order to watch them in locations without internet access](https://freehebrew.online/offline/).
> 1. The KCNA watch website provides an archive of all material published by the DPRK (i.e. North Korea).
>   They use `yt-dlp` to archive videos,
>   and you can find the [archived repository here](https://kcnawatch.org/kctv-archive/).
>   Foreign policy analysts can rely on the fact that videos in this archive will not be modified/deleted due to changes in the political climate.
>   `yt-dlp` also has the nice advantage that it can download from *any* video website, not just youtube.
>   So these archivists can archive *any* videos that the DPRK puts online.
>
>   <img src=img/dlp.png width=400px />
>
> Previously, the standard package for downloading content from youtube was called `youtube-dl`,
> but a legal battle with the RIAA caused the project to "fork" to the new `yt-dlp` project.
> The primary complaint that the RIAA had against `youtube-dl` was that they used several examples in their documentation that could be construed as encouraging piracy;
> the `yt-dlp` documentation does not contain these examples and so is not subject to the same litigation,
> although it can certainly still be used for piracy.
> In general in the US, developing or possessing software is never illegal,
> and you cannot be prosecuted for developing or possessing particular software.
> You will be prosecuted for any illegal activity that you use the software for.
> The distinction is subtle but important.
>
> You can find details on the history of `youtube-dl`/`yt-dlp` and the legalities at Hacker News: <https://news.ycombinator.com/item?id=24872911>.
> This is a famous social media website for news and discussions about programming.

Scripts generally provide detailed help that tells you how to use the command if you pass the `--help` flag.
If you run
```
$ python3 yt_dlp/__main__.py --help
```
you can see that `yt-dlp` has many options for things like setting the audio/video quality of the download, downloading entire playlists, and using web proxies for the download.

## Submission

Upload your downloaded video to canvas.
