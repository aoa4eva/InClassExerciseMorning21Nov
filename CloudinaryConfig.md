***Create a cloudinary configuration class called CloudinaryConfig:***

```
import com.cloudinary.Cloudinary;
import com.cloudinary.Singleton;
import com.cloudinary.Transformation;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

import java.io.IOException;
import java.util.Map;

@Component
public class CloudinaryConfig {
    private Cloudinary cloudinary;

    @Autowired
    public CloudinaryConfig(@Value("${cloudinary.apikey}") String key,
                            @Value("${cloudinary.apisecret}") String secret,
                            @Value("${cloudinary.cloudname}") String cloud)
    {
        cloudinary = Singleton.getCloudinary();
        cloudinary.config.cloudName=cloud ;
        cloudinary.config.apiSecret=secret;
        cloudinary.config.apiKey=key;
        System.out.println("Cloud name:"+cloud);


    }

    public Map upload(Object file, Map options)
    {
        try{
            return cloudinary.uploader().upload(file,options);
        }catch(IOException e)
        {
            e.printStackTrace();
            return null;
        }
    }

    public String createUrl(String name)
    {
        //This method generates the URL for the actor's list
        return cloudinary.url().transformation( new Transformation().width(100).height(100).crop("fill").radius(50).gravity("face")
        ).generate(name);

    }

    public String createUrl(String name, int width, int height)
    {
        //This method generates the URL for an image whose name is known and has been provided
        return cloudinary.url().transformation( new Transformation().width(width).height(height).crop("fill").radius(50).gravity("face")
        ).generate(name);

    }

    public String createSmallImage(String url, int width, int height)
    {
        //Creates a transformation from the URL provided
       return cloudinary.url().transformation(new Transformation().width(width).height(height).crop("fill").radius(50).gravity("face"))
                .type("fetch").generate(url);

    }
}
```

*** Update your application properties file.***
Make sure you comment out the code that you will not be using.
If you are not using the configuration settings AT ALL for the project, delete them.

```
# ===============================
# H2 Configuration
# ===============================
spring.datasource.url=jdbc:h2:mem:testdb
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
spring.jpa.hibernate.ddl-auto=create

# ===============================
# Thymeleaf configuration
# ===============================
spring.thymeleaf.mode=LEGACYHTML5
spring.thymeleaf.cache=false
# ===============================
# Cloudinary configuration
# ===============================
cloudinary.cloudname=
cloudinary.apisecret=
cloudinary.apikey=

# ===============================
# SERVER AND FILE CONFIGURATION
# ===============================
server.port=8086
spring.http.multipart.max-file-size=5MB
spring.http.multipart.max-request-size=5MB

# DO NOT PUSH YOUR CLOUDINARY CONFIGURATION TO GITHUB!!! #
```
