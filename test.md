# CPML Coding Standard

If you haven't written in a "coding standard" before it is written out instruction's of how the code
should be written. Following the "coding standard" will allow the code to be easily understood and will also make the
entire project similar in the "coding standard"

## 1. Naming Conventions

### 1a. Variables

- Use descriptive names clearly states the purpose.
- Use [camelCase](https://en.wikipedia.org/wiki/Camel_case) for variable names.
- Don't create variables with the name length greater than 25 characters.

<details>
<summary>Example</summary>

```java
private String projectVersion = "1.0.0";
private double currentProjectBuild = 1;
private boolean developerMode = false;
```

</details>

### 2b. Methods and Method Parameters

- Use [camelCase](https://en.wikipedia.org/wiki/Camel_case) for both methods and parameters.
- Use descriptive names that accurately describe the action performed by the parameter or method.
- Method names can not be longer than 17 characters.
- Parameter names can not be longer than 20 characters.

<details>
<summary>Example</summary>

```java
public int initModLoader(ClassLoader currentClassLoader, Logger infoLogger, String[] args) {
    return ExitCode.INIT_LOADER_CRASH;
}
```

</details>

### 3c. Classes, Enums and Annotations

- Use [PascalCase](https://en.wiktionary.org/wiki/Pascal_case) for Classes, Enums and Annotations.
- Only use clear and concise words to explain a class, enum and annotation.
- Classes, Enums and Annotations can not be longer than 20 characters.

<details>
<summary>Example</summary>

```java
// class example
public class ModFile {
}

//enum
public enum Environment {}

// annotation
public @interface ModInfo {
}
```

</details>

### 4d. Interfaces

- Use [PascalCase](https://en.wiktionary.org/wiki/Pascal_case) for Interfaces.
- Use descriptive names that clearly explain what the interface is doing.
- Interface names can not be longer than 20 characters.
- At the prefix of every interface add a "I" to indicate it is an interface.

<details>
<summary>Example</summary>

```java
public interface IMod {
}
```

</details>

## 2. Formatting

### 1a. Indentation and Spacing

- Use 4 spaces for each level of indentation.
- Place spaces around operators.

<details>
<summary>Example</summary>

```java
int add = a + b;
```

</details>

### 2b. Braces

- Use [Java K&R](https://en.wikipedia.org/wiki/Indentation_style#Java) style for braces.

<details>
<summary>Example</summary>

```java
public Object createObject() {
    return null;
}
```

</details>

## 3. Documentation and Comments

### 1a. Comments

- Write in clear and concise English only.
- Use to explain important decisions, complex algorithms or to provide context.

### 2b. Documentation

- Use to document API using [Javadocs](https://en.wikipedia.org/wiki/Javadoc).
- Include information about parameters, return values, and exceptions.
- Write in clear and concise English only.

## 4. Error Handling and Crashes

### 1a. Error Handling

- Always handle exceptions.
- Provide clear information of what is happening.
- Use the LoggingAPI to log the error correctly.

### 2b. Crashes

- Always use the CrashAPI.
- Include concise information of what caused the crash for further investigation.

## 6. Version Control

- todo

# Conclusion
Adherence to this coding standard is essential for your code to be implemented in CPML (Cross Platform Mod Loader). Failure to comply may result in exclusion.
However, should you adhere to the coding standard, your code will undergo retesting. If it passes the tests and meets the criteria, it will be considered for inclusion.
Moreover, following this coding standard will significantly enhance the consistency, readability, and maintainability of CPML (Cross Platform Mod Loader).
