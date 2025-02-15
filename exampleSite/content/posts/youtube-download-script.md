+++
title = "Youtube Downloader Windows Script"
image = "/images/post/ytdlp.jpg"
author = "Sedat"
date = "2025-02-08T00:03:00Z"
description = "youtube downloader windows"
categories = ["Windows"]
type = "post"

+++
A YouTube downloader Windows batch script automates the process of downloading videos using command-line tools like yt-dlp or youtube-dl. By writing a simple .bat file, users can quickly download videos by running the script without manually entering commands. The script can include options to specify quality, format, and output directory, making it convenient for batch downloads. Additionally, integrating the script with a graphical interface or a scheduled task allows for automated video downloads, enhancing efficiency for users who frequently save YouTube content.

***

### Download 720p

```
@echo off
setlocal enabledelayedexpansion

rem Prompt the user for the YouTube URL
set /p "userURL=Enter the YouTube URL: "

rem Initialize the command variable with the yt-dlp command
set "command=yt-dlp.exe -f "bestvideo[ext=mp4][height=720]+bestaudio[ext=m4a]/best[height=720][ext=mp4]""

rem Check if the user input is empty
if "%userURL%"=="" (
    echo No URL provided. Exiting...
    exit /b
)

rem Enclose the user URL in double quotes
set "command=!command! "!userURL!""

rem Execute the command
!command!
```
***

### Download 1080p

```
@echo off
setlocal enabledelayedexpansion

rem Prompt the user for the YouTube URL
set /p "userURL=Enter the YouTube URL: "

rem Initialize the command variable with the yt-dlp command
set "command=yt-dlp.exe -f "bestvideo[ext=mp4][height=1080]+bestaudio[ext=m4a]/best[height=1080][ext=mp4]""

rem Check if the user input is empty
if "%userURL%"=="" (
    echo No URL provided. Exiting...
    exit /b
)

rem Enclose the user URL in double quotes
set "command=!command! "!userURL!""

rem Execute the command
!command!
```

***

### Download Specific Format (selection)

```
@echo off
setlocal enabledelayedexpansion

rem Prompt the user to choose between video or audio
set /p "mediaType=Do you want to download a video or audio (v/a)? "

rem Check if the user input is empty
if "%mediaType%"=="" (
    echo No selection provided. Exiting...
    exit /b
)

rem Prompt the user for the YouTube URL
set /p "userURL=Enter the YouTube URL: "

rem Check if the user input is empty
if "%userURL%"=="" (
    echo No URL provided. Exiting...
    exit /b
)

rem Use the --list-formats option to get the available formats
yt-dlp.exe --list-formats "!userURL!"

if /i "%mediaType%"=="v" (
    rem Video selected
    rem Prompt the user to enter the desired format code
    set /p "formatCode=Enter the format code (or press Enter to use bestvideo+bestaudio): "

    rem Initialize the command variable with the yt-dlp command for video
    if "!formatCode!"=="" (
        set "command=yt-dlp.exe -f "bestvideo[height<=1080]+bestaudio" --merge-output-format mp4 "!userURL!""
    ) else (
        rem Check if the format code contains a plus sign
        echo !formatCode! | findstr "+" >nul
        if !errorlevel! == 0 (
            rem Format code includes both video and audio
            set "command=yt-dlp.exe -f "!formatCode!" "!userURL!""
        ) else (
            rem Assume the user selected a video format only, merge with best audio
            set "command=yt-dlp.exe -f "!formatCode!+bestaudio" --merge-output-format mp4 "!userURL!""
        )
    )
) else if /i "%mediaType%"=="a" (
    rem Audio selected
    set "command=yt-dlp.exe -x --audio-format mp3 "!userURL!""
) else (
    echo Invalid selection. Please enter 'v' for video or 'a' for audio.
    exit /b
)

rem Execute the command
!command!
```

***

### Download Specific Format (without selection, example usage: ./script 136)

```
@echo off
setlocal enabledelayedexpansion

rem Check if a format code is provided as a command-line argument
set "formatCode=%~1"

rem Prompt the user to choose between video or audio
set /p "mediaType=Do you want to download a video or audio (v/a)? "

rem Check if the user input is empty
if "%mediaType%"=="" (
    echo No selection provided. Exiting...
    exit /b
)

rem Prompt the user for the YouTube URL
set /p "userURL=Enter the YouTube URL: "

rem Check if the user input is empty
if "%userURL%"=="" (
    echo No URL provided. Exiting...
    exit /b
)

rem Use the --list-formats option to get the available formats
yt-dlp.exe --list-formats "!userURL!"

if /i "%mediaType%"=="v" (
    rem Video selected
    rem If no format code was provided, prompt the user
    if "%formatCode%"=="" (
        set /p "formatCode=Enter the format code (or press Enter to use bestvideo+bestaudio): "
    )

    rem Initialize the command variable with the yt-dlp command for video
    if "!formatCode!"=="" (
        set "command=yt-dlp.exe -f "bestvideo[height<=1080]+bestaudio" --merge-output-format mp4 "!userURL!""
    ) else (
        rem Check if the format code contains a plus sign
        echo !formatCode! | findstr "+" >nul
        if !errorlevel! == 0 (
            rem Format code includes both video and audio
            set "command=yt-dlp.exe -f "!formatCode!" "!userURL!""
        ) else (
            rem Assume the user selected a video format only, merge with best audio
            set "command=yt-dlp.exe -f "!formatCode!+bestaudio" --merge-output-format mp4 "!userURL!""
        )
    )
) else if /i "%mediaType%"=="a" (
    rem Audio selected
    set "command=yt-dlp.exe -x --audio-format mp3 "!userURL!""
) else (
    echo Invalid selection. Please enter 'v' for video or 'a' for audio.
    exit /b
)

rem Execute the command
!command!
```

### Download Mp3 Format

```
@echo off
setlocal enabledelayedexpansion

rem Prompt the user for the YouTube URL
set /p "userURL=Enter the YouTube URL: "

rem Initialize the command variable with the yt-dlp command
set "command=yt-dlp.exe -x --audio-format mp3"

rem Check if the user input is empty
if "%userURL%"=="" (
    echo No URL provided. Exiting...
    exit /b
)

rem Enclose the user URL in double quotes
set "command=!command! "!userURL!""

rem Execute the command
!command!
```

***

##### Additional Notes

```
(download video with specific resolution)
yt-dlp.exe -f "bestvideo[ext=mp4][height=1080]" <video-url>
or
yt-dlp.exe -f "bestvideo[ext=mp4][height<=1080]" <video_url>


(To download a specific range of videos in playlist)
yt-dlp --playlist-items 1-5 <video_url>


(update)
yt-dlp.exe -U


(download audio format)
yt-dlp -x --audio-format mp3 <video-url>


(download course from auth. source using browser)
yt-dlp.exe --cookies "firefox" https://www.udemy.com/course-url


(list formats - with cookie path specified)
yt-dlp.exe --cookies "E:\Downloads\cookies.txt" --list-formats "https://www.youtube.com/watch?v=wxyzasdfghjk"
```
