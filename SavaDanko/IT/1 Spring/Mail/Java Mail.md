---
tags:
  - review
sr-due: 2026-03-20
sr-interval: 80
sr-ease: 250
---
---
[Article](https://www.baeldung.com/spring-email)

---
###### **Dependencies**
```groovy
implementation("org.springframework.boot:spring-boot-starter-mail")
```

###### **Mail Server Properties**
The interfaces and classes for Java mail support in the Spring framework are organized as follows:
1. `MailSender interface`: the top-level interface that provides basic functionality for sending simple emails
2. `JavaMailSender interface`: the subinterface of the above `MailSender`. It supports MIME messages and is mostly used in conjunction with the `MimeMessageHelper` class for the creation of a `MimeMessage`. It’s recommended to use the `MimeMessagePreparator` mechanism with this interface.
3. `JavaMailSenderImpl class` provides an implementation of the `JavaMailSender` interface. It supports the `MimeMessage` and `SimpleMailMessage`.
4. `SimpleMailMessage class`: used to create a simple mail message including the from, to, cc, subject and text fields
5. `MimeMessagePreparator interface` provides a callback interface for the preparation of MIME messages.
6. `MimeMessageHelper class`: helper class for the creation of MIME messages. It offers support for images, typical mail attachments and text content in an HTML layout.

###### **Spring Boot Mail Server Properties**
```application.properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=<login user to smtp server>
spring.mail.password=<login password to smtp server>
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```
Some SMTP servers require a TLS connection, so we use the property `spring.mail.properties.mail.smtp.starttls.enable` to enable a TLS-protected connection.

Note that the password for our account should not be an ordinary password but an application password generated for our Google account. Follow this [link](https://support.google.com/accounts/answer/185833) to see the details and to generate your Google App Password.

###### **Sending Simple Emails**
```java
@Component
public class EmailServiceImpl implements EmailService {

    @Autowired
    private JavaMailSender emailSender;

    public void sendSimpleMessage(
      String to, String subject, String text) {
        ...
        SimpleMailMessage message = new SimpleMailMessage(); 
        message.setFrom("noreply@baeldung.com");
        message.setTo(to); 
        message.setSubject(subject); 
        message.setText(text);
        emailSender.send(message);
        ...
    }
}
```

###### **Sending Emails With Attachments**
```java
@Override
public void sendMessageWithAttachment(
  String to, String subject, String text, String pathToAttachment) {
    // ...
    
    MimeMessage message = emailSender.createMimeMessage();
     
    MimeMessageHelper helper = new MimeMessageHelper(message, true);
    
    helper.setFrom("noreply@baeldung.com");
    helper.setTo(to);
    helper.setSubject(subject);
    helper.setText(text);
        
    FileSystemResource file 
      = new FileSystemResource(new File(pathToAttachment));
    helper.addAttachment("Invoice", file);

    emailSender.send(message);
    // ...
}
```