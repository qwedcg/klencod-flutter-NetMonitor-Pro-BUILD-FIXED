# NetMonitor Pro

Build configuration fixed for GitHub Actions.

- Android Gradle Plugin 8.7.3
- Gradle 8.9
- Java 17
- compileSdk 35
- targetSdk 35
- minSdk 23

The project uses a standard Android `app` module. This is intentional: placing the
Android source directly in the Gradle project root can trigger Gradle 8 implicit
file-dependency validation errors such as `compileDebugJavaWithJavac` consuming
`mergeDebugAssets`/`mergeExtDexDebug` outputs without an explicit dependency.

The VPN monitor requires the user to grant Android VPN permission and select at
least one launchable application. The current capture implementation reads IPv4
TCP/UDP packets from the VPN TUN interface and reports the remote endpoint.

Important: a VpnService is a routing VPN, not a passive packet-sniffer API. A
production monitor that must preserve full Internet connectivity while inspecting
all TCP/UDP traffic needs a packet-forwarding/user-space networking layer. The
included capture loop intentionally does not claim to provide transparent
forwarding for every protocol.
