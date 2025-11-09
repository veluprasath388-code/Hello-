name: Build Laser Report APK

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up JDK
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'
      - name: Set up Android SDK
        uses: android-actions/setup-android@v2
      - name: Build debug APK
        run: ./gradlew assembleDebug
      - name: Upload APK artifact
        uses: actions/upload-artifact@v3
        with:
          name: LaserReport-APK
          path: app/build/outputs/apk/debug/app-debug.apk
