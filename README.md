<h1 align="center">📦 APK2AAB Converter</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%20%7C%20Android-blue.svg" />
  <img src="https://img.shields.io/badge/Language-Java%20%7C%20.NET-purple.svg" />
  <img src="https://img.shields.io/badge/Manual%20Support-Yes-green.svg" />
</p>

> **Convert your APKs to AAB (Android App Bundles) with ease.**  
> Use Windows, Android, or manual tools — complete guide below.  
> ⚠️ **Note:** APK2AAB (exe & apk tools) are no longer maintained due to time limitations. Manual method still works.

---

## 📥 Windows EXE Tool

📍 Location: `APK2AAB/Windows-exe/APK2AAb.exe`

### 🛠 Requirements:
- [.NET 6.0 Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)
- [Java 8](https://www.oracle.com/in/java/technologies/javase/javase8-archive-downloads.html) (Add to system environment variables)

### ⚙️ Usage:
- Ensure your APK and output AAB paths have **no spaces**
- Set same values in `AndroidManifest.xml`:
  - `minSdkVersion`
  - `targetSdkVersion`
  - `versionName`
  - `versionCode`
- Output AAB must be **signed** before uploading to Play Store

---

## 📱 Android APK Tool

📍 Location: `APK2AAB/Android-Tool/APK2AAb.apk`

### 🚀 Steps:
1. Install the APK on your Android device
2. Pick the APK file and choose output path
3. AAB will be generated at selected location
4. Sign it with your keystore before Play Store release

---

## 🔧 Manual Method (Fully Functional)

### 🔩 Required Tools:
| Tool | Link |
|------|------|
| Bundletool | [Download](https://github.com/google/bundletool/releases) |
| Apktool | [Download](https://github.com/iBotPeaches/Apktool) |
| AAPT2 | [Download](https://dl.google.com/dl/android/maven2/com/android/tools/build/aapt2/4.2.1-7147631/aapt2-4.2.1-7147631-windows.jar) |
| Android.jar | Provided in Android SDK |
| Java 8 | [Download](https://www.oracle.com/in/java/technologies/javase/javase8-archive-downloads.html) |

Add Java to system path: [Help Guide](https://www.java.com/en/download/help/path.html)

---

### 📂 Step-by-Step Instructions:

#### 1. **Unzip APK**

```bash
java -jar apktool_2.5.0.jar d test.apk -s -o decompile_apk -f
```

#### 2. **Compile Resources**

```bash
aapt2.exe compile --dir decompile_apk\res -o res.zip
```

#### 3. **Link Resources**

Replace variables with your values:

```bash
aapt2.exe link --proto-format -o base.zip -I android.jar --manifest decompile_apk\AndroidManifest.xml \
--min-sdk-version 7 --target-sdk-version 30 --version-code 1 --version-name 1.0 \
-R res.zip --auto-add-overlay
```

#### 4. **Prepare Final AAB Structure**

Unzip `base.zip`, and prepare directory as below:

```
base/
├── assets/
├── dex/
├── lib/
├── manifest/AndroidManifest.xml
├── res/
├── root/
│   └── kotlin/
└── resources.pb
```

#### 5. **Create base.zip**

From inside `/base` folder:

```bash
jar cMf base.zip manifest dex res root lib assets resources.pb
```

#### 6. **Generate AAB**

From your tools directory:

```bash
java -jar bundletool.jar build-bundle --modules=base.zip --output=base.aab
```

🎉 Your `.aab` file is ready!  
📌 Don't forget to **sign it** with your keystore before publishing to Play Store.

---

## 💡 Final Notes

- GUI tools (EXE/APK) are deprecated but still available
- Manual method is **tested** and fully functional
- Contributions, forks, or updates are welcome!

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/Anmol-In-Verse">Anmol-in-Verse</a>
</p>
