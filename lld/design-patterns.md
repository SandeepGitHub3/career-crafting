# Design Patterns Notes

---

## Index
1. [Creational Patterns](#1-creational-patterns)
2. [Structural Patterns](#2-structural-patterns)
   - [2.1 Adapter](#21-adapter)
   - [2.2 Decorator](#22-decorator)
   - [2.3 Bridge](#23-bridge)
   - [2.4 Composite](#24-composite)
   - [2.5 Facade](#25-facade)
   - [2.6 Flyweight](#26-flyweight)
   - [2.7 Proxy](#27-proxy)
3. [Behavioral Patterns](#3-behavioral-patterns)
## 1. Creational Patterns
*(To be filled later)*

---

## 2. Structural Patterns

### 2.1 Adapter
**Intent:** Convert one interface into another expected by the client.  
**Problem it Solves:** Integrating incompatible classes or legacy code into a new system without modifying existing code.

<img width="655" height="426" alt="image" src="https://github.com/user-attachments/assets/654f7a0e-b7c3-46ca-8d54-a0b2cb47835b" />

**Java Example:**
```java
interface MediaPlayer {
    void play(String audioType, String fileName);
}

class MP3Player implements MediaPlayer {
    public void play(String audioType, String fileName) {
        System.out.println("Playing MP3 file: " + fileName);
    }
}

class MP4Player {
    void playMP4(String fileName) {
        System.out.println("Playing MP4 file: " + fileName);
    }
}

class MediaAdapter implements MediaPlayer {
    private MP4Player mp4Player;

    MediaAdapter(MP4Player mp4Player) { this.mp4Player = mp4Player; }

    public void play(String audioType, String fileName) {
        if(audioType.equalsIgnoreCase("mp4")) {
            mp4Player.playMP4(fileName);
        }
    }
}

// Usage
MediaPlayer player = new MediaAdapter(new MP4Player());
player.play("mp4", "video.mp4");
```
**Backend Example:** Adapting a legacy CSV parser to a system expecting JSON input.  
**Real-life Java Example:** Using `java.util.Arrays#asList()` to adapt an array to a `List` interface.

---

### 2.2 Decorator
**Intent:** Dynamically add behavior or responsibilities to objects.  
**Problem it Solves:** Adding features to objects at runtime without creating multiple subclasses.

<img width="664" height="459" alt="image" src="https://github.com/user-attachments/assets/dd20b7f7-ab7e-4c4d-995d-0a678bc440e2" />

**Java Example:**
```java
interface Coffee { double cost(); }

class SimpleCoffee implements Coffee {
    public double cost() { return 5; }
}

class MilkDecorator implements Coffee {
    private Coffee coffee;
    MilkDecorator(Coffee coffee) { this.coffee = coffee; }
    public double cost() { return coffee.cost() + 2; }
}

// Usage
Coffee coffee = new MilkDecorator(new SimpleCoffee());
System.out.println(coffee.cost()); // 7
```
**Backend Example:** Wrapping a notification service to add logging or retry.  
**Real-life Java Example:** `java.io.BufferedReader` decorating a `FileReader` to add buffering.

---

### 2.3 Bridge
**Intent:** Decouple abstraction from implementation to allow independent variation.  
**Problem it Solves:** Avoiding class explosion when multiple dimensions of variation exist.

<img width="631" height="414" alt="image" src="https://github.com/user-attachments/assets/3923576d-5f0c-49ab-b45b-323c275b15ec" />

**Java Example:**
```java
interface Color { String fill(); }
class Red implements Color { public String fill() { return "red"; } }
class Blue implements Color { public String fill() { return "blue"; } }

abstract class Shape {
    protected Color color;
    Shape(Color color) { this.color = color; }
    abstract void draw();
}
class Circle extends Shape {
    Circle(Color color) { super(color); }
    void draw() { System.out.println("Circle " + color.fill()); }
}
```
**Backend Example:** Notification abstraction with different delivery mechanisms.

**Real-life Java Example:** `java.sql.DriverManager` abstracts JDBC drivers for different databases.

---

### 2.4 Composite
**Intent:** Treat individual objects and object groups uniformly.  
**Problem it Solves:** Simplifies operations on hierarchies of objects, like tree structures.

<img width="660" height="415" alt="image" src="https://github.com/user-attachments/assets/b357badf-7449-475d-b3b7-b13a2d0819ab" />

**Java Example:**
```java
// Component
interface FileSystemComponent {
    void showDetails();
}

// Leaf
class File implements FileSystemComponent {
    private String name;
    File(String name) { this.name = name; }

    public void showDetails() {
        System.out.println("File: " + name);
    }
}

// Composite
class Directory implements FileSystemComponent {
    private String name;
    private List<FileSystemComponent> children = new ArrayList<>();

    Directory(String name) { this.name = name; }

    public void add(FileSystemComponent component) {
        children.add(component);
    }

    public void showDetails() {
        System.out.println("Directory: " + name);
        for (FileSystemComponent c : children) c.showDetails();
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        FileSystemComponent file1 = new File("resume.pdf");
        FileSystemComponent file2 = new File("photo.png");
        Directory folder = new Directory("Documents");
        folder.add(file1);
        folder.add(file2);

        folder.showDetails();
    }
}

```
**Backend Example:** Sending individual or grouped notifications to campaigns.

**Real-life Java Example:** `javax.swing.JComponent` hierarchy, where containers and leaf components share the same interface.

---

### 2.5 Facade
**Intent:** Provide a simplified interface to a complex subsystem.  
**Problem it Solves:** Hides complex subsystem logic and reduces coupling for clients.

<img width="629" height="426" alt="image" src="https://github.com/user-attachments/assets/edd10224-c958-479f-b5a0-8838afa98635" />

**Java Example:**
```java
class EmailService { void sendEmail(String to, String msg) {} }
class SMSService { void sendSMS(String to, String msg) {} }
class PushService { void sendPush(String to, String msg) {} }

class NotificationFacade {
    private EmailService email = new EmailService();
    private SMSService sms = new SMSService();
    private PushService push = new PushService();
    void sendAll(String to, String msg) {
        email.sendEmail(to, msg);
        sms.sendSMS(to, msg);
        push.sendPush(to, msg);
    }
}
```
**Backend Example:** Unified API endpoint to send all types of notifications.

**Real-life Java Example:** `javax.faces.context.FacesContext` provides a single interface for multiple JSF APIs.

---

### 2.6 Flyweight
**Intent:** Reduce memory use by sharing immutable data among similar objects.  
**Problem it Solves:** Avoids memory bloat when many similar objects exist.

<img width="651" height="395" alt="image" src="https://github.com/user-attachments/assets/eb1cbdd9-6b53-4f33-b8da-e24dd4549bcd" />

**Java Example:**
```java
// Flyweight
class NotificationTemplate {
    private final String type;
    private final String content;

    NotificationTemplate(String type, String content) {
        this.type = type;
        this.content = content;
    }

    void send(String recipient, String data) {
        System.out.println("To: " + recipient + " | " + content.replace("{data}", data));
    }
}

// Flyweight Factory
class TemplateFactory {
    private static final Map<String, NotificationTemplate> cache = new HashMap<>();

    static NotificationTemplate getTemplate(String type) {
        if (!cache.containsKey(type)) {
            switch (type) {
                case "WELCOME":
                    cache.put(type, new NotificationTemplate("WELCOME", "Welcome {data}!"));
                    break;
                case "ALERT":
                    cache.put(type, new NotificationTemplate("ALERT", "Alert: {data}"));
                    break;
            }
        }
        return cache.get(type);
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        NotificationTemplate t1 = TemplateFactory.getTemplate("WELCOME");
        t1.send("UserA", "to the app");

        NotificationTemplate t2 = TemplateFactory.getTemplate("WELCOME");
        System.out.println(t1 == t2);  // true → reused same object
    }
}
```
**Backend Example:** Sharing notification templates across users.

**Real-life Java Example:** `java.lang.Integer.valueOf()` caches frequently used Integer objects.

---

### 2.7 Proxy
**Intent:** Control access to another object via a surrogate.  
**Problem it Solves:** Adds access control, caching, or lazy initialization for expensive or sensitive objects.
  
**Java Example:**
```java
interface Service {
    void request();
}

// Real Subject
class RealService implements Service {
    public void request() {
        System.out.println("Executing real service...");
    }
}

// Proxy
class ServiceProxy implements Service {
    private RealService realService;
    private String userRole;

    ServiceProxy(String userRole) {
        this.userRole = userRole;
    }

    public void request() {
        if (userRole.equals("ADMIN")) {
            if (realService == null)
                realService = new RealService();
            realService.request();
        } else {
            System.out.println("Access denied. Only ADMIN can perform this action.");
        }
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Service adminProxy = new ServiceProxy("ADMIN");
        adminProxy.request();

        Service userProxy = new ServiceProxy("USER");
        userProxy.request();
    }
}
```
**Backend Example:** Controlling API access, caching, or lazy loading of services.

**Real-life Java Example:** `java.lang.reflect.Proxy` to create dynamic proxy instances for interfaces.

---

## 3. Behavioral Patterns
*(To be filled later)*

