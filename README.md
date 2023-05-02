## HTML 2 Slack mrkdwn
Convert HTML into [Slack mrkdwn](https://api.slack.com/reference/surfaces/formatting) with Java.

### Build with Gradle

* gradle wrapper
* export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_181.jdk/Contents/Home
* ./gradlew tasks --all
* ./gradlew clean assemble
* ls build/libs/html2mrkdwn-1.0.1.jar

### Build and Distribution with Maven

* export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_181.jdk/Contents/Home
* Install gpg or gpg2 according to https://mikeross.xyz/gpg-without-gpgtools-on-mac/ and set gpg.executable inside ~/.m2/settings.xml
* export GPG_TTY=$(tty)
* Make sure that the pom file contains the maven-gpg-plugin plugin according to https://central.sonatype.org/publish/publish-maven/#gpg-signed-components
* Make sure that the pom file contains the distributionManagement section according to https://central.sonatype.org/publish/publish-maven/#distribution-management-and-authentication
* Make sure that the pom file contains the required meta information according to https://central.sonatype.org/publish/requirements/#sufficient-metadata
* mvn clean install (Use gpg.passphrase from ~/.m2/settings.xml)
* ls target/html2mrkdwn-1.0.1.jar
* mvn clean deploy (Use gpg.passphrase from ~/.m2/settings.xml)
* https://s01.oss.sonatype.org/#stagingRepositories (https://central.sonatype.org/publish/release/#locate-and-examine-your-staging-repository)
* https://s01.oss.sonatype.org/content/groups/public/org/wyona/html2mrkdwn/html2mrkdwn/
* https://repo1.maven.org/maven2/org/wyona/html2mrkdwn/html2mrkdwn/ (available typically within 30 minutes)

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

import org.wyona.html2mrkdwn.CopyDown;

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
import org.wyona.html2mrkdwn.CopyDown;
import org.wyona.html2mrkdwn.Options;
import org.wyona.html2mrkdwn.OptionsBuilder;

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
