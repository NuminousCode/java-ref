Setting up a **Spring Boot** application in **Visual Studio Code (VS Code)** using **Maven** is straightforward. Below is a step-by-step guide to create a bare-bones application that launches in your browser. This setup includes necessary VS Code extensions, Maven configuration, and basic Spring Boot code.

---

## **1. Install Necessary VS Code Extensions**

To enhance your development experience, install the following VS Code extensions:

1. **Java Extension Pack** by Microsoft
   - **Includes**: Language Support for Java™, Debugger for Java, Java Test Runner, Maven for Java, and more.
   - **Link**: [Java Extension Pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)

2. **Spring Boot Extension Pack** by Pivotal
   - **Includes**: Spring Boot support, Spring Initializr integration, Spring Boot Dashboard, and more.
   - **Link**: [Spring Boot Extension Pack](https://marketplace.visualstudio.com/items?itemName=Pivotal.vscode-spring-boot)

3. **Maven for Java** (if not included in Java Extension Pack)
   - **Link**: [Maven for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-maven)

4. **Debugger for Java** (if not included)
   - **Link**: [Debugger for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug)

*To install an extension:*
- Open VS Code.
- Go to the **Extensions** view by clicking the square icon on the sidebar or pressing `Ctrl+Shift+X`.
- Search for the extension name and click **Install**.

---

## **2. Create a New Spring Boot Project Using Spring Initializr**

You can use the **Spring Initializr** integrated into VS Code to generate the project structure.

1. **Open Command Palette**:
   - Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (macOS).

2. **Run Spring Initializr**:
   - Type `Spring Initializr: Generate a Maven Project` and select it.

3. **Configure Project Settings**:
   - **Group ID**: `com.example`
   - **Artifact ID**: `demo`
   - **Version**: `0.0.1-SNAPSHOT`
   - **Package Name**: `com.example.demo`
   - **Java Version**: Select your installed Java version (e.g., `17` or `11`)

4. **Select Dependencies**:
   - **Web**: `Spring Web`
   
   *(Optional: You can skip additional dependencies for a bare-bones setup.)*

5. **Choose Project Location**:
   - Select the folder where you want to create the project.

6. **Project Generation**:
   - VS Code will generate the project and open it in the workspace.

---

## **3. Explore the Project Structure**

Your project should have the following structure:

```
demo
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── example
│   │   │           └── demo
│   │   │               └── DemoApplication.java
│   │   └── resources
│   │       ├── application.properties
│   │       └── static
│   │           └── (optional static files)
│   └── test
│       └── java
│           └── com
│               └── example
│                   └── demo
│                       └── DemoApplicationTests.java
├── .gitignore
├── mvnw
├── mvnw.cmd
├── pom.xml
└── README.md
```

---

## **4. Add a Simple Controller**

Create a basic controller to handle HTTP requests and display a message in the browser.

1. **Create Controller Class**:
   - Navigate to `src/main/java/com/example/demo/`.
   - Create a new Java class named `HelloController.java`.

2. **Add the Following Code**:

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/")
    public String home() {
        return "Hello, Spring Boot!";
    }
}
```

*This controller maps the root URL (`"/"`) to a simple greeting message.*

---

## **5. Configure Application Properties (Optional)**

By default, Spring Boot runs on port `8080`. If you want to change the port or other settings, edit the `application.properties` file.

- **Location**: `src/main/resources/application.properties`
  
- **Example** (to change the server port to `8081`):

  ```properties
  server.port=8081
  ```

*This step is optional. You can skip it if you are fine with the default settings.*

---

## **6. Build the Project**

Ensure that your project is correctly built and all dependencies are resolved.

1. **Open Terminal in VS Code**:
   - Press ``Ctrl+` `` (Windows/Linux) or ``Cmd+` `` (macOS).

2. **Navigate to Project Directory** (if not already there):
   ```bash
   cd path/to/your/project/demo
   ```

3. **Build with Maven**:
   ```bash
   mvn clean install
   ```

*This command compiles the project, runs tests, and packages the application.*

---

## **7. Run the Spring Boot Application**

You can run the application directly from VS Code or using the terminal.

### **Option 1: Using VS Code Run and Debug**

1. **Open the Main Application Class**:
   - Open `DemoApplication.java` located at `src/main/java/com/example/demo/`.

2. **Run the Application**:
   - You should see a **Run** or **Debug** button above the `main` method.
   - Click **Run** ▶️ to start the application.

### **Option 2: Using Terminal**

1. **Ensure You're in the Project Directory**:
   ```bash
   cd path/to/your/project/demo
   ```

2. **Run the Application with Maven**:
   ```bash
   mvn spring-boot:run
   ```

*The application will start, and you should see logs indicating it's running.*

---

## **8. Access the Application in Your Browser**

1. **Open Your Web Browser**.

2. **Navigate to**:
   - If you didn't change the port:
     ```
     http://localhost:8080/
     ```
   - If you changed the port to `8081` (or another):
     ```
     http://localhost:8081/
     ```

3. **You Should See**:
   ```
   Hello, Spring Boot!
   ```

*This confirms that your Spring Boot application is running successfully.*

---

## **9. Additional Tips**

- **Hot Reload with Spring Boot DevTools**:
  - To enable automatic restarts on code changes, add the `spring-boot-devtools` dependency.
  
  ```xml
  <!-- Add inside <dependencies> in pom.xml -->
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <optional>true</optional>
  </dependency>
  ```
  
  - **Note**: This is optional and primarily used during development.

- **Using VS Code's Spring Boot Dashboard**:
  - The **Spring Boot Dashboard** extension provides a visual interface to manage your Spring Boot applications.
  - Access it from the **Explorer** sidebar after installing the **Spring Boot Extension Pack**.

- **Debugging**:
  - You can set breakpoints in your code and use VS Code’s debugging tools to troubleshoot.

---

## **Complete `pom.xml` Example**

Ensure your `pom.xml` has the necessary dependencies. Below is a minimal example:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>demo</name>
    <description>Demo project for Spring Boot</description>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.1.2</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <properties>
        <java.version>17</java.version>
    </properties>
    <dependencies>
        <!-- Spring Web Starter -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <!-- Optional: Spring Boot DevTools for hot reload -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
        </dependency>

        <!-- Optional: Testing dependencies -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <!-- Spring Boot Maven Plugin -->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>3.1.2</version>
            </plugin>
        </plugins>
    </build>
</project>
```

*Ensure the Spring Boot version and Java version match your setup.*

---

## **Conclusion**

You've successfully set up a bare-bones Spring Boot application using Maven in VS Code. This setup provides a solid foundation to build more complex applications. Explore additional Spring Boot features, integrate databases, and enhance your application as needed.

If you encounter any issues, consider consulting the [Spring Boot Documentation](https://spring.io/projects/spring-boot) or the [VS Code Java Documentation](https://code.visualstudio.com/docs/languages/java).

Happy coding!