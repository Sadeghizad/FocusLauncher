# App Session Wrapper Maker

A modern **Windows launcher generator** that helps you limit, log, and manage your app usage.

With a simple **PySide6 UI**, you can:

* Select any `.exe` file.
* Set total allowed time and warning times.
* Automatically log start/end events (with reason prompt).
* Show on-screen warnings before time runs out.
* Automatically close the app when the limit is reached.
* (Optional) create a **desktop shortcut** with the original app’s icon.

---

## ✨ Features

* **Time-limited usage**
  Define a total session length, plus one or two warning popups.

* **Usage logging**
  Every launch is logged with timestamp and reason to a `.log` file.

* **Two-layer wrapper**

  * `.vbs` launcher → asks for your reason & starts monitoring.
  * `.bat` session script → tracks running time, shows warnings, kills app on timeout.

* **Shared popup script**
  A single `popup.vbs` file is reused across all apps.

* **Custom output locations**
  Choose where to store the wrappers and logs.

* **Desktop shortcut creation** *(requires pywin32)*
  Creates a `.lnk` pointing to the launcher, with the app’s icon.

---

## 📂 How It Works

1. **Pick the executable** you want to wrap.
   Example: `C:\Program Files\Telegram\Telegram.exe`

2. **Enter process name** (as in Task Manager → Details).
   Example: `Telegram.exe`

3. **Set session duration** and **warning times** in seconds.

4. **Choose output folder** (where `.vbs`, `.bat`, and `popup.vbs` will be stored).

5. **Choose log folder** (where `.log` files will be written).

6. *(Optional)* **Check “Create Desktop shortcut”** to auto-generate a `.lnk` on your desktop.

7. Click **Generate Wrapper**.

   * A `.vbs` launcher file is created for that app.
   * A `.bat` session monitor file is created.
   * A `popup.vbs` file is created if not already present.

8. **Launch the app** by double-clicking the generated `.vbs` file (or its shortcut).

---

## 📜 Session Flow

1. `.vbs` prompts: *“Why do you want to open {AppName}?”*
2. Reason is logged in `{AppName}.log` in your log folder.
3. `.bat` starts the app and tracks elapsed time.
4. At warning times → `popup.vbs` shows notifications.
5. If time runs out → `.bat` forcibly closes the app.
6. End reason & duration are logged.

---

## 🖼 Icons

* If `pywin32` is installed, the generated shortcut will use **the icon of your selected `.exe`**.
* Without `pywin32`, you can still run `.vbs` manually, but no icon customization is done.

---

## ⚡ Tip for Full Replacement

If you want this wrapper to completely replace your normal app shortcut **(including in Windows Search and Start Menu)**:

1. When generating, **check the “Create Desktop shortcut”** option.
2. **Copy that shortcut** and paste it into:

   * `%AppData%\Microsoft\Windows\Start Menu\Programs`
     *(this is what Windows Search uses)*
3. Replace your old app shortcut with the new one.
4. From now on, searching or clicking your app will use the **time-limited wrapper**.
