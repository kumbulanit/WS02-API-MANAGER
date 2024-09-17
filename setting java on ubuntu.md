To set the `JAVA_HOME` environment variable for OpenJDK 11 on Ubuntu, follow these steps:

### Step 1: Install OpenJDK 11
If OpenJDK 11 is not installed, you can install it using the following command:
```bash
sudo apt update
sudo apt install openjdk-11-jdk
```

### Step 2: Find the Java Installation Path
After installation, determine the installation path of OpenJDK 11 by running:
```bash
sudo update-alternatives --config java
```
The output will show the installation paths of the installed Java versions. For OpenJDK 11, the path is usually something like:
```
/usr/lib/jvm/java-11-openjdk-amd64
```

### Step 3: Set the `JAVA_HOME` Environment Variable
Once you have the installation path, set the `JAVA_HOME` variable.

#### Temporary Setup (For Current Session Only)
You can set `JAVA_HOME` temporarily by running:
```bash
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```

To verify that `JAVA_HOME` is set, run:
```bash
echo $JAVA_HOME
```

#### Permanent Setup (For All Sessions)
To set `JAVA_HOME` permanently, you need to add the export command to your shell configuration file.

- If you use **Bash** (the default shell on Ubuntu):
  ```bash
  echo "export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64" >> ~/.bashrc
  ```

- If you use **Zsh**:
  ```bash
  echo "export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64" >> ~/.zshrc
  ```

After adding the line, apply the changes by running:
```bash
source ~/.bashrc  # For Bash users
# or
source ~/.zshrc   # For Zsh users
```

### Step 4: Verify `JAVA_HOME`
To ensure `JAVA_HOME` is correctly set, run:
```bash
echo $JAVA_HOME
```

You can also check the Java version to confirm:
```bash
java -version
```

This should now display the correct path and version of OpenJDK 11.