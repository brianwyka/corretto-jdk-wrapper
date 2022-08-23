# Corretto JDK Wrapper

A wrapper script to manage downloading Corretto JDK or re-using a previously downloaded version.  

## Compatibility
Currently, this is only compatible with Linux and MacOS and Java 11+.

## Installation

Create a `.corretto/wrapper.properties` file in root of repository.
```sh 
mkdir -p .corretto
touch .corretto/wrapper.properties
```

Add a valid Corretto JDK `version` and `dist` to the file.
```properties
version = 17.0.4.9.1
dist = linux-x64
```

Add the `correttow` executable file to the root of the repository.
```sh 
curl -ksLO https://raw.githubusercontent.com/brianwyka/corretto-jdk-wrapper/main/correttow
chmod +x correttow
```

## Usage

Export the Corretto JDK Home location to `JAVA_HOME` environment variable.

__Uses version and dist from `.corretto/wrapper.properties`__
```sh 
export JAVA_HOME=$(./correttow)
```

__Specify version and dist in the command (overrides file)__
```sh 
export JAVA_HOME=$(./correttow '17.0.4.9.1' 'linux-x64')
```

## Integrations
This tooling is meant to integrate with other build tools such as `jEnv`, `Maven`, and `Gradle`.

For example, with `jenv`:
```sh 
jenv add $(./correttow)
```

For example, with `maven`:
```sh 
export JAVA_HOME=$(./correttow)
mvn clean install
```

For example, with `gradle`:
```sh 
gradle -Dorg.gradle.java.home=$(./correttow) clean build
```