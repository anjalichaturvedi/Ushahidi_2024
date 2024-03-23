### Issue: https://github.com/ushahidi/platform/issues/4848#issue-2194357217
### Solution: https://gist.github.com/anjalichaturvedi/dd19eb4820406754e76b568b8c88e2c1
---

/*
# API Whatsapp
Description: 
Sending a WhatsApp message via the Infobip API is the selected functionality. With the Infobip messaging service, customers may now programmatically send messages to WhatsApp numbers.
Test-Case Situation:
Goal: To confirm that the Infobip API can be used by the system to send a WhatsApp message successfully.
1. The sender's WhatsApp number as an input.
2. WhatsApp number of the receiver.
3. Content of the message.
4. Infobip API permission token.
5. Infobip API endpoint URL.
Expected Results: 
1. The WhatsApp message was sent successfully.
2. A successful HTTP response status code (200).
Behavior: 
1. The test case will create a JSON payload including the sender and recipient numbers, message content, and the Infobip API authorization token, along with all the information required to send a WhatsApp message.
2. Using the created payload and permission headers, the test will send a POST request to the Infobip API endpoint.
3. The test anticipates receiving an HTTP response status code of 200, which denotes successful message delivery, after the message has been sent successfully.
Steps for the test: 
1. Gather the required inputs, such as the message content, the Infobip API authorization token, and the WhatsApp numbers of the sender and recipient.
2. Use the message data to create a JSON payload.
3. Send a POST request with the created payload and authorization headers to the Infobip API endpoint.
4. Confirm that the HTTP response status code is 200, which denotes a successful transmission of the message.
*/

describe('Sending WhatsApp Message using Infobip API', () => {
    it('Sends a WhatsApp message successfully', () => {
        const headers = {
            "Authorization": "App 2be149b19e5587eddc7937e017fd03a2-bc35d7ff-a2a6-4e6b-bd75-3307bfc971e1",
            "Content-Type": "application/json",
            "Accept": "application/json"
        };

        const raw = JSON.stringify({
            "messages": [{
                "from": "447860099299", 
                "to": "919711206358", 
                "messageId": "", 
                "content": {
                    "templateName": "message_test", 
                    "templateData": {
                        "body": {
                            "placeholders": ["Anjali"] 
                        }
                    }, 
                    "language": "en" 
                }
            }]
        });

        const requestOptions = {
            method: "POST",
            headers: headers, 
            body: raw,<img width="763" alt="Screenshot 2024-03-23 at 11 11 47 PM" src="https://github.com/anjalichaturvedi/Ushahidi_2024/assets/72503808/bb8428f7-332e-49a5-8114-42234093c614">

            redirect: "follow"
        };

        cy.request({
            method: requestOptions.method,
            url: "https://y3e6jj.api.infobip.com/whatsapp/1/message/template",
            headers: requestOptions.headers,
            body: requestOptions.body,
            failOnStatusCode: false 
        }).then(response => {
            expect(response.status).to.eq(200); 
        });
    });
});
<img width="874" alt="Screenshot 2024-03-23 at 11 10 57 PM" src="https://github.com/anjalichaturvedi/Ushahidi_2024/assets/72503808/898b7822-f04d-43e3-beea-60a028876843">
<img width="763" alt="Screenshot 2024-03-23 at 11 11 47 PM" src="https://github.com/anjalichaturvedi/Ushahidi_2024/assets/72503808/ce058275-86bc-4d67-877c-24d8457c0f4f">

