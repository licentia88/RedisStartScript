## How to Start Redis Automatically on WSL

To automate the process of starting Redis on WSL with a password prompt, follow these steps:

### Step 1: Create the Shell Script File (`start-redis.sh`)

1. **Open Ubuntu WSL on Windows**:
   - Open your terminal for Ubuntu in WSL.

2. **Create the Script File**:
   - In the terminal, type the following to open the nano editor and create a new file named `start-redis.sh` in your home directory:
     ```bash
     nano ~/start-redis.sh
     ```

3. **Add the Script Contents**:
   - In the nano editor, paste the following content:
     ```bash
     #!/bin/bash
     echo "Starting Redis with password prompt..."
     sudo service redis-server start
     ```
   - This script will start Redis and prompt for your password as usual.
   - To start redis witout password prompt add the following content
    ```bash
     #!/bin/bash
    echo "Starting Redis with prompt..."
    echo "asimLuna88!" | sudo -S service redis-server start
    ```
    **Make the Script Accessible Only to You**: Restrict access to the script so only your user account can read or execute it:
    ```bash
    chmod 700 ~/start-redis.sh
     ```
5. **Save and Exit**:
   - In nano, press `Ctrl + X` to exit.
   - When prompted to save, press `Y` for yes, then press `Enter` to confirm the filename.

### Step 2: Make the Script Executable

To allow the script to be executed directly, set the necessary permissions.

1. **Run the Following Command**:
   ```bash
   chmod +x ~/start-redis.sh

### Step 3: Test the Script

Run the script by typing:
```bash
~/start-redis.sh
```
This should prompt for your password and start the Redis service, or start the redis server depending on your script contents

### Step 4: (Optional) Set Up Task Scheduler to Run the Script on Windows Startup

If you want Redis to start every time Windows boots, you can configure Task Scheduler to run this script automatically.

1. **Open Task Scheduler in Windows**:
   - Press `Win + R`, type `taskschd.msc`, and press `Enter`.

2. **Create a New Task**:
   - Select **Action > Create Task**.

3. **Configure the Task**:
   - In the **General** tab, name the task (e.g., "Start Redis in WSL").
   - Under **Security options**, choose **Run whether user is logged on or not**.
   - Check **Run with highest privileges**.

4. **Set the Trigger**:
   - Go to the **Triggers** tab and click **New**.
   - Set the task to begin **At log on**.

5. **Add the Action**:
   - In the **Actions** tab, click **New**.
   - In **Action**, select **Start a program**.
   - In the **Program/script** box, enter:
     ```plaintext
     wsl
     ```
   - In the **Add arguments** box, enter:
     ```plaintext
     -d Ubuntu -- ~/start-redis.sh
     ```

This setup will ensure that the `start-redis.sh` script runs on each login, prompting you to enter the password when starting Redis.

