# Homebrew Tap for claude-in-mobile

Homebrew formula for installing [claude-in-mobile](https://github.com/AlexGladkov/claude-in-mobile) CLI.

## Installation

```bash
brew tap AlexGladkov/claude-in-mobile-homebrew https://github.com/AlexGladkov/claude-in-mobile-homebrew
brew install claude-in-mobile
```

## Supported Platforms

- macOS ARM64 (Apple Silicon)

Other platforms coming soon.

---

## Maintainer Guide

### Updating the formula for a new release

1. **Build binaries** (see [CLI README](https://github.com/AlexGladkov/claude-in-mobile/tree/main/cli#building-release-binaries))

2. **Create GitHub Release** in `AlexGladkov/claude-in-mobile`:
   - Tag: `release-X.Y.Z`
   - Upload assets:
     - `claude-in-mobile-X.Y.Z-darwin-arm64.tar.gz`
     - `claude-in-mobile-X.Y.Z-darwin-x86_64.tar.gz` (optional)
     - `claude-in-mobile-X.Y.Z-linux-x86_64.tar.gz` (optional)

3. **Calculate SHA256 hashes**:
   ```bash
   shasum -a 256 claude-in-mobile-X.Y.Z-darwin-arm64.tar.gz
   ```

4. **Update formula** in `Formula/claude-in-mobile.rb`:
   ```ruby
   version "X.Y.Z"
   # ...
   sha256 "NEW_HASH_HERE"
   ```

5. **Test locally**:
   ```bash
   brew install --build-from-source ./Formula/claude-in-mobile.rb
   claude-in-mobile --version
   ```

6. **Commit and push**

### Formula structure

```ruby
class ClaudeInMobile < Formula
  version "X.Y.Z"

  on_macos do
    on_arm do
      url "https://github.com/.../release-X.Y.Z/claude-in-mobile-X.Y.Z-darwin-arm64.tar.gz"
      sha256 "..."
    end
    # Add on_intel block when x86_64 binary is available
  end

  # Add on_linux block when Linux binary is available
end
```

### Adding new platforms

To add Intel Mac support:

```ruby
on_macos do
  on_arm do
    url "...darwin-arm64.tar.gz"
    sha256 "ARM64_HASH"
  end
  on_intel do
    url "...darwin-x86_64.tar.gz"
    sha256 "X86_64_HASH"
  end
end
```

To add Linux support:

```ruby
on_linux do
  url "...linux-x86_64.tar.gz"
  sha256 "LINUX_HASH"
end
```

---

## Links

- [Main repository](https://github.com/AlexGladkov/claude-in-mobile)
- [CLI documentation](https://github.com/AlexGladkov/claude-in-mobile/tree/main/cli)
- [Releases](https://github.com/AlexGladkov/claude-in-mobile/releases)
