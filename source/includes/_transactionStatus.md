# Transactions

## Transaction Callback

> **POST** https://example.com/transactions

```json
{
  "card_id": "",
  "date_time": "",
  "merchant_name": "",
  "merchant_city": "",
  "merchant_id": "",
  "merchant_country": "",
  "mcc": "",
  "amount": "",
  "currency": "",
  "response_code": "",
  "external_id": ""
}
```

After we process a transaction, we can make a callback call to an API provided by you. It works pretty much in real time and it will have all the transaction data you may need to make financial reconciliation on your end.

It will always be a POST call with the same payload, you may also provide a key that will be sent in the Authorization header.

## Transaction Status

When checking for transactions, you will receive a `response_code`, this are all the possible responses you will get. The most common ones are:

#### 0 Approved

Successfull transaction. You don't need to do anything.

#### 51 Insufficient Funds

You have ran out of funds or credit for this transactions to get approved. You could check the admin dashboard for more information, add more funds to your wallet or make a payment to retrieve more credit back.

#### 63 Security Violation on Credit Card or Machine

The merchant tried to transaction with the wrong CVV code. You could ask the merchant to retry with the right code a second time.

#### 125 Blocked Card

The card is current inactive per your activation configuration. You could either ask the merchant to retry at a different date or activate the card in the API ou admin dashboard.

#### 190 Card not found - expiry date mismatch

The transaction failed because the wrong expiration date was provided. You should ask the merchant to retry with the correct information.

<details>
  <summary>All Codes</summary>

  <table>
    <thead>
      <td> Code </td><td> Status Description </td>
    </thead>
    <tr><td> 0 </td><td> Approved </td></tr>
    <tr><td> 1 </td><td> Refer to Issuer </td></tr>
    <tr><td> 2 </td><td> Refer to Issuer (Special Condition) </td></tr>
    <tr><td> 3 </td><td> Invalid Merchant </td></tr>
    <tr><td> 4 </td><td> Pickup Card </td></tr>
    <tr><td> 5 </td><td> Declined </td></tr>
    <tr><td> 6 </td><td> Error </td></tr>
    <tr><td> 7 </td><td> Pickup Card Special Condition </td></tr>
    <tr><td> 8 </td><td> Approved Honour with ID </td></tr>
    <tr><td> 9 </td><td> Request in Progress </td></tr>
    <tr><td> 10 </td><td> Partially approved </td></tr>
    <tr><td> 11 </td><td> Approved VIP Approval </td></tr>
    <tr><td> 12 </td><td> Invalid transaction </td></tr>
    <tr><td> 13 </td><td> Invalid Amount </td></tr>
    <tr><td> 14 </td><td> Invalid account number </td></tr>
    <tr><td> 15 </td><td> Unknown issuer </td></tr>
    <tr><td> 16 </td><td> Approved Update Track 3 </td></tr>
    <tr><td> 17 </td><td> Customer Cancellation </td></tr>
    <tr><td> 18 </td><td> Customer Dispute </td></tr>
    <tr><td> 19 </td><td> Re-enter Transaction </td></tr>
    <tr><td> 20 </td><td> Invalid Response </td></tr>
    <tr><td> 21 </td><td> No Action Taken </td></tr>
    <tr><td> 22 </td><td> Suspected Malfunction </td></tr>
    <tr><td> 23 </td><td> Unacceptable Transaction Fee </td></tr>
    <tr><td> 24 </td><td> File Update Unsupported </td></tr>
    <tr><td> 25 </td><td> Account Number Missing </td></tr>
    <tr><td> 26 </td><td> Duplicate File Update Replaced </td></tr>
    <tr><td> 27 </td><td> File Update Edit Error </td></tr>
    <tr><td> 28 </td><td> File Temporarily Unavailable </td></tr>
    <tr><td> 29 </td><td> File Update Failed </td></tr>
    <tr><td> 30 </td><td> Format error </td></tr>
    <tr><td> 31 </td><td> Bank Unsupported </td></tr>
    <tr><td> 32 </td><td> Completed Partially </td></tr>
    <tr><td> 33 </td><td> Expired Card Pickup </td></tr>
    <tr><td> 34 </td><td> Suspected Fraud Pickup </td></tr>
    <tr><td> 35 </td><td> Contact Acquirer Pickup </td></tr>
    <tr><td> 36 </td><td> Restricted Card Pickup </td></tr>
    <tr><td> 37 </td><td> Call Acquirer Security Pickup </td></tr>
    <tr><td> 38 </td><td> PIN Retries Exceeded Capture </td></tr>
    <tr><td> 39 </td><td> No Credit Account </td></tr>
    <tr><td> 40 </td><td> Function Unsupported </td></tr>
    <tr><td> 41 </td><td> Lost card </td></tr>
    <tr><td> 42 </td><td> No Unsupported Account </td></tr>
    <tr><td> 43 </td><td> Stolen card </td></tr>
    <tr><td> 44 </td><td> No Investment Account </td></tr>
    <tr><td> 51 </td><td> Insufficient funds </td></tr>
    <tr><td> 52 </td><td> No account of type requested </td></tr>
    <tr><td> 53 </td><td> No Savings Account </td></tr>
    <tr><td> 54 </td><td> Expired card </td></tr>
    <tr><td> 55 </td><td> Incorrect PIN </td></tr>
    <tr><td> 56 </td><td> Card Record Not Found </td></tr>
    <tr><td> 57 </td><td> Transaction not permitted to cardholder </td></tr>
    <tr><td> 58 </td><td> Transaction not permitted at terminal </td></tr>
    <tr><td> 59 </td><td> Suspected Fraud </td></tr>
    <tr><td> 60 </td><td> Contact Acquirer </td></tr>
    <tr><td> 61 </td><td> Limit Exceeded </td></tr>
    <tr><td> 62 </td><td> Restricted card </td></tr>
    <tr><td> 63 </td><td> Security Violation </td></tr>
    <tr><td> 64 </td><td> Original Amount Incorrect </td></tr>
    <tr><td> 65 </td><td> Frequency Exceeded </td></tr>
    <tr><td> 66 </td><td> Call Acquirer </td></tr>
    <tr><td> 67 </td><td> ATM Card Capture </td></tr>
    <tr><td> 68 </td><td> Response Too Late </td></tr>
    <tr><td> 70 </td><td> Contact Card Issuer </td></tr>
    <tr><td> 75 </td><td> PIN tries exceeded </td></tr>
    <tr><td> 76 </td><td> Unable to locate previous message </td></tr>
    <tr><td> 77 </td><td> Previous message inconsistent </td></tr>
    <tr><td> 78 </td><td> Card not unblocked </td></tr>
    <tr><td> 79 </td><td> Key ex. validation failed </td></tr>
    <tr><td> 80 </td><td> Credit Issuer Unavailable </td></tr>
    <tr><td> 81 </td><td> PIN Crypto Error </td></tr>
    <tr><td> 82 </td><td> CVV Check Failed </td></tr>
    <tr><td> 83 </td><td> PIN Not Verified </td></tr>
    <tr><td> 85 </td><td> Data Check Approved </td></tr>
    <tr><td> 86 </td><td> PIN Validation Not Possible </td></tr>
    <tr><td> 87 </td><td> Approved Purchase Only (No Cashback) </td></tr>
    <tr><td> 88 </td><td> Cryptography Error </td></tr>
    <tr><td> 90 </td><td> Cutoff in progress </td></tr>
    <tr><td> 91 </td><td> Issuer not available </td></tr>
    <tr><td> 92 </td><td> No Route Available </td></tr>
    <tr><td> 93 </td><td> Txn Cannot Complete - Violation of Law </td></tr>
    <tr><td> 94 </td><td> Duplicate Txn </td></tr>
    <tr><td> 95 </td><td> Reconciliation Error </td></tr>
    <tr><td> 96 </td><td> System Error </td></tr>
    <tr><td> 97 </td><td> Invalid MAC </td></tr>
    <tr><td> 98 </td><td> Issuer Timed Out </td></tr>
    <tr><td> 100 </td><td> Inline Device Failure </td></tr>
    <tr><td> 101 </td><td> Invalid PIN Block </td></tr>
    <tr><td> 104 </td><td> Configuration Error </td></tr>
    <tr><td> 105 </td><td> Transaction Content Invalid </td></tr>
    <tr><td> 106 </td><td> Undefined Transaction Purpose </td></tr>
    <tr><td> 107 </td><td> Undefined Transaction Purpose </td></tr>
    <tr><td> 108 </td><td> Invalid Key Version </td></tr>
    <tr><td> 109 </td><td> Invalid Key Generation </td></tr>
    <tr><td> 110 </td><td> Database Error </td></tr>
    <tr><td> 111 </td><td> Invalid Track 1 </td></tr>
    <tr><td> 112 </td><td> Invalid Track 2 </td></tr>
    <tr><td> 113 </td><td> Invalid Track 3 </td></tr>
    <tr><td> 114 </td><td> Invalid Terminal </td></tr>
    <tr><td> 115 </td><td> Transaction Already Matched </td></tr>
    <tr><td> 116 </td><td> No Account Hierarchy </td></tr>
    <tr><td> 117 </td><td> Cannot Convert Currency </td></tr>
    <tr><td> 118 </td><td> Card Track Database Mismatch </td></tr>
    <tr><td> 119 </td><td> Resource Busy </td></tr>
    <tr><td> 120 </td><td> At PIN Retry Limit </td></tr>
    <tr><td> 121 </td><td> Product Restriction </td></tr>
    <tr><td> 122 </td><td> PIN Data Missing </td></tr>
    <tr><td> 123 </td><td> Security hsware error </td></tr>
    <tr><td> 124 </td><td> International Restriction </td></tr>
    <tr><td> 125 </td><td> Blocked Card </td></tr>
    <tr><td> 126 </td><td> Approved account by Issuer </td></tr>
    <tr><td> 127 </td><td> Partial approved account by Issuer </td></tr>
    <tr><td> 128 </td><td> Approved Update ICC </td></tr>
    <tr><td> 129 </td><td> Invalid Time </td></tr>
    <tr><td> 130 </td><td> Invalid Sequence Number </td></tr>
    <tr><td> 131 </td><td> PIN Not Active </td></tr>
    <tr><td> 132 </td><td> ATM Exception Without Reversal </td></tr>
    <tr><td> 133 </td><td> Service Unavailable </td></tr>
    <tr><td> 134 </td><td> Cashback Limit Exceeded </td></tr>
    <tr><td> 135 </td><td> Invalid CVV2 </td></tr>
    <tr><td> 136 </td><td> Invalid Billing Info </td></tr>
    <tr><td> 137 </td><td> PIN Change Declined </td></tr>
    <tr><td> 138 </td><td> Inline Device Failure </td></tr>
    <tr><td> 139 </td><td> Forward to Issuer </td></tr>
    <tr><td> 140 </td><td> Cannot Authenticate Card </td></tr>
    <tr><td> 141 </td><td> Incorrect Routing </td></tr>
    <tr><td> 142 </td><td> PIN Length Error </td></tr>
    <tr><td> 143 </td><td> PIN Key Sync Error </td></tr>
    <tr><td> 144 </td><td> Redemption Denied Loyalty </td></tr>
    <tr><td> 145 </td><td> Blocked Account </td></tr>
    <tr><td> 146 </td><td> RFID Transponder Blocked </td></tr>
    <tr><td> 147 </td><td> RFID Transponder Unknown </td></tr>
    <tr><td> 148 </td><td> RFID Illegal Response </td></tr>
    <tr><td> 149 </td><td> Reconciliation Error No Reattempts </td></tr>
    <tr><td> 150 </td><td> Issuer Inoperative </td></tr>
    <tr><td> 151 </td><td> Issuer Malfunction </td></tr>
    <tr><td> 152 </td><td> MAC Key Sync Error </td></tr>
    <tr><td> 153 </td><td> Crypto Decline No Capture </td></tr>
    <tr><td> 154 </td><td> Product Ceiling Exceeded </td></tr>
    <tr><td> 155 </td><td> Safeframe Error </td></tr>
    <tr><td> 156 </td><td> Unable to Store </td></tr>
    <tr><td> 157 </td><td> Invalid 'To' Account </td></tr>
    <tr><td> 158 </td><td> Invalid 'From' Account </td></tr>
    <tr><td> 159 </td><td> Invalid Account General </td></tr>
    <tr><td> 160 </td><td> Domestic Debit Transaction Not Allowed </td></tr>
    <tr><td> 161 </td><td> Invalid Auth Lifecycle </td></tr>
    <tr><td> 162 </td><td> Valid for Zero Amount Transactions </td></tr>
    <tr><td> 163 </td><td> CVV Validation Unavailable </td></tr>
    <tr><td> 164 </td><td> Invalid Surcharge </td></tr>
    <tr><td> 165 </td><td> Cannot authorise force STIP </td></tr>
    <tr><td> 166 </td><td> Cash service not available </td></tr>
    <tr><td> 167 </td><td> Unsafe PIN </td></tr>
    <tr><td> 168 </td><td> Stop Payment Order </td></tr>
    <tr><td> 169 </td><td> Revocation of authorisation </td></tr>
    <tr><td> 170 </td><td> Revocation of all authorisations </td></tr>
    <tr><td> 171 </td><td> Invalid CVV3 </td></tr>
    <tr><td> 172 </td><td> Invalid ATC </td></tr>
    <tr><td> 173 </td><td> Invalid ARQC </td></tr>
    <tr><td> 174 </td><td> CVV generation Failed </td></tr>
    <tr><td> 175 </td><td> Invalid CVV </td></tr>
    <tr><td> 176 </td><td> Invalid PIN Format </td></tr>
    <tr><td> 177 </td><td> Product price out of range </td></tr>
    <tr><td> 178 </td><td> Inconsistent PIN fields </td></tr>
    <tr><td> 179 </td><td> PIN translate failed </td></tr>
    <tr><td> 180 </td><td> PRV generation failed </td></tr>
    <tr><td> 181 </td><td> HSM unavailable </td></tr>
    <tr><td> 182 </td><td> Fraud decline </td></tr>
    <tr><td> 183 </td><td> Fraud referral </td></tr>
    <tr><td> 184 </td><td> Fraud blocked 24h </td></tr>
    <tr><td> 185 </td><td> Invalid product </td></tr>
    <tr><td> 186 </td><td> Approved amount changed </td></tr>
    <tr><td> 187 </td><td> Fraud blocked </td></tr>
    <tr><td> 188 </td><td> Invalid currency </td></tr>
    <tr><td> 189 </td><td> Invalid luhn </td></tr>
    <tr><td> 190 </td><td> Card not found - expiry date mismatch </td></tr>
    <tr><td> 191 </td><td> Card not found - track expiry mismatch </td></tr>
    <tr><td> 192 </td><td> Reversal expiry mismatch </td></tr>
    <tr><td> 193 </td><td> Parked transaction timed out </td></tr>
    <tr><td> 194 </td><td> Invalid fallback </td></tr>
    <tr><td> 195 </td><td> Contactless not allowed </td></tr>
    <tr><td> 196 </td><td> Original preauth not found </td></tr>
    <tr><td> 197 </td><td> Original preauth balance not found </td></tr>
    <tr><td> 198 </td><td> Original preauth expired </td></tr>
    <tr><td> 199 </td><td> EMV offline PIN data mismatch </td></tr>
    <tr><td> 200 </td><td> Hidden instrument type </td></tr>
    <tr><td> 201 </td><td> Key not available </td></tr>
    <tr><td> 202 </td><td> TVR CVM Failed </td></tr>
    <tr><td> 203 </td><td> TVR CVM Unknown </td></tr>
    <tr><td> 204 </td><td> TVR cannot provide PIN </td></tr>
    <tr><td> 205 </td><td> TVR PIN required but not given </td></tr>
    <tr><td> 206 </td><td> Token wallet profile configuration error </td></tr>
    <tr><td> 207 </td><td> Token to PAN failure </td></tr>
    <tr><td> 219 </td><td> Card digitization invalid </td></tr>
    <tr><td> 220 </td><td> Mobile not allowed </td></tr>
    <tr><td> 221 </td><td> Token invalid reference ID </td></tr>
    <tr><td> 222 </td><td> Token invalid res method </td></tr>
    <tr><td> 223 </td><td> Token invalid channel </td></tr>
    <tr><td> 224 </td><td> Token data unavailable </td></tr>
    <tr><td> 225 </td><td> Invalid TC </td></tr>
    <tr><td> 226 </td><td> Invalid AAC </td></tr>
    <tr><td> 229 </td><td> Unknown CID AC type </td></tr>
    <tr><td> 230 </td><td> AC type mismatch </td></tr>
    <tr><td> 231 </td><td> Exceeded ECommerce limit </td></tr>
    <tr><td> 232 </td><td> Unable to build keyholder </td></tr>
    <tr><td> 233 </td><td> Token expired </td></tr>
    <tr><td> 234 </td><td> Token device score </td></tr>
    <tr><td> 235 </td><td> Token account score </td></tr>
    <tr><td> 236 </td><td> Original preauth reversed </td></tr>
    <tr><td> 237 </td><td> Delivery blocked </td></tr>
    <tr><td> 238 </td><td> Token invalid value </td></tr>
    <tr><td> 239 </td><td> Token data conflict </td></tr>
    <tr><td> 240 </td><td> Invalid original credit </td></tr>
    <tr><td> 241 </td><td> Invalid account funding </td></tr>
    <tr><td> 243 </td><td> Fraud full block 24h </td></tr>
    <tr><td> 244 </td><td> Fraud full block </td></tr>
    <tr><td> 245 </td><td> Invalid service code </td></tr>
    <tr><td> 246 </td><td> No service code present </td></tr>
    <tr><td> 247 </td><td> Duplicate ATC </td></tr>
    <tr><td> 248 </td><td> ATC exceeds lower </td></tr>
    <tr><td> 249 </td><td> ATC exceeds higher </td></tr>
    <tr><td> 250 </td><td> Not signed on </td></tr>
    <tr><td> 251 </td><td> Incorrect CVV length </td></tr>
    <tr><td> 252 </td><td> Approved unspecified </td></tr>
    <tr><td> 253 </td><td> Invalid PIN block content </td></tr>
    <tr><td> 254 </td><td> Cash Limit Exceeded </td></tr>
    <tr><td> 255 </td><td> Wrongly Keyed Expiry </td></tr>
    <tr><td> 256 </td><td> PIN Change Not Allowed </td></tr>
    <tr><td> 257 </td><td> Peripheral Down Req. STIP </td></tr>
    <tr><td> 258 </td><td> Invalid Token State </td></tr>
    <tr><td> 259 </td><td> Customer not found </td></tr>
    <tr><td> 260 </td><td> Invalid MCC </td></tr>
    <tr><td> 261 </td><td> Unsupported Issuer Service </td></tr>
    <tr><td> 262 </td><td> Sanction OI Merchant Block </td></tr>
    <tr><td> 263 </td><td> Sanction OI Country Block </td></tr>
    <tr><td> 264 </td><td> Sanction Score Threshold Exceeded </td></tr>
    <tr><td> 265 </td><td> PIN Data Required </td></tr>
    <tr><td> 266 </td><td> OCT Daily Activity Limit Exceeded </td></tr>
    <tr><td> 267 </td><td> OCT Weekly Activity Limit Exceeded </td></tr>
    <tr><td> 268 </td><td> OCT 30 Day Activity Limit Exceeded </td></tr>
    <tr><td> 269 </td><td> No Matching Balance Rule </td></tr>
    <tr><td> 270 </td><td> Inactive Card </td></tr>
    <tr><td> 271 </td><td> Inactive Account </td></tr>
    <tr><td> 272 </td><td> Delinquent (30 Days) </td></tr>
    <tr><td> 273 </td><td> Delinquent (90 Days) </td></tr>
    <tr><td> 274 </td><td> Blocked Customer </td></tr>
    <tr><td> 275 </td><td> Inactive Customer </td></tr>
    <tr><td> 276 </td><td> Closed Customer </td></tr>
    <tr><td> 380 </td><td> Approved: At an unspecified time and date within the PSD Guidelines. </td></tr>
    <tr><td> 381 </td><td> Approved: On the same day </td></tr>
    <tr><td> 382 </td><td> Approved: On the next calendar day </td></tr>
    <tr><td> 383 </td><td> Approved: On the next Working Day </td></tr>
    <tr><td> 384 </td><td> Approved: After the next Working Day within the PSD Guidelines </td></tr>
    <tr><td> 400 </td><td> Approved Offline </td></tr>
    </tr>
  </table>

</details>
