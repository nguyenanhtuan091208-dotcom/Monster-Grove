# AN · Monster Grove

Monster Grove is a browser puzzle RPG with Minesweeper clues, turn-based encounters, and creature befriending. This export contains the current Vietnamese and English game, including Easy, Normal, Hard, and Expert. A fresh page opens in Vietnamese on Hard, as in the original.

## Play on Windows

1. Right-click the ZIP and choose **Extract All**.
2. Open `Monster-Grove/web/index.html` in Microsoft Edge, Chrome, or Firefox. Keep the `web` folder intact so the page can load the game script, stylesheet, and fonts.
3. Pick a difficulty, then click or tap a tile. Use right-click, a half-second hold, or Flag mode to mark a tile. A correctly flagged monster grants a pre-emptive strike when you reveal its tile. Reveal every safe tile and defeat or befriend every monster to win.

The game has no build step. For development, serving the files over localhost also gives the browser a consistent origin for fonts. If you have Python installed, open PowerShell in `Monster-Grove` and run the command below. Open [the local game](http://localhost:8000/) in your browser and press **Ctrl+C** in PowerShell when finished.

```powershell
py -m http.server 8000 --bind 127.0.0.1 --directory web
```

## Project layout

```text
Monster-Grove/
  README.md
  web/
    index.html       Game page, HUD, and battle dialog
    style.css        Existing layout and styling
    game.js          Grid, controls, battles, difficulty, and translations
    assets/
      fonts/         DM Sans and Space Grotesk, local CSS, and license files
```

The game markup and JavaScript match the current playable version. The only stylesheet change points to local copies of the Google Fonts resources, including Vietnamese subsets. Creature art and icons are emoji and text rendered by the operating system. Their appearance can vary by device. The font licenses are in `web/assets/fonts/`.

## Upload to GitHub

Create an empty GitHub repository and copy its HTTPS URL. Open PowerShell in the extracted `Monster-Grove` folder. With Git for Windows installed and your GitHub account ready to authenticate, run these commands after replacing `YOUR-ACCOUNT` and `YOUR-REPO`.

```powershell
git init -b main
git add README.md web
git commit -m "Import Monster Grove source"
git remote add origin https://github.com/YOUR-ACCOUNT/YOUR-REPO.git
git push -u origin main
```

See [GitHub’s guide to importing local code](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github).

## Use the source in an Android app

1. In Android Studio, create a Kotlin project with a Views activity and add the AndroidX WebKit dependency. Use a `WebView` as the activity’s content view.
2. Copy `web/` to `app/src/main/assets/web/`, keeping the directory structure. Configure `WebViewAssetLoader` with an `AssetsPathHandler` at `/assets/`. Use a `WebViewClientCompat` to delegate resource requests to the loader.
3. Enable JavaScript on the `WebView` for the local game and load `https://appassets.androidplatform.net/assets/web/index.html`. The bundled fonts load from assets alongside the game files.
4. Run on a device or emulator with an up-to-date Android System WebView. Check tap and hold controls, the battle dialog, both languages, and each difficulty before packaging the Android build.

See [Android’s guide to loading local WebView content](https://developer.android.com/develop/ui/views/layout/webapps/load-local-content) for the activity code. This ZIP is the web source project. You add the native wrapper in Android Studio.
