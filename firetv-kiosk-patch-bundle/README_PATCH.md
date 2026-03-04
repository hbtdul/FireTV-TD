# FireTV Kiosk – Patch Bundle

Dieses ZIP ist **kein vollständiges Android-Projekt**, sondern ein **Patch-Bundle** zum Einfügen in dein bestehendes Repo.

## Enthalten
- `MainActivity.kt` mit:
  - Options-Taste (Fire TV) öffnet Dialog für **URL + Rotation (0/90/180/-90)**
  - Rotation wird gespeichert und auf `root` angewendet
  - optionaler Update-Check über GitHub Releases (APK-Asset: `firekiosk.apk`)
- GitHub Actions:
  - `android-build.yml`: baut Debug-APK bei Push/Manual und lädt Artifact hoch
  - `release-apk.yml`: baut APK bei Tag `v*` und hängt `firekiosk.apk` ans Release → fester Downloader-Link

## Einbau (kurz)
1) `MainActivity.kt` nach:
   `app/src/main/java/de/firewebkiosk/MainActivity.kt` kopieren (ersetzen).
2) Workflows nach:
   `.github/workflows/android-build.yml`
   `.github/workflows/release-apk.yml`

## Voraussetzungen
- Dein Repo muss im Root den **Gradle Wrapper** enthalten:
  - `gradlew`, `gradlew.bat`, `gradle/wrapper/...`
- `activity_main.xml` braucht:
  - `FrameLayout` mit `@+id/root`
  - `WebView` mit `@+id/webView`

## Fire TV Install-Link (Downloader)
Sobald du ein Tag pushst/Release erstellst (z.B. `v1.0.0`) und der Workflow durch ist:

`https://github.com/<USER>/<REPO>/releases/latest/download/firekiosk.apk`

## Hinweis: AndroidManifest namespace
Wenn du im Manifest noch `package="..."` hast, entferne es und setze stattdessen im `app/build.gradle`:

```gradle
android {
  namespace "de.firewebkiosk"
}
```
