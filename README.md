# MULTIPLE JAVA VERSION USING HOMEBREW AND JENV


## INSTALLING JENV
We need to install a tool called **jenv** - Java version manager which is similar to **nvm**(nodeJs version manager).

```bash
brew install jenv
```
Export the jenv path to .bash_profile or .zshrc - whatever you are using. I am using .zshrc
```bash
echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(jenv init -)"' >> ~/.zshrc
source ~/.zshrc
```
Check the jenv health
```bash
jenv doctor
```
It will return something similar to this 
```bash
[OK]	No JAVA_HOME set
[ERROR]	Java binary in path is not in the jenv shims.
[ERROR]	Please check your path, or try using /path/to/java/home is not a valid path to java installation.
	PATH : /usr/local/Cellar/jenv/0.5.2/libexec/libexec:/Users/gramcha/.jenv/shims:/Users/gramcha/.jenv/shims:/Users/gramcha/.jenv/bin:/Users/gramcha/.jenv/bin:/Users/gramcha/chromedriver:/opt/local/bin:/opt/local/sbin:/Users/gramcha/.jenv/shims:/Users/gramcha/.jenv/bin:/Users/gramcha/.jenv/bin:/Users/gramcha/chromedriver:/opt/local/bin:/opt/local/sbin:/Users/gramcha/.jenv/shims:/Users/gramcha/.jenv/bin:/Users/gramcha/.jenv/shims:/Users/gramcha/.jenv/bin:/Users/gramcha/chromedriver:/opt/local/bin:/opt/local/sbin:/Users/gramcha/.nvm/versions/node/v10.17.0/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
[OK]	Jenv is correctly loaded
```
No need to worry about error message as long as **Jenv is correctly loaded** is printed.
To ensure that JAVA_HOME is correct
```bash
jenv enable-plugin export
```
Assuming Maven is used and to educate maven about Java version used
```bash
jenv enable-plugin maven
```

## INSTALLING JAVA

Intalling latest open jdk version at the time of writing this script
```bash
brew install openjdk
```
After installation complete execute the suggested command by the installation process
```bash
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk

openjdk is keg-only, which means it was not symlinked into /usr/local,
because it shadows the macOS `java` wrapper.

If you need to have openjdk first in your PATH run:
  echo 'export PATH="/usr/local/opt/openjdk/bin:$PATH"' >> ~/.zshrc

For compilers to find openjdk you may need to set:
  export CPPFLAGS="-I/usr/local/opt/openjdk/include"
```
similar if you want to install java8 execute below and follow the instruction command.
```bash
brew install openjdk@8
```


## ADD JAVA TO JENV JAVA LIST

Execute below command to see available JVM's in machine
```bash
/usr/libexec/java_home -V
```
It will print something like this
```bash
17.0.11 (x86_64) "Eclipse Adoptium" - "OpenJDK 17.0.11" /Library/Java/JavaVirtualMachines/temurin-17.jdk/Contents/Home
    11.0.23 (arm64) "Homebrew" - "OpenJDK 11.0.23" /opt/homebrew/Cellar/openjdk@11/11.0.23/libexec/openjdk.jdk/Contents/Home
/Library/Java/JavaVirtualMachines/temurin-17.jdk/Contents/Home
```

above command will show the list of available java on your machine, now Add java to the jenv java list.
by typing  ```jenv add JAVAPATH``` example
```bash
jenv add /Library/Java/JavaVirtualMachines/openjdk.jdk/Contents/Home
jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
```
It will print something like this.
```
openjdk64-17.0.1 added
17.0 added
```
Check the available java on jenv
```
jenv versions
```
It will print something like this
```
* system
  11
  11.0
  11.0.23
  17
  17.0
  17.0.11
  openjdk64-11.0.23
  temurin64-17.0.11
```


## SET USED JAVA USING JENV

Set system level version
```bash
jenv global 17
```
Some of projects wants older version like java8 to support that add project wise version.
Go inside the specific project folder and execute below command
```bash
jenv local 1.8
```
This will create the .java-version file that describes which java version to use.
To set the java specific version at teminal level execute that
```bash
jenv shell 1.8
```
Check the `jenv versions` it should print
```bash
  system
  11
  11.0
  11.0.23
* 17 (set by USER/.jenv/version)
  17.0
  17.0.11
  openjdk64-11.0.23
  temurin64-17.0.11
```

now check your java version
```bash
java --version
```
