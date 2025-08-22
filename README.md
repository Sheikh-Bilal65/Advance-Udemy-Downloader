# Udemy Downloader with DRM support

Unlock your Udemy courses for offline access with this powerful Python script! Seamlessly download lectures, including DRM-protected content, by easily extracting cookies and Widevine keys. This tool is designed for educational purposes, demonstrating automation techniques for personal use. Get started quickly and enjoy your learning journey, anytime, anywhere.

This Python script empowers you to download Udemy courses for offline access, including those with DRM protection. By guiding you through the process of extracting necessary cookies and Widevine decryption keys, it enables seamless access to your purchased content. Perfect for learners who want to study on the go, without an internet connection.

**Empower Your Automation Journey!**

If this tool has helped you, consider supporting its continued development. Your contribution, no matter how small, fuels the creation of more free, powerful, and feature-rich tools like this one. Let's build amazing things together!

<a href="https://buymeacoffee.com/bilalsheikh" target="_blank"> <img src="https://img.shields.io/badge/Buy%20Me%20A%20Coffee-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black" alt="Buy Me A Coffee"> </a>

### 💸 Crypto Donation

If you’d like to support this project, you can donate via cryptocurrency!

#### **Option 1: Binance ID (Direct Transfer for Binance Users)**
- **Binance ID:** `150697028`
  - *(This allows instant transfers between Binance accounts. Just use my ID in the “Send via Binance ID” section!)*

#### **Option 2: Direct Wallet Address (BNB Smart Chain BEP20)**

**BNB (Binance Coin, BEP20):**  
- **Network:** BNB Smart Chain (BEP20)  
- **Wallet Address:**  
  `0xef6e84f601441439e809088fe0355ec63b9f0017`

![BNB Wallet QR code](BNB.jpg)

---

**USDT (Tether USD, BEP20):**  
- **Network:** BNB Smart Chain (BEP20)  
- **Wallet Address:**  
  `0xef6e84f601441439e809088fe0355ec63b9f0017`

![USDT Wallet QR code](USDT.jpg)

---

> **Note:**  
> Do not send NFTs to this address.  
> For other cryptocurrencies, or if you’d like an ERC20 or TRC20 address, reach out via email or GitHub!


---

Utility script to download Udemy courses, has support for DRM videos but requires the user to acquire the decryption key (for legal reasons).<br>
Windows is the primary development OS, but I've made an effort to support Linux also (Mac untested).

> [!IMPORTANT]  
> This tool will not work on encrypted courses without decryption keys being provided!
>
> Downloading courses is against Udemy's Terms of Service, I am NOT held responsible for your account getting suspended as a result from the use of this program!
>
> This program is WIP, the code is provided as-is and I am not held resposible for any legal issues resulting from the use of this program.

### Requirements

The following third-party tools are required to run the script. They are **not included in this repository** and must be downloaded and installed manually, ensuring they are accessible in your system's PATH.

-   [Python 3](https://python.org/)
-   [ffmpeg](https://www.ffmpeg.org/) - This tool is also available in Linux package repositories.
    -   NOTE: It is recommended to use a custom build from the yt-dlp team that contains various patches for issues when used alongside yt-dlp, however it is not required. Latest builds can be found [here](https://github.com/yt-dlp/FFmpeg-Builds/releases/tag/latest)
-   [aria2/aria2c](https://github.com/aria2/aria2/) - This tool is also available in Linux package repositories
-   [shaka-packager](https://github.com/shaka-project/shaka-packager/releases/latest)
-   [yt-dlp](https://github.com/yt-dlp/yt-dlp/) - This tool is also available in Linux package repositories, but can also be installed using pip if desired (`pip install yt-dlp`)

### Quick Start

To download DRM-protected courses, you'll need to extract cookies and Widevine decryption keys. Follow these steps:

1)  **Extract Cookies (for Udemy Login)**:
    *   Install a "Cookies Editor" extension for your browser. Mozilla Firefox is recommended for better compatibility with Widevine L3 Decrypter.
        *   **Google Chrome**: [Cookies Editor](https://cookie-editor.com/)
        *   **Mozilla Firefox**: [Cookies Editor](https://cookie-editor.com/)
    *   Log in to your Udemy account in your browser.
    *   Open the installed "Cookies Editor" extension.
    *   Copy the cookies in "Netscape" format.
    *   Paste the copied content into the `cookie.txt` file located in the project directory.

2)  **Extract Widevine DRM Keys (for Encrypted Videos)**:
    *   **Important**: As of now, the "Widevine L3 Decrypter" extension is not fully supported on Google Chrome for key extraction. It is highly recommended to use **Mozilla Firefox** for this step.
    *   Install the "Widevine L3 Decrypter" extension on Mozilla Firefox:
        *   **Mozilla Firefox**: [Widevine L3 Decrypter](https://addons.mozilla.org/en-US/firefox/addon/widevine-l3-decrypter/)
    *   If you copied cookies from Google Chrome in the previous step, ensure you are logged into your Udemy account on Mozilla Firefox.
    *   Navigate to the Udemy course you wish to download and start playing any video lecture.
    *   While the video is playing, open the "Widevine L3 Decrypter" extension.
    *   With default settings, click the "Guess" button. Wait for the extension to process and display the decryption keys.
    *   Copy the "Key" and "Key ID" provided by the extension.
    *   Paste these keys into the `keyfile.json` file in the project directory. This will allow the script to decrypt the encrypted files downloaded from Udemy and bypass DRM protection.

3)  **Install dependencies** (Python 3.9+ recommended):
    ```bash
    pip install -r requirements.txt
    ```

2)  **Run the automation script**:
    Use the `main.py` script with command-line arguments to specify the target URL and desired actions.

    **Example Usage:**
    -   Passing a Bearer Token and Course ID as an argument
    -   `python main.py -c <Course URL> -b <Bearer Token>`
    -   `python main.py -c https://www.udemy.com/courses/myawesomecourse -b <Bearer Token>`
-   Download a specific quality
    -   `python main.py -c <Course URL> -q 720`
-   Download assets along with lectures
    -   `python main.py -c <Course URL> --download-assets`
-   Download assets and specify a quality
    -   `python main.py -c <Course URL> -q 360 --download-assets`
-   Download captions (Defaults to English)
    -   `python main.py -c <Course URL> --download-captions`
-   Download captions with specific language
    -   `python main.py -c <Course URL> --download-captions -l en` - English subtitles
    -   `python main.py -c <Course URL> --download-captions -l es` - Spanish subtitles
    -   `python main.py -c <Course URL> --download-captions -l it` - Italian subtitles
    -   `python main.py -c <Course URL> --download-captions -l pl` - Polish Subtitles
    -   `python main.py -c <Course URL> --download-captions -l all` - Downloads all subtitles
    -   etc
-   Skip downloading lecture videos
    -   `python main.py -c <Course URL> --skip-lectures --download-captions` - Downloads only captions
    -   `python main.py -c <Course URL> --skip-lectures --download-assets` - Downloads only assets
-   Keep .VTT caption files:
    -   `python main.py -c <Course URL> --download-captions --keep-vtt`
-   Skip parsing HLS Streams (HLS streams usually contain 1080p quality for Non-DRM lectures):
    -   `python main.py -c <Course URL> --skip-hls`
-   Print course information only:
    -   `python main.py -c <Course URL> --info`
-   Specify max number of concurrent downloads:
    -   `python main.py -c <Course URL> --concurrent-downloads 20`
    -   `python main.py -c <Course URL> -cd 20`
-   Cache course information:
    -   `python main.py -c <Course URL> --save-to-file`
-   Load course cache:
    -   `python main.py -c <Course URL> --load-from-file`
-   Change logging level:
    -   `python main.py -c <Course URL> --log-level DEBUG`
    -   `python main.py -c <Course URL> --log-level WARNING`
    -   `python main.py -c <Course URL> --log-level INFO`
    -   `python main.py -c <Course URL> --log-level CRITICAL`
-   Use course ID as the course name:
    -   `python main.py -c <Course URL> --id-as-course-name`
-   Encode in H.265:
    -   `python main.py -c <Course URL> --use-h265`
-   Encode in H.265 with custom CRF:
    -   `python main.py -c <Course URL> --use-h265 -h265-crf 20`
-   Encode in H.265 with custom preset:
    -   `python main.py -c <Course URL> --use-h265 --h265-preset faster`
-   Encode in H.265 using NVIDIA hardware transcoding:
    -   `python main.py -c <Course URL> --use-h265 --use-nvenc`
-   Use continuous numbering (don't restart at 1 in every chapter):
    -   `python main.py -c <Course URL> --continue-lecture-numbers`
    -   `python main.py -c <Course URL> -n`
-   Download specific chapters:
    - `python main.py -c <Course URL> --chapter "1,3,5"` - Downloads chapters 1, 3, and 5
    - `python main.py -c <Course URL> --chapter "1-5"` - Downloads chapters 1 through 5
    - `python main.py -c <Course URL> --chapter "1,3-5,7,9-11"` - Downloads chapters 1, 3 through 5, 7, and 9 through 11
-   Download specific chapters with quality:
    - `python main.py -c <Course URL> --chapter "1-3" -q 720`
-   Download specific chapters with captions:
    - `python main.py -c <Course URL> --chapter "1,3" --download-captions`

### About the Creator

Hello! I'm **Sheikh Bilal**, a passionate Java developer who loves coding and automation. This tool is a testament to that passion, designed to help you understand and explore Udemy automation.

Connect with me:
*   **GitHub**: [https://github.com/sheikh-bilal65](https://github.com/sheikh-bilal65)
*   **LinkedIn**: [https://www.linkedin.com/in/bilal-ahmad2](https://www.linkedin.com/in/bilal-ahmad2)
*   **Gmail**: [bilalahmadallbd@gmail.com](mailto:bilalahmadallbd@gmail.com)
*   **Instagram**: [https://www.instagram.com/sheikhh.bilal/](https://www.instagram.com/sheikhh.bilal/)

Facing issues? Hit me up on my Instagram or mail me!


This tool is provided for **educational purposes only**. It demonstrates automation techniques and is not intended for violating Udemy's Terms of Service or any applicable laws. The creator, Sheikh Bilal, is not responsible for any misuse of this tool or any consequences that may arise from its use. Users are solely responsible for adhering to Udemy's policies and local regulations.
