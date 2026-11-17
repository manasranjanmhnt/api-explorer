# Build and run on macOS

## Prerequisites

- A Mac running a supported macOS version.
- Node.js 22.12 or newer with npm.
- Git only if you need to scan or clone GitHub repositories.
- An Apple Developer ID Application certificate and app-specific password only if you want to sign and notarize the package.

Check the installed tools in Terminal:

```sh
node --version
npm --version
git --version
```

The Git check is optional. If Node.js was installed while Terminal was open, close and reopen Terminal before continuing.

## Get the project

Clone the public repository and enter its folder:

```sh
git clone https://github.com/manasranjanmhnt/reqzen.git
cd reqzen
```

For an existing checkout, use `cd` with that repository's path instead. All following commands must run in the directory containing `package.json`.

## Install, test, and run from source

Install the exact dependency versions in the lock file, run the tests, then launch the desktop app:

```sh
npm ci
npm test
npm start
```

The app's compiled UI is already included; there is no separate frontend build step.

## Create an unsigned macOS disk image

Close the running app, then run:

```sh
npm run dist:mac
```

The `.dmg` is written to `release/`. The build targets the architecture of the Mac running it: Apple silicon produces arm64; Intel produces x64. To install, open the disk image and drag Reqzen to Applications.

This package is unsigned and not notarized. On first launch, macOS may block the app. Only proceed if you obtained the build from the official Releases page and trust it. In Finder, Control-click Reqzen, choose **Open**, and confirm. If macOS still blocks the app, open **System Settings → Privacy & Security**, scroll to the Security section, and choose **Open Anyway** for Reqzen.

## Create a signed and notarized disk image

This requires a Developer ID Application certificate available in your login keychain and an app-specific password. Keep the credentials out of the repository, project files, and shell profiles. In Terminal, set them for this build only:

```sh
export CSC_NAME="Developer ID Application: Your Name (TEAMID)"
export APPLE_ID="you@example.com"
export APPLE_TEAM_ID="TEAMID"
printf "App-specific password: "
read -s APPLE_APP_SPECIFIC_PASSWORD
echo
export APPLE_APP_SPECIFIC_PASSWORD
npm run dist:mac-signed
unset APPLE_APP_SPECIFIC_PASSWORD
```

Replace the example certificate identity, Apple ID, team ID, and password with your own values. The signed and notarized `.dmg` is written to `release/`. If the build fails, check the certificate/keychain and Apple credentials; do not add them to the repository.

Build macOS packages on macOS. The Windows and macOS packages are separate outputs and should be built on their respective platforms.

## Optional: local model support

Install Ollama using its official macOS installer. In Terminal, download the model and start the local service:

```sh
ollama pull qwen2.5:3b
ollama serve
```

Basic search and scanning do not require Ollama. Model-assisted ranking and description filling do.
