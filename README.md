# x86-uiautomator2-server

x86 server which connects to the **[Android UIAutomator2 Server](https://github.com/snakx/android-uiautomator2-server)**

# How it works

```
JadbConnection jadb = new JadbConnection();

// Deinstalliere Instrumentation
jadb.getAnyDevice().executeShell("pm uninstall com.github.uiautomator2.test");

// Deinstalliere Anwendung
jadb.getAnyDevice().executeShell("pm uninstall com.github.uiautomator2");

// Übertrage Instrumentation (C:\Users\Torsten Klinger\Desktop\snakx\android-uiautomator2-server\app\build\outputs\apk\androidTest\server\debug)
jadb.getAnyDevice().push(new File("snakx-uiautomator2-server-debug-androidTest.apk"), new RemoteFile( "/data/local/tmp/snakx-uiautomator2-server-debug-androidTest.apk"));

// Installiere Instrumentation (C:\Users\Torsten Klinger\Desktop\snakx\android-uiautomator2-server\app\build\outputs\apk\androidTest\server\debug)
jadb.getAnyDevice().executeShell("pm install -g " + Bash.quote("/data/local/tmp/snakx-uiautomator2-server-debug-androidTest.apk"));

// Übertrage Anwendung (C:\Users\Torsten Klinger\Desktop\snakx\android-uiautomator2-server\app\server\release)
jadb.getAnyDevice().push(new File("snakx-uiautomator2-server-release.apk"), new RemoteFile( "/data/local/tmp/snakx-uiautomator2-server-release.apk"));

// Installiere Anwendung (C:\Users\Torsten Klinger\Desktop\snakx\android-uiautomator2-server\app\server\release)
jadb.getAnyDevice().executeShell("pm install -g " + Bash.quote("/data/local/tmp/snakx-uiautomator2-server-release.apk"));

// Warte 7 Sekunden
Thread.sleep(7 * 1000);

// Starte Instrumentation
jadb.getAnyDevice().executeShell("am instrument -w -m    -e debug false -e class 'com.github.uiautomator2.test.UiAutomator2Server' com.github.uiautomator2.test/androidx.test.runner.AndroidJUnitRunner");

// Warte für immer
try {
    Object lock = new Object();
    synchronized (lock) {
        while (true) {
            lock.wait();
        }
    }
} catch (InterruptedException ex) {}
```
