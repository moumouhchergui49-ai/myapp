name: Build APK

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Install dependencies
        run: |
          sudo apt update
          sudo apt install -y python3 python3-pip git zip unzip openjdk-17-jdk
     
          pip install --upgrade pip
          pip install cython buildozer

      - name: Build APK
        run: |
          buildozer init
          buildozer -v android debug

      - name: Upload APK
        uses: actions/upload-artifact@v3
        with:
          name: MyApp-APK
          path: bin/*.apk
