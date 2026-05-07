<!-- markdownlint-disable MD013 -->

# Send & receive SMS messages with Twilio and Java

Learn how to send and receive SMS with Twilio and Rust with this repository.
In just a few lines of code, you can see your phone light up sending and receiving SMS with Twilio and Rust.

## Prerequisites

To run the app locally, you need the following:

- Java 21 or later
- [ngrok][ngrok] and a free ngrok account
- A [Twilio account][twilio_signup] with an active phone number that can send SMS
- Some command-line/terminal and [Spring][java_spring] experience would be helpful, but it's not necessary

## Quickstart

First things first, clone or download this repository.

### Send an SMS

Before you can send an SMS, you need to complete the following

1. Go to the [Twilio Console][twilio_console] and find your **Account SID**, **Auth Token**, and Twilio phone number.
1. Copy those values and set them as the values of `<TWILIO_ACCOUNT_SID>`, `<TWILIO_AUTH_TOKEN>`, and `<TWILIO_PHONE_NUMBER>`, respectively, in the command below.

   ```bash
   TWILIO_ACCOUNT_SID=<TWILIO_ACCOUNT_SID> TWILIO_AUTH_TOKEN=<TWILIO_AUTH_TOKEN> TWILIO_PHONE_NUMBER=<TWILIO_PHONE_NUMBER> \
        mvn spring-boot:run
   ```

1. Run the command above to start the Java Spring application.
1. Replace `<YOUR_PHONE_NUMBER>` in the command below with your phone number in [E.164 format][e164_format]

   ```bash
   curl --data-urlencode "recipient=<YOUR_PHONE_NUMBER>" http://localhost:8080/send
   ```

1. Run the command to send an SMS

### Receive an SMS

Before you can receive an SMS, you need to complete a few further steps.

1. Start your ngrok server:

   ```bash
   ngrok http 8080
   ```

1. Go to the [Active numbers][active_numbers] page in the Twilio Console.
1. Click your Twilio phone number.
1. Go to the **Configure** tab and find the **Messaging Configuration** section.
1. In the **A call comes in** row, select the **Webhook** option.
1. Paste your ngrok **Forwarding** URL in the **URL** field followed by "/receive/".
   For example, if your ngrok console shows Forwarding "<https://1aaa-123-45-678-910.ngrok-free.app>", enter "<https://1aaa-123-45-678-910.ngrok-free.app/receive/>".
   - To receive an SMS **without** responding to it, append "no-response" to the URL
   - To receive an SMS and respond to it, append "with-response" to the URL
1. Click **Save configuration**.
1. Start the Java Spring web app

   ```bash
   mvn spring-boot:run
   ```

1. With both the Java Spring app and ngrok running, send an SMS to your Twilio phone number, containing whatever message you like.
   If you want a response, try sending "never gonna" as the message.

[active_numbers]: https://console.twilio.com/us1/develop/phone-numbers/manage/incoming
[java_spring]: https://spring.io
[e164_format]: https://www.twilio.com/docs/glossary/what-e164
[ngrok]: https://ngrok.com/
[twilio_console]: https://console.twilio.com
[twilio_signup]: https://www.twilio.com/try-twilio

<!-- markdownlint-enable MD013 -->
