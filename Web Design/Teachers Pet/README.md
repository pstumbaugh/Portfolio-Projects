This web application is split into two sections:

\*Note - The web app is on the OSU server and requires the OSU VPN access to view website and use microservice. Please view example pictures below to see final output. Also, this project was meant as practice in microservice architecture and back-end work, thus the front-end of the website is a fairly simple design.

1. Web app home page:
   This web app is designed to give teachers suggestions for topics their students can research all based around
   one central theme (or keyword). The user enters the keyword, follows the instructions, and results will be
   printed on the results page.

2. Thumbnail microservice:
   This service was part of team project that other members are using. It is not implemented within this Teacher's Pet project.

    This service takes in an incoming image (URL or image type) as a message (through the "PatQueue" queue) through RabbitMQ.
    It then transforms it into a thumbnail size (200x200) and sends the new image (saved as "thumbnail.jpg") as a message
    back through RabbitMQ (in the "thumbnailTransformer" exchange).

    HOW THE SERVICE WORKS:
    (service is in the "SERVICE" folder in this repo)

    1. Once started, the service is always watching "PatQueue" for new messages
    2. Once a message is received from that queue, it is processed (transformed into a thumbnail, if possible)
       _- If the message is a URL or acceptable picture type, the message will be transformed to a thumbnail
       _- If the message is not transformable via the service, a generic (leopard picture) will be used in it's place
    3. The new thumbnail will then be sent to the "thumbnailTransformer" exchange for pickup by a consumer.
    4. If you are the consumer as well (which is expeted in most cases), assert the "thumbnailTransformer" exchange and consume messages from there (in your own queue if needed)
       \*- see example of consuming from the exchange in the file named "receiveTest.js" (see below for startup instructions)

    STARTING THE SERVICE (and the test sending and receiving services too!):
    (Service will eventually be running forever on a flip server, but until then, feel free to follow the below instructions to test)

    1. Navigate into "SERVICE" folder
    2. run the thumbnail transofrmation service by entering in console: "node service.js"
       _- you may need to install node modules if needed
       _- The service will continue running until manually stopped. Please hit CTRL+C to stop service
       To Test the service, I have two js files to use:
    3. In the same "SERVICE" folder, enter on console: "node sendToQueue"
       _- This will send a message to the queue "PatQueue", which the service above is looking at for incoming messsages
       _- There are multiple other messages commented out. Please feel free to test with the other messages
    4. In the same "SERVICE" folder, enter on console: "node receiveTest.js"
       _- This will consume message from the service (where the messages have been sent to the exchange).
       _- When a message is received, you'll see it save your files as "NewUrlThumbnail.jpg"

Examples of Teacher's Pet:

Main screen:

![main screen](https://github.com/pstumbaugh/PORTFOLIO-Web-Development-HTML5-CSS-Node.js-JavaScript-C-Cpp-Flutter-Dart-Rust-Assembly-Language/blob/main/Web%20Design/Teachers%20Pet/EXAMPLE%20IMAGES/mainPage.png)

Loading Screen:

![loading](https://github.com/pstumbaugh/PORTFOLIO-Web-Development-HTML5-CSS-Node.js-JavaScript-C-Cpp-Flutter-Dart-Rust-Assembly-Language/blob/main/Web%20Design/Teachers%20Pet/EXAMPLE%20IMAGES/loading.png)

Results screen:

![results](https://github.com/pstumbaugh/PORTFOLIO-Web-Development-HTML5-CSS-Node.js-JavaScript-C-Cpp-Flutter-Dart-Rust-Assembly-Language/blob/main/Web%20Design/Teachers%20Pet/EXAMPLE%20IMAGES/exampleResults.png)
