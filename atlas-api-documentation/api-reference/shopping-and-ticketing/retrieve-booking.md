# Retrieve Booking

### Dependency

`Order` function should be called in prior to this call.

### Endpoint {% debug uid="queryOrderDetails_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/queryOrderDetails.do](https://sandbox.atriptech.com/queryOrderDetails.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "XXXXXXXX",
    "orderNo": "ZNMKU20220119160129691"
}             
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    0: success

    2: System error
*   **msg **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Error message
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number
*   **orderStatus **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    0: Unpaid

    1: Ticketing-in-Process

    2: Ticketed
    
    \-3: Cancelled(When the booking is failed due to the request information)
*   **ticketErrorCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    It's only available when orderStatus = -3.&#x20;

    Please check the definition of ticketErrorCode [**here**](../overview/errors.md#ticket-error-codes)****
*   **ticketErrorMessage **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    It's only available when orderStatus = -3.&#x20;

    Error message
*   **totalPrice **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Total fare of this order in the currency TheAtlas settled with you.
*   **totalTransactionFee **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Total technical fees for this order in the currency TheAtlas settled with you.
*   **currency **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The currency TheAtlas settled with you.
*   **vendorTotalPrice **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Total fare of this order in the vendor's currency, reference for you to generate the specific credit card.
*   **vendorTotalAncillaryPrice **<mark style="color:blue;">**decimal**</mark>** 

    Total ancillary fare of this order in the vendor's currency.
*   **vendorCurrency **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Vendor's currency.
*   **supportPaymentMethod **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    1: Prepayment Only

    3: Both Credit Card Payment and Prepayment Available
*   **tktLimitTime **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Payment deadline for this order.
*   **paxTicketInfos Array<**[**PAXTicketInfo**](broken-reference/)**> **<mark style="color:green;">**Required**</mark>

    Ticket information for passengers, the same format as the PAXTicketInfo in order response.
*   **routing Object<**[**RouteElement**](broken-reference/)**> **<mark style="color:green;">**Required**</mark>

    Route and fare details. The structure is the same format as "Routing Element" in search response.
*   **airlineBookings Array<**[**ManageBookingElement**](broken-reference/)**> **<mark style="color:green;">**Required**</mark>

    Booking information for airline.    
    
{% endtab %}

{% tab title="Samples" %}
```
{
    "status": 0,
    "msg": "success",
    "orderNo": "ZNMKU20220119160129691",
    "orderStatus": "2",
    "paxTicketInfos": [
        {
            "name": "YAO/SAHA",
            "passengerType": 1,
            "birthday": "20140103",
            "gender": "M",
            "cardNum": "EJ19771700",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20300311",
            "nationality": "CN",
            "ticketNos": [
                "S10491"
            ],
            "airlinePNRs": [
                "S10491"
            ],
            "ancillaries": []
        },
        {
            "name": "SONG/YUN",
            "passengerType": 0,
            "birthday": "19921027",
            "gender": "M",
            "cardNum": "EC50717400",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20280308",
            "nationality": "CN",
            "ticketNos": [
                "S10491"
            ],
            "airlinePNRs": [
                "S10491"
            ],
            "ancillaries": []
        }
    ],
    "totalPrice": 37.90,
    "currency": "USD",
    "tktLimitTime": "2022-01-19 16:51:30",
    "vendorTotalPrice": 45000.00,
    "vendorTotalAncillaryPrice":3000,
    "vendorCurrency": "KRW",
    "adultTotalFare": 18.95,
    "childTotalFare": 18.95,
    "totalTransactionFee": 0,
    "supportPaymentMethod": 3,
    "routing": {
        "routingIdentifier": "Nvm0BG9VCGJRUPzvRCF2hU1okLJgXsVU46VwnmDdMe/JgpxanH/Xja3hYaj9X/EHLiR7QMsFKwl97AMIwqGNDbcG9kV3bXzylDL2dNM3c07PTcQ67WyTJvK9ITR1HmHC2t2K1gUJztkSI4hVwhMjOGZUlo8qqzhJ8N3Bzta2M87ijqfQHCXkoLAseTdGienIy33IOIIHB6aknLdpZrvz8tCOBxWuNSYc0Plc3dWtFJH1GEmT5TthTQ==",
        "supportCreditTransPayment": "0",
        "currency": "USD",
        "adultPrice": 10.02,
        "adultTax": 8.93,
        "childPrice": 10.02,
        "childTax": 8.93,
        "InfantPrice": 0,
        "InfantTax": 0,
        "transactionFeePerPax": 0,
        "nationalityType": 0,
        "nationality": "",
        "suitAge": "",
        "PaxType": "ADT",
        "fromSegments": [
            {
                "carrier": "7C",
                "flightNumber": "7C137",
                "depAirport": "GMP",
                "depTime": "202201251915",
                "arrAirport": "CJU",
                "arrTime": "202201252020",
                "stopCities": "",
                "duration": 65,
                "codeShare": false,
                "cabin": "",
                "cabinClass": 1,
                "seatCount": 4,
                "aircraftCode": "738",
                "depTerminal": "",
                "arrTerminal": "",
                "operatingCarrier": "",
                "operatingFlightnumber": ""
            }
        ],
        "retSegments": [],
        "combineIndexs": [],
        "rule": {
            "hasBaggage": 1,
            "baggageElements": [
                {
                    "segmentNo": 1,
                    "passengerType": 0,
                    "baggagePiece": 0,
                    "baggageWeight": 15
                }
            ],
            "refundRules": [
                {
                    "refundType": 0,
                    "refundStatus": "T",
                    "refundFee": 0.0,
                    "currency": "CNY",
                    "refNoshow": "T",
                    "refNoShowCondition": 48,
                    "refNoshowFee": 0.0
                }
            ],
            "changesRules": [
                {
                    "changesType": 0,
                    "changesStatus": "T",
                    "changesFee": 0.0,
                    "currency": "CNY",
                    "revNoshow": "T",
                    "revNoShowCondition": 48,
                    "revNoshowFee": 0.0,
                    "ruleList": []
                }
            ]
        },
        "ancillaryProductElements": [],
        "vendorFare": null,
        "bundleOptions": []
    },
    "airlineBookings":
        [
            {
                "airlineCode":"FR",
                "airlineName":"xxx",
                "airlinePnr":"xxx",
                "airlineWebSiteAddress":"xxx.com",
                "mmbEmail":"xxx@email.com",
                "tailDigitsOfPaymentCard:"xxxx",
                "extras":[{"name":"email","remark":"emailAddress","value":"xxx@sample.com"}]
            }
        ],
    "itineraryDownload": "https://sandbox.atriptech.com/itineraryDownload.do?orderNo=intP%2Biv7Jv70kjemGsbAJ10N%2F%2Bzwdpj%2F"
}
```
{% endtab %}
{% endtabs %}
