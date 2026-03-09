# The Way God Intended - Installation Guides

### 🛠️ Client Installation Guide

Follow these steps to set up your Minecraft game to connect to the server.

### Prerequisites
* **Minecraft: Java Edition**.
* **Java 21** installed (required for Minecraft 1.21+).
* (For 3PC users)A Minecraft launcher of your choice (e.g., Prism Launcher, CurseForge, Badlion, Modrinth).
* (Curseforge is recommended for easy installation but not required)

### Standard Installation Steps (3PC Users)

*Note: If you are downloading the pre-packaged modpack from curseforge (or github), follow the modpack launcher's import instructions instead.*

1.  **Install Fabric Loader:**
    * Go to [fabricmc.net](https://fabricmc.net/) and download the installer.
    * Run the installer. Select the correct Minecraft Version (**1.21** or **1.21.10** as required) and the recommended Loader version.
    * Click "Install".

2.  **Locate your Minecraft Folder:**
    * **Windows:** `%appdata%\.minecraft`
    * **macOS:** `~/Library/Application Support/minecraft`
    * **Linux:** `~/.minecraft`

3.  **Install Mods & Dependencies:**
    * Open your `.minecraft` folder and locate (or create) the `mods` folder.
    * Download the `TWGI_v*_NON3PC.zip`
    * Copy all `.jar` files into the `mods` folder.
    * **Crucial:** Ensure you have the exact version of **Fabric API** required by the server, or you will encounter connection errors.

4.  **Install Resource Packs (Optional):**
    * Place `.zip` resource packs into the `resourcepacks` folder.

5.  **Launch the Game:**
    * Open your Minecraft Launcher.
    * Select the newly created profile titled "Fabric Loader [Minecraft Version]".
    * Launch the game.

## 🖥️ Server Installation (Self-Hosted)

Use this guide if you are hosting the server on your own hardware.

### Steps
1. **Directory Setup:** Create a new folder for your server files.
2. **Fabric Server Jar:** Download the Fabric Installer and select the "Server" tab. Choose version 1.21.10.
3. **Accept EULA:** Run the server once to generate `eula.txt`. Change `eula=false` to `eula=true`.
4. **Mod Cleanup:** Copy your mods to the server `mods` folder. **IMPORTANT:** You must delete client-only mods from the server folder to prevent connection errors:
    * `configured-fabric.jar`
    * `e4mc-minecraft.jar`
    * `ModMenu.jar`
5. **Launch:** Use a `start.bat` or `start.sh` script to run the server with Java 21.

## ☁️ Server Installation (Hosting Sites)

Use this guide for providers like ApexHosting, PebbleHost, Bisect, or Shockbyte.

### Steps
1. **Engine Selection:** Set your server type to **Fabric** and version to **1.21.10**.
2. **File Access:** Use the built-in File Manager or an SFTP client (like FileZilla) to access your server files.
3. **Upload Mods:** Upload your mods to the `/mods` directory.
4. **Remove Networking Blockers:** Ensure `configured-fabric` and `e4mc` are deleted from the server-side mods folder. These mods attempt to sync data that 1.21.10 cannot encode, leading to immediate "Connection Lost" errors.
5. **Restart:** Restart the server from your hosting dashboard.

## 🖥️ Dedicated Server Setup Steps

1.  **Setup Server Directory:**
    * Create a new empty folder on your machine dedicated to the server files (e.g., `~/Desktop/minecraft_server`).

2.  **Download & Install Fabric Server:**
    * Download the Fabric Installer from [fabricmc.net](https://fabricmc.net/).
    * Run the installer and select the **"Server"** tab.
    * Select Minecraft **[Version, e.g., 1.21]**.
    * Select your empty server folder as the installation location. Click "Install".

3.  **Download the Minecraft Server Jar:**
    * After the Fabric installation, click the "Download server jar" button in the installer window to download the vanilla `server.jar`.

4.  **Initial Launch & EULA:**
    * Open your command prompt/terminal, navigate to your server folder, and run:
        ```bash
        java -jar fabric-server-launch.jar nogui
        ```
    * The server will generate files and stop immediately.
    * Open the newly created `eula.txt` file and change `eula=false` to `eula=true`.

5.  **Install Mods & Dependencies:**
    * Locate the `mods` folder in your server directory.
    * Copy all server-side mods (`.jar`) into this folder.
    * **CRUCIAL compatibility notes for 1.21 sub-versions:**
        * **MATCH FABRIC API:** Ensure the server is running the *exact same version* of Fabric API as the clients to avoid `custom_payload` network desyncs.
        * **REMOVE CLIENT-SIDE MODS:** Do NOT install purely client-side mods on the server (e.g., *Configured*, *Oculus/Iris*, *ModMenu*). They will likely cause encoder exceptions (`EncoderException: Failed to encode packet configured:session_data`) and prevent players from joining.

6.  **Create a Startup Script:**
    * Create a new text file named `start.bat` (Windows) or `start.sh` (Linux/macOS) in your server folder. Paste the following (adjusting RAM `Xmx` as needed):

        **Windows (`start.bat`):**
        ```batch
        @echo off
        java -Xmx4G -Xms4G -jar fabric-server-launch.jar nogui
        pause
        ```

        **Linux/macOS (`start.sh`):**
        ```bash
        #!/bin/bash
        java -Xmx4G -Xms4G -jar fabric-server-launch.jar nogui
        ```
        *(Linux/macOS users: remember to `chmod +x start.sh`)*

7.  **Final Launch:**
    * Run your startup script (`start.bat` or `./start.sh`) to start the server.

## ⚠️ 1.21.10 Networking Stability Fixes

If you experience "Internal Exception" or "Connection Lost" errors, check the following:

| Error Message | Solution |
| :--- | :--- |
| **EncoderException (configured:session_data)** | Delete the **Configured** mod from the server files. It is a client-side utility and breaks 1.21.10 server networking. |
| **Unknown Target (carryon:carry_on_data)** | Ensure both client and server are using **Fabric API 0.115.4**. Newer versions may have packet sync issues with Carry On. |
| **Custom Payload Error** | Remove **e4mc** from the server. Use Port Forwarding or Essential for stable connectivity. |

## 📥 Download Links

| Resource | Link |
| :--- | :--- |
| **Fabric API (1.21.10)** | [Modrinth](https://modrinth.com/mod/fabric-api) |
| **Java 21** | [Adoptium](https://adoptium.net/temurin/releases/?version=21) |
