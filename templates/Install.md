# Installation Instructions
This document explains how to obtain the Git Credential Manager for Mac and Linux (GCM) and how to configure Git to use the GCM as its credential helper.


## System Requirements

Great care was taken to avoid using any features of Java that would impact compatibility with Java 6.  Unfortunately, at this time, only the JavaFX-based browser is available, which excludes Java 6.  If you find a compatibility issue, please report it and provide as many details about your platform as necessary to reproduce the problem.

1. Mac OS X version 10.10.5 and up OR a GNU/Linux distribution with a desktop environment.
2. Oracle Java 7 Update 6 and up, Oracle Java 8, or OpenJDK with OpenJFX.
3. Git version 1.9 and up.


## How to install
On Mac OS X, installing via Homebrew is highly recommended.
On Linux, if you have an RPM-based package manager, installing via the RPM is recommended.
You will also soon have the option of installing via Linuxbrew.

If you can't use any of the package managers, you can also download [${project.artifactId}-${project.version}.jar](https://github.com/Microsoft/Git-Credential-Manager-for-Mac-and-Linux/releases/download/${project.artifactId}-${project.version}/${project.artifactId}-${project.version}.jar) somewhere safe and stable, such as `~/${project.artifactId}/`, and then follow the instructions for automatic or manual configuration.


### Installing on Mac using Homebrew (recommended)

1. Install the needed resources using Homebrew:

    ```
    brew install ${project.artifactId}
    ```
2. Run the GCM in `install` mode, which will check its requirements and then update the "global" Git configuration file (the one in your home folder):

    ```
    ${project.artifactId} install
    ```

    
### Installing on Linux using RPM (recommended)

1. Download [${project.artifactId}-${project.version}-1.noarch.rpm](https://github.com/Microsoft/Git-Credential-Manager-for-Mac-and-Linux/releases/download/${project.artifactId}-${project.version}/${project.artifactId}-${project.version}-1.noarch.rpm) and copy the file somewhere locally.
2. Download the [PGP key used to sign the RPM](https://java.visualstudio.com/Content/RPM-GPG-KEY-olivida.txt).
3. Import the signing key into RPM's database:

    ```
    sudo rpm --import RPM-GPG-KEY-olivida.txt
    ```
4. Verify the GCM RPM:

    ```
    rpm --checksig --verbose ${project.artifactId}-${project.version}-1.noarch.rpm
    ```
    ...you should see a line (among those there) that is equal to the following:
    
    ```
    V4 RSA/SHA256 Signature, key ID ba34dbc2: OK
    ```
5. Install the RPM:

    ```
    sudo rpm --install ${project.artifactId}-${project.version}-1.noarch.rpm
    ```
6. Run the GCM in `install` mode, which will check its requirements and then update the "global" Git configuration file (the one in your home folder):

    ```
    ${project.artifactId} install
    ```


### Installing on Mac or Linux without a package manager
Download [${project.artifactId}-${project.version}.jar](https://github.com/Microsoft/Git-Credential-Manager-for-Mac-and-Linux/releases/download/${project.artifactId}-${project.version}/${project.artifactId}-${project.version}.jar) somewhere safe and stable, such as `~/${project.artifactId}/`

#### Automatic configuration (recommended)
1. Run the GCM in `install` mode, which will check its requirements and then update the "global" Git configuration file (the one in your home folder):

    ```
    java -jar /home/example/${project.artifactId}/${project.artifactId}-${project.version}.jar install
    ```

#### Manual configuration
1. Configure the `credential.helper` setting to launch Java with the absolute path to the JAR (make sure you surround the whole value with 'single quotes'):

    ```
    git config --global credential.helper '!java -Ddebug=false -jar /home/example/${project.artifactId}/${project.artifactId}-${project.version}.jar'
    ```


## How to enable (or disable) debug mode

Debug mode will turn on tracing and assertions, producing a lot of output to `stderr`.  Only turn this on temporarily, when trying to isolate a defect.


### Automatic configuration (recommended)
1. Run the GCM in `install` mode with the `debug` property set to `true` (or `false` to disable):

    ```
    java -Ddebug=true -jar /home/example/${project.artifactId}/${project.artifactId}-${project.version}.jar install
    ```

### Manual configuration
1. Retrieve the value of the `credential.helper` configuration:

    ```
    git config --global --get credential.helper ${project.artifactId}
    ```
    ...it should look like this:

    ```
    !java -Ddebug=false -jar /home/example/${project.artifactId}/${project.artifactId}-${project.version}.jar
    ```
2. Set a new value for the `credential.helper` configuration (essentially repeating the _manual configuration step_, being careful with quoting and spaces), changing the value of the `debug` property to `true` (or `false` to disable).


## How to remove or uninstall
We are sad to see you go!  Please give us some feedback on how we could do better next time.

### Uninstall from Mac using Homebrew

1. Run the GCM in `uninstall` mode, which will update the "global" Git configuration file (the one in your home folder):

    ```
    ${project.artifactId} uninstall
    ```
2. Uninstall the ${project.artifactId} package with Homebrew:

    ```
    brew uninstall ${project.artifactId}
    ```
3. Archive the `insecureStore.xml` file from the `${project.artifactId}` sub-folder under your HOME folder.


### Uninstall from Linux using RPM

1. Run the GCM in `uninstall` mode, which will update the "global" Git configuration file (the one in your home folder):

    ```
    ${project.artifactId} uninstall
    ```
2. Uninstall the ${project.artifactId} package with RPM:

    ```
    sudo rpm --erase ${project.artifactId}-${project.version}-1.noarch
    ```
3. Archive the `insecureStore.xml` file from the `${project.artifactId}` sub-folder under your HOME folder.


### Automatic configuration removal (recommended)
1. Retrieve the value of the `credential.helper` configuration:

    ```
    git config --global --get credential.helper ${project.artifactId}
    ```
2. Run the GCM in `uninstall` mode, which will update the "global" Git configuration file (the one in your home folder):

    ```
    java -jar /home/example/${project.artifactId}/${project.artifactId}-${project.version}.jar uninstall
    ```
3. The value retrieved in _step 1_ contained the path to the JAR.  You can go delete that JAR.
4. Archive the `insecureStore.xml` file from the `${project.artifactId}` sub-folder under your HOME folder.


### Manual configuration removal

1. Retrieve the value of the `credential.helper` configuration:

    ```
    git config --global --get credential.helper ${project.artifactId}
    ```
2. Delete the value of the `credential.helper` configuration:

    ```
    git config --global --unset credential.helper ${project.artifactId}
    ```
3. The value retrieved in _step 1_ contained the path to the JAR.  You can go delete that JAR.
4. Archive the `insecureStore.xml` file from the `${project.artifactId}` sub-folder under your HOME folder.