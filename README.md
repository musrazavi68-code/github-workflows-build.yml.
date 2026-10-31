herename: Build APK
on:
  push:
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: unzip -q ProxyBot-phase*.zip
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/actions/setup-gradle@v3
        with:
          gradle-version: 8.7
      - run: gradle assembleDebug --no-daemon
        working-directory: ProxyBot
      - uses: actions/upload-artifact@v4
        with:
          name: ProxyBot-APK
          path: ProxyBot/app/build/outputs/apk/debug/app-debug.apk
