# Chapter 1
It's ok, no issue, and some useful explanations about why should you use hibernate over some custom libraries written in a hurry.

# Chapter 2
Here it sarts...

## 2.1.2
You obviously don't use Ant now, so it will be normal Maven project structure
And i'd prefer to have less problems because of versions so I worked with:
```
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>3.5.6-Final</version>
        </dependency>
```
//TODO check why dependencies for version 6 are not hibernate-core but hibernate-commons-annotations and some jakarta packages

***
In mapping file, because of this you most probably will see all mapping underlined with red
```
<?xml version="1.0"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD//EN"
"http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
```

Actually the issue is with the link `http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd` it probably won't work.
instead you can try `http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd`

***
in sub-chapter **Storing and loading objects**
You will see that no matter the imports you choose - `HibernateUtil` from the *Listing 2.3 The “Hello World” main application code* will stay red - Just continue reading! This class will be implemented by us and explained later in the book.


## 2.1.3
Same problem as with mapping file following link might not work
`<!DOCTYPE hibernate-configuration SYSTEM "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">`
So instead try
```
<?xml version="1.0"?>
<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN" "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
```
***
In **Handling the SessionFactory**

when we finally get to implementation of HibernateUtil you might see the red under ExceptionInInitializerError and the problem there can actually be the wrong spelling - so pay attention. 
```java
        }catch(Throwable ex) {
            throw new ExceptionInInitializerError(ex);
        }
```
In **Enabling logging and statistics**
initially inserted log4j2 dependencies
```
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-api</artifactId>
            <version>2.14.0</version>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>2.14.0</version>
        </dependency>
```
But got `SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".`
added dependency for slf4j adapter
```
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-slf4j-impl</artifactId>
            <version>2.14.0</version>
            <scope>compile</scope>
        </dependency>
```
than I had `SLF4J: The requested version 1.6 by your slf4j binding is not compatible with [1.5.5, 1.5.6, 1.5.7, 1.5.8]`
and it was solved with appropriate slf4j version
```
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.6.6</version>
        </dependency>
```
Then I've got `main ERROR Unable to locate appender "MAIN" for logger config "root"`
Cancelled "MAIN" appender from log4j config file

`Exception in thread "main" org.hibernate.MappingException: An AnnotationConfiguration instance is required to use <mapping class="com.hibernate.raw.Message"/>`



