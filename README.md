# Unity-WebGL-WebAudio

A robust Unity plugin that automatically manages Web Audio API contexts in WebGL builds, ensuring reliable audio playback across different browsers and device states.

## 🎯 Overview

This plugin solves common WebGL audio issues by intelligently handling AudioContext lifecycle events, including:
- Browser tab visibility changes
- Mobile device sleep/wake cycles  
- User interaction requirements for audio initialization
- AudioContext suspension and resumption
- Automatic recovery from closed/invalid audio contexts

## ✨ Features

- **Automatic AudioContext Management**: Handles suspend/resume cycles seamlessly
- **Mobile-Optimized**: Designed for iOS Safari and Android Chrome compatibility
- **Zero Configuration**: Works out of the box with Unity's audio system
- **Lightweight**: Minimal performance impact with smart event handling
- **Error Recovery**: Automatically recreates AudioContext when needed
- **Debug Logging**: Comprehensive console output for troubleshooting

## 🚀 Quick Start

### Installation

1. Download the latest release or clone this repository
2. Copy both files to your Unity project's `Plugins/WebGL` folder:
   ```
   Assets/
   └── Plugins/
       └── BrowserWEBAudio/
           ├── BrowserWEBAudio.cs
           └── BrowserWEBAudio.jslib
   ```
3. Add the `BrowserWEBAudio` component to any GameObject in your first scene
4. Build for WebGL - the plugin activates automatically!

### Folder Structure
```
YourUnityProject/
├── Assets/
│   └── Plugins/
│       └── BrowserWEBAudio/
│           ├── BrowserWEBAudio.cs      # Unity C# component
│           └── BrowserWEBAudio.jslib   # JavaScript library
└── ...
```

## 🔧 How It Works

### The Problem
WebGL audio faces several challenges:
- Browsers require user interaction before playing audio
- Mobile browsers suspend AudioContext when tabs become inactive
- AudioContext can become permanently closed on some devices
- Unity's built-in WebGL audio doesn't always handle edge cases

### The Solution
This plugin provides:

1. **Visibility Management**: Automatically suspends audio when the tab is hidden and resumes when visible
2. **Touch Activation**: Ensures AudioContext is ready after user interaction
3. **Smart Recovery**: Detects closed AudioContext and recreates it when needed
4. **Delayed Resume**: Accounts for mobile device audio hardware initialization delays

## 📱 Browser Compatibility

| Browser | Desktop | Mobile |
|---------|---------|--------|
| Chrome | ✅ | ✅ |
| Firefox | ✅ | ✅ |
| Safari | ✅ | ✅ |
| Edge | ✅ | ✅ |

## 🛠️ Technical Details

### Component Lifecycle
```csharp
void Start()
{
#if UNITY_WEBGL && !UNITY_EDITOR
    InitBrowserWEBAudio(); // Only runs in WebGL builds
#endif
}
```

### JavaScript Events Handled
- `visibilitychange`: Tab focus/blur management
- `touchstart`: Mobile interaction detection
- AudioContext state monitoring

### Performance Characteristics
- **Memory Usage**: < 1KB runtime footprint
- **CPU Impact**: Event-driven, no polling
- **Audio Latency**: No additional latency introduced

## 📄 API Reference

### C# Component
```csharp
public class BrowserWEBAudio : MonoBehaviour
{
    // Automatically initializes on Start() in WebGL builds only
    // No public methods - fully automatic operation
}
```

### JavaScript Functions
```javascript
// Internal functions (not for direct use)
InitBrowserWEBAudio()    // Main initialization
recreateAudioContext()   // Emergency recovery function
```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Unity Technologies for WebGL audio architecture
- Web Audio API specification contributors
- Community feedback and testing

---

**Made with ❤️ for Unity developers struggling with WebGL audio**

*If this plugin helped your project, consider giving it a ⭐ on GitHub!*
