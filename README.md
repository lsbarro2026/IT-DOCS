# SiteDocs helper

The SiteDocs helper runs on a computer you control and receives the photographs the SiteDocs iPhone
app takes, saving them in folders that follow the site you are documenting. Pair a phone with it
once, and photographs arrive whenever both are running, including when the phone is on another
network.

Download it from the [latest release](https://github.com/lsbarro2026/IT-DOCS/releases/latest), which
says which file your machine needs and how to check it.

## Install and first run

Where a step names a file, use the name of the one you downloaded. The command-line helper runs until
you press Ctrl+C and remembers its folder, so later runs need only `serve`.

### Mac app

1. Open `sitedocs-helper-desktop-darwin-universal.zip`. If your browser has not unzipped it already,
   double-click it in Finder.
2. Double-click **SiteDocs helper**. When macOS asks whether you are sure you want to open it, click
   **Open**.
3. Choose the folder to receive photographs into.
4. [Pair a phone](#pair-a-phone).

Closing the window leaves the helper running, with its icon in the menu bar. To start it each time
you log in, click **Keep running after login** once a phone is paired, and confirm.

### Linux desktop app

1. Make the file executable:

   ```
   chmod +x sitedocs-helper-desktop-linux-amd64
   ```

2. Open it. In GNOME Files, right-click it and choose **Run as a Program…**. From a terminal, run
   `./sitedocs-helper-desktop-linux-amd64`.
3. Choose the folder to receive photographs into.
4. [Pair a phone](#pair-a-phone).

To start it each time you log in, click **Keep running after login** once a phone is paired, and confirm.

### Windows

1. Open PowerShell in the folder you downloaded the file into, and start the helper:

   ```
   .\sitedocs-helper-windows-amd64.exe serve
   ```

2. If Windows shows **Windows protected your PC**, click **More info**, then **Run anyway**.
3. When the helper asks which folder to receive photographs into, press Enter to accept the one it
   offers, or type another path.
4. [Pair a phone](#pair-a-phone).

### Linux command line

1. On the machine itself, download the file, make it executable and start the helper:

   ```
   curl -LO https://github.com/lsbarro2026/IT-DOCS/releases/latest/download/sitedocs-helper-linux-amd64
   chmod +x sitedocs-helper-linux-amd64
   ./sitedocs-helper-linux-amd64 serve
   ```

   That address always fetches the latest release. To check the file, fetch
   `https://github.com/lsbarro2026/IT-DOCS/releases/latest/download/SHA256SUMS` as well, and follow
   the release's **Verify the download**.
2. When the helper asks which folder to receive photographs into, press Enter to accept `~/SiteDocs`,
   or type another path. In a script, where nothing can answer, name a folder that already exists
   instead: `./sitedocs-helper-linux-amd64 serve --dir /srv/sitedocs --pair`.
3. [Pair a phone](#pair-a-phone).

### Mac command line

1. In Terminal, in the folder you downloaded the file into, make it executable and start the helper:

   ```
   chmod +x sitedocs-helper-darwin-arm64
   ./sitedocs-helper-darwin-arm64 serve
   ```

2. macOS refuses to open it the first time. Open **System Settings**, click **Privacy & Security**,
   scroll down to the message about `sitedocs-helper-darwin-arm64`, and click **Open Anyway**.
   Confirm with your password or Touch ID, and the helper starts.
3. When the helper asks which folder to receive photographs into, press Return to accept
   `~/SiteDocs`, or type another path.
4. [Pair a phone](#pair-a-phone).

## Pair a phone

1. Show the helper's pairing code:
   - In the desktop app, click **Pair a phone**.
   - From the command line, open the link the helper prints on its first run,
     `https://127.0.0.1:8443/pairing/`, in a browser on the same machine. Your browser warns about the
     page's certificate, because the helper makes its own; continue to the page (in Chrome, click
     **Advanced**, then **Proceed to 127.0.0.1 (unsafe)**). To pair another phone later, start the
     helper with `serve --pair`.
2. In the SiteDocs app, open **Pair a Helper**, tap **Scan the helper's code**, and hold the phone
   over the code.

On a machine you reach over SSH, forward the port from your own computer, then open the same link
there:

```
ssh -L 8443:127.0.0.1:8443 you@helper-host
```

If you cannot scan the code, type the helper's address and its eight-character code into the app
instead, under **If you cannot scan the code**. A code works for ten minutes.

## Update to a new version

Quit the helper, then install the new release the same way, in place of the old file or app. The
folder, settings and paired phones carry over. If the helper starts when you log in, click **Keep
running after login** again in the new version, so that the copy started at login is the new one.

## Version numbers

To see which version a helper is, run it with `version`:

```
./sitedocs-helper-linux-amd64 version
```

It prints the version and then the build, such as `1.2.0 (4f9a2c1)`. For the Mac app, select it in
Finder and choose **File** > **Get Info**.

The first number goes up when an update needs the SiteDocs app updated too, or stops supporting a
system the previous version ran on. The second goes up when the helper gains something you would
notice, and the third for fixes only.

## Reporting a problem

[Open an issue](https://github.com/lsbarro2026/IT-DOCS/issues/new) that says what you did and what
happened, with the line `version` prints and your operating system and its version. Issues are
public, so leave out site names, addresses, pairing codes and photographs.
