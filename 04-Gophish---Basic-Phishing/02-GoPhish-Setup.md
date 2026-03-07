# Installing GoPhish on Your Ubuntu EC2 Instance

In this section, we'll walk through the installation of **GoPhish**, an open-source phishing toolkit built with Golang. We'll cover updating your server, installing Golang, cloning the GoPhish repository, and preparing the executable. Finally, we'll set up GoPhish as a system service to ensure it runs automatically after server reboots.

## Step 1: Update Your Ubuntu Instance

Before installing any new software, it's good practice to update your package lists and upgrade existing packages.

```bash
sudo apt update
sudo apt upgrade -y
```

This ensures your server has the latest security patches and dependencies.

## Step 2: Install Golang

GoPhish is written in Golang, so you'll need to install the Go compiler.

```bash
sudo apt install golang-go -y
```

After installation, verify that Go is installed correctly:

```bash
go version
```

You should see output similar to `go version go1.x.x linux/amd64`.

## Step 3: Clone the GoPhish Repository

Navigate to your home directory (or any directory where you want to store GoPhish) and clone the official repository.

```bash
git clone https://github.com/gophish/gophish.git
```

This will create a folder named `gophish` containing all the source files.

## Step 4: Build GoPhish

Change into the `gophish` directory and build the executable.

```bash
cd gophish
go build
```

The build process may take a few minutes. Once completed, you'll see a new executable file named `gophish` in the directory (highlighted in green when you run `ls`).

### Note on SQLite Errors

During the build, you might see an error related to SQLite. This is a known issue and can be safely ignored—it does not affect the functionality of GoPhish.

## Step 5: Verify the Build

Run `ls` to confirm the presence of the `gophish` executable:

```bash
ls -la
```

You should see a file named `gophish` with execute permissions.

## Step 6: Set Up GoPhish as a System Service (Optional but Recommended)

To ensure GoPhish starts automatically whenever your EC2 instance reboots, you can configure it as a systemd service.

### Create a Systemd Service File

1. Create a new service file using `nano` or your preferred text editor:

   ```bash
   sudo nano /etc/systemd/system/gophish.service
   ```

2. Add the following content to the file:

   ```ini
   [Unit]
   Description=GoPhish Phishing Server
   After=network.target

   [Service]
   Type=simple
   User=ubuntu
   WorkingDirectory=/home/ubuntu/gophish
   ExecStart=/home/ubuntu/gophish/gophish
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```

   - Adjust the `User` and `WorkingDirectory` paths if your username or installation directory differs.

3. Save and exit the file (in `nano`, press `Ctrl+O`, then `Enter`, and `Ctrl+X`).

### Enable and Start the Service

```bash
sudo systemctl daemon-reload
sudo systemctl enable gophish.service
sudo systemctl start gophish.service
```

### Verify the Service Status

```bash
sudo systemctl status gophish.service
```

You should see output indicating that the service is active and running.

## Next Steps

With GoPhish installed and set up as a system service, it will now run continuously in the background. In the next file, we'll configure GoPhish and explore its web interface to start building phishing campaigns.

---

*Note: If you encounter any issues during installation, double-check that all dependencies are installed and that you've followed each step carefully.*
