## HTML 2 Slack mrkdwn
Convert HTML into [Slack mrkdwn](https://api.slack.com/reference/surfaces/formatting) with Java.

### Build
gradle wrapper
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_181.jdk/Contents/Home
./gradlew tasks --all
./gradlew clean assemble
ls build/libs/html2mrkdwn-1.0.1.jar

### Installation
Gradle:
```gradle
dependencies {
    compile 'org.wyona.html2mrkdwn:html2mrkdwn:1.0.1'
}
```

Maven:
```xml
<dependencies>
    <dependency>
        <groupId>org.wyona.html2mrkdwn</groupId>
        <artifactId>html2mrkdwn</artifactId>
        <version>1.0.1</version>
    </dependency>
</dependencies>
```

### Usage

```java

import io.github.furstenheim.CopyDown;
public class Main {
    public static void main (String[] args) {
        CopyDown converter = new CopyDown();
        String myHtml = "<h1>Some title</h1><div>Some html<p>Another paragraph</p></div>";
        String markdown = converter.convert(myHtml);
        System.out.println(markdown);
        // Some title\n==========\n\nSome html\n\nAnother paragraph\n
    }
}
```

### Options

It is possible to use options for converting markdown:

```java
import io.github.furstenheim.CopyDown;
import io.github.furstenheim.Options;
import io.github.furstenheim.OptionsBuilder;

public class Main {
   public static void main (String[] args) {
       OptionsBuilder optionsBuilder = OptionsBuilder.anOptions();
       Options options = optionsBuilder
               .withBr("-")
               // more options
               .build();
       CopyDown converter = new CopyDown(options);
       String myHtml = "<h1>Some title</h1><div>Some html<p>Another paragraph</p></div>";
       String markdown = converter.convert(myHtml);
       System.out.println(markdown);
   }
}
```


| Option                | Valid values  | Default |
| :-------------------- | :------------ | :------ |
| `headingStyle`        | `SETEXT` or `ATX` | `SETEXT`  |
| `hr`                  | Any [Thematic break](http://spec.commonmark.org/0.27/#thematic-breaks) | `* * *` |
| `bulletListMarker`    | `-`, `+`, or `*` | `*` |
| `codeBlockStyle`      | `INDENTED` or `FENCED` | `INDENTED` |
| `fence`               | ` ``` ` or `~~~` | ` ``` ` |
| `emDelimiter`         | `_` or `*` | `_` |
| `strongDelimiter`     | `**` or `__` | `**` |
| `linkStyle`           | `INLINED` or `REFERENCED` | `INLINED` |
| `linkReferenceStyle`  | `FULL`, `COLLAPSED`, or `SHORTCUT` | `FULL` |


### Acknowledgment
This library is a fork of https://github.com/furstenheim/copy-down which is a port to Java of the wonderful library [Turndown.js](https://github.com/domchristie/turndown).

This project is supported by Intellij open source license
