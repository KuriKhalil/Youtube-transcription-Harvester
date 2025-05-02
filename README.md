# 📘 YouTube Transcript Harvester

Extract transcripts at scale. Bypass limits. Supercharge your NotebookLM.

> This Python tool automates the extraction of transcripts from YouTube videos — whether it's a single video, a playlist, or an entire channel — using Selenium. It helps bypass NotebookLM’s frustrating 50-source limit, which normally requires adding video links one by one. With this script, you can instantly retrieve transcripts from dozens or even hundreds of videos. Just merge the generated .txt files to build a rich, searchable corpus that can be fed into NotebookLM — all without needing to pay the \$20/month subscription

## Features

* Automatically extracts transcripts from a variety of YouTube URLs:

  * Single video links
  * Playlists (extracts all videos in the playlist)
  * Entire channels (extracts all public videos)
* Accepts a mixed list of video, playlist, and channel URLs
* Saves transcripts as plain text files, organized into relevant folders
* Supports headless browser mode for full automation

## Prerequisites

* Python 3.7+
* Google Chrome browser installed
* Compatible ChromeDriver in project root (named `chromedriver.exe` or appropriate for your OS)

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/KuriKhalil/Youtube-transcription.git
   ```

2. Install Python dependencie:

   ```bash
   pip install selenium
   ```

3. Ensure [chromedriver](https://getwebdriver.com/chromedriver) matches your Chrome version. Place it in the project root or update the path in `youtube_transcript.py`.


## Usage

The script reads a list of YouTube URLs from `Youtube_links.txt`, then extracts and saves each transcript as a `.txt` file inside the `Transcript/` directory.

### Step-by-step:

1. Open the `Youtube_links.txt` file in any text editor.

2. Paste one URL per line. You can mix individual videos, playlists, and channel links. Example:

   ```text
   https://www.youtube.com/watch?v=VIDEO_ID,
   https://www.youtube.com/playlist?list=PLAYLIST_ID,
   https://www.youtube.com/@ChannelName/videos,
   ```

3. Save the file.

4. Run the script:

   ```bash
   python youtube_transcript.py
   ```

5. The script will:

   * Detect the type of each URL (video, playlist, channel)
   * Open the link in a headless Chrome browser
   * Extract the transcript (if available)
   * Save it under `Transcript/` with a logical folder structure

### Output Structure Example:

```plaintext
Transcript/
├── SingleVideo.txt
├── MyPlaylist/
│   ├── video1.txt
│   └── video2.txt
└── MyChannel/
    ├── video1.txt
    └── video2.txt
```

You can then merge these `.txt` files to create a larger corpus with :

```
copy /b *.txt merged.txt
```

## Configuration

* **Headless Mode**: Currently set via `options.add_argument("--headless=new")`. Remove this line to see the browser.
* **Max Threads**: To modify how many videos are processed simultaneously, change the `max_workers` parameter in the `ThreadPoolExecutor` inside the `main()` function of `youtube_transcript.py`.

## File Structure

```plaintext
.
├── chromedriver.exe          # ChromeDriver executable
├── requirements.txt          # Python dependencies
├── Youtube_links.txt         # Input file with URLs
├── youtube_transcript.py     # Main harvesting script
└── Transcript/               # Output transcripts
    ├── video_title1.txt
    ├── playlist_name/
    │   ├── video1.txt
    │   └── video2.txt
    └── channel_name/
        ├── video1.txt
        └── video2.txt
```

## License

MIT License. See [LICENSE](LICENSE) for details.
