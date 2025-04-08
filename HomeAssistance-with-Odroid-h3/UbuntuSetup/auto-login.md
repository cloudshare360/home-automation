To enable auto-login on Ubuntu Desktop, follow these steps:

### **Method 1: Using GUI (Recommended for most users)**
1. Open **Settings**:
   - Click the **Activities** menu (top-left corner or press `Super` (Windows) key).
   - Search for **"Settings"** and open it.

2. Go to **Users**:
   - In the left sidebar, click **"Users"**.
   - Unlock the settings by clicking **"Unlock"** (you'll need your password).

3. Enable Auto-Login:
   - Toggle the **"Automatic Login"** switch to **ON**.
   - Select your user account from the dropdown if prompted.

4. Restart to Test:
   - Reboot your system (`sudo reboot` or via the power menu).
   - Your system should now log in automatically.

---

### **Method 2: Using Command Line (For Advanced Users)**
1. Edit the **GDM (GNOME Display Manager)** configuration:
   ```bash
   sudo nano /etc/gdm3/custom.conf
   ```
   (Use `daemon.conf` for older Ubuntu versions.)

2. Add or modify these lines:
   ```ini
   [daemon]
   AutomaticLoginEnable = true
   AutomaticLogin = your_username
   ```
   Replace `your_username` with your actual username.

3. Save (`Ctrl+O`) and exit (`Ctrl+X`).

4. Restart:
   ```bash
   sudo systemctl restart gdm3
   ```

---

### **Troubleshooting**
- If auto-login fails:
  - Ensure no password is required on wake/screensaver (`Settings` → `Privacy` → `Screen Lock`).
  - Check for typos in `/etc/gdm3/custom.conf`.
  - For LightDM (Ubuntu flavors like Xubuntu/Lubuntu), edit `/etc/lightdm/lightdm.conf` instead.

Let me know if you need further adjustments!