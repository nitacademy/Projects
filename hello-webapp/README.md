# Hello WebApp (Maven WAR)

A tiny Java web application you can build into a `.war` and deploy on Apache Tomcat.

## Build

```bash
cd hello-webapp
mvn -v                 # ensure Maven is installed
mvn clean package      # produces target/hello-webapp-1.0.0.war
```

## Deploy to Tomcat

Copy the WAR to Tomcat's `webapps/` directory and Tomcat will auto-deploy it.

```bash
# Example (adjust path to your Tomcat install):
cp target/hello-webapp-1.0.0.war /opt/tomcat/webapps/
# or deploy via the Tomcat Manager UI
```

Then visit:

- `http://<server>:<port>/hello-webapp-1.0.0/` (JSP index)
- `http://<server>:<port>/hello-webapp-1.0.0/hello` (Servlet)

> Tip: To have a stable context path like `/hello-webapp`, you can rename the WAR to `hello-webapp.war` before copying.

## Tomcat 10/11 (Jakarta) note

If you're on Tomcat 10+ you must switch from `javax.servlet` to `jakarta.servlet`:

1. In `pom.xml`, replace the `javax.servlet-api` dependency with:

```xml
<dependency>
  <groupId>jakarta.servlet</groupId>
  <artifactId>jakarta.servlet-api</artifactId>
  <version>5.0.0</version>
  <scope>provided</scope>
</dependency>
```

2. In `HelloServlet.java`, change imports from `javax.servlet.*` to `jakarta.servlet.*`.

## Java version

The `pom.xml` is set to compile with Java 17 (`<maven.compiler.release>17</maven.compiler.release>`). 
If you're on Java 21, you can change this to `21`.
