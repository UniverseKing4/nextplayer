# Next Player - Auto Build & Release

Android video player with automated CI/CD pipeline.

## Automated Workflow

The repository includes a GitHub Actions workflow that automatically:
- ✅ Builds the APK on every push to `main`
- ✅ Signs the APK with your keystore
- ✅ Uploads build artifacts
- ✅ Creates GitHub releases with APK when you push a tag

## Setup Instructions

### 1. Generate Signing Key

```bash
keytool -genkey -v -keystore release.keystore -alias nextplayer -keyalg RSA -keysize 2048 -validity 10000
```

### 2. Convert Keystore to Base64

```bash
base64 release.keystore > keystore.txt
```

### 3. Add GitHub Secrets

Go to: `Settings` → `Secrets and variables` → `Actions` → `New repository secret`

Add these secrets:
- `SIGNING_KEY`: Content of keystore.txt (base64 encoded keystore)
- `ALIAS`: Your keystore alias (e.g., "nextplayer")
- `KEY_STORE_PASSWORD`: Your keystore password
- `KEY_PASSWORD`: Your key password

## Usage

### Automatic Build on Push
```bash
git add .
git commit -m "Your changes"
git push origin main
```
→ Workflow runs automatically, APK available in Actions artifacts

### Create Release
```bash
git tag v1.0.0
git push origin v1.0.0
```
→ Workflow creates a GitHub release with the signed APK

## Workflow Features

- Java 17 setup
- Gradle build with caching
- APK signing
- Artifact upload (every push)
- GitHub release creation (on tags)
- Auto-generated release notes

---

Repository: https://github.com/UniverseKing4/nextplayer
