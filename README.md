# captcha

## hCaptcha

>reference
>
>- https://hcaptcha.com/
>- https://docs.hcaptcha.com/

- site key

   92cf0e1c-5257-4729-b5be-2f401736e511

- verify token at server side

   ```bash
   curl https://hcaptcha.com/siteverify \
     -X POST \
     -d "response=<response_text>&secret=0xacc92A4f87Acb7eb951D6DCB006366536aB290e7"
   ```

- result

   ```json
   // success
   {
       "success": true,
       "challenge_ts": "2021-03-05T14:22:51",
       "hostname": "192.168.1.196",
       "credit": false
   }
   // failure
   {
       "success": false,
       "error-codes": [
           "invalid-or-already-seen-response"
       ]
   }
   ```

## google reCaptcha v3

[faq](https://developers.google.cn/recaptcha/docs/faq)
replace www.google.com with www.recaptcha.net

- site key

   6LcFwHcaAAAAAHCnoyXSy_w-xCaOsjkfvuqSl6J_

- verify token at server side

   reference https://developers.google.com/recaptcha/docs/verify

   ```bash
   curl https://www.google.com/recaptcha/api/siteverify \
     -X POST \
     -d "response=<response_text>&secret=6LcFwHcaAAAAAPdsqWdcZPatHCcXqFhLaKDekBPA"
   ```

   result

   ```json
   {
     "success": true,
     "challenge_ts": "2021-03-09T04:01:17Z",
     "hostname": "localhost",
     "score": 0.9,
     "action": "submit"
   }
   
   {
     "success": false,
     "error-codes": [
       "timeout-or-duplicate"
     ]
   }
   ```

## google reCaptcha v2

- site key

   ```text
   6Lc2y3caAAAAAJsjvipiWaspD5294F2LyCqqF2dG
   6Lej8XcaAAAAAOPHJC37FLTRnIITtjiF0CeyJUFT
   ```

- verify token at server side

   ```bash
   curl https://www.google.com/recaptcha/api/siteverify \
     -X POST \
     -d "response=<response_text>&secret=6Lc2y3caAAAAAPvAwGMyHAhh5G7KL10fsPjR3xt5"
   # 6Lej8XcaAAAAABshQdKUd2bzT2fXDdcs1bH8OrXF
   ```

- result

   ```json
   {
     "success": true,
     "challenge_ts": "2021-03-09T06:50:20Z",
     "hostname": "localhost"
   }
   
   {
     "success": false,
     "error-codes": [
       "timeout-or-duplicate"
     ]
   }
   ```

## request flow

### hCaptcha
![request-flow-hcaptcha](https://mermaid.ink/img/eyJjb2RlIjoic2VxdWVuY2VEaWFncmFtXG5wYXJ0aWNpcGFudCBVc2VyXG5wYXJ0aWNpcGFudCBZb3VyIFdlYnNpdGUgb3IgQXBwXG5wYXJ0aWNpcGFudCBoQ2FwdGNoYSBDbGllbnQgQVBJXG5wYXJ0aWNpcGFudCBZb3VyIFNlcnZlclxucGFydGljaXBhbnQgaENhcHRjaGEgU2l0ZXZlcmlmeVxuVXNlci0-PllvdXIgV2Vic2l0ZSBvciBBcHA6IExvYWQgV2Vic2l0ZSBvciBBcHBcbllvdXIgV2Vic2l0ZSBvciBBcHAtPj5Vc2VyOiBMb2FkIGhDYXB0Y2hhIEpTIG9yIFNES1xuVXNlci0-PmhDYXB0Y2hhIENsaWVudCBBUEk6IFBsZWFzZSBpc3N1ZSBwYXNzY29kZVxuaENhcHRjaGEgQ2xpZW50IEFQSS0-PlVzZXI6IFJldHVybnMgY2hhbGxlbmdlIG9yIHBhc3Njb2RlXG5oQ2FwdGNoYSBDbGllbnQgQVBJLT4-WW91ciBXZWJzaXRlIG9yIEFwcDogUGFzc2NvZGUgZW1iZWRkZWQgaW4gZm9ybSBvciByZXR1cm5lZCB2aWEgSlMvY2FsbGJhY2tcbllvdXIgV2Vic2l0ZSBvciBBcHAtPj5Zb3VyIFNlcnZlcjogRm9ybSBvciBYSFIgd2l0aCBoQ2FwdGNoYSBwYXNzY29kZVxuWW91ciBTZXJ2ZXItPj5oQ2FwdGNoYSBTaXRldmVyaWZ5OiBJcyB0aGlzIHBhc3Njb2RlIHZhbGlkP1xuaENhcHRjaGEgU2l0ZXZlcmlmeS0-PllvdXIgU2VydmVyOiBQYXNzY29kZSBpcyB2YWxpZCAoc3VjY2VzcyBpcyB0cnVlKVxuWW91ciBTZXJ2ZXItPj5Vc2VyOiBTZXNzaW9uIGF1dGhvcml6ZWQsIHByb2NlZWQiLCJtZXJtYWlkIjoie1xuICBcInRoZW1lXCI6IFwiZGVmYXVsdFwiXG59IiwidXBkYXRlRWRpdG9yIjp0cnVlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6dHJ1ZX0)

### reCaptcha

![request-flow-recaptcha](https://mermaid.ink/img/eyJjb2RlIjoiXG4lJXtpbml0OiB7J3NlY3VyaXR5TGV2ZWwnOiAnbG9vc2UnLCAndGhlbWUnOidkZWZhdWx0JywgICdzZXF1ZW5jZSc6IHsnc2hvd1NlcXVlbmNlTnVtYmVycyc6IGZhbHNlLCdtaXJyb3JBY3RvcnMnOnRydWV9fX0lJVxuc2VxdWVuY2VEaWFncmFtXG5wYXJ0aWNpcGFudCBVIGFzIFVzZXJcbnBhcnRpY2lwYW50IEIgYXMgVXNlckFnZW50PGJyLz5Ccm93c2VyXG5wYXJ0aWNpcGFudCBGIGFzIEZyb250ZW5kPGJyLz5VSVxucGFydGljaXBhbnQgQSBhcyBCYWNrZW5kPGJyLz5BcGlcbnBhcnRpY2lwYW50IEcgYXMgR29vZ2xlPGJyLz5yZUNhcHRjaGFcblxuVSAtPj4gQjogYWNjZXNzXG5CIC0-PiBGOiBsb2FkIHBhZ2VcbkYgLS0-PiBCOiBbcGFnZV1cbkIgLT4-IEc6IHJlbmRlciByZUNhcHRjaGEgVUkgdXNpbmcgW3NpdGUga2V5XVxuRyAtLT4-IEI6IFtyZUNhcHRjaGEgVUldXG5cbnJlY3QgcmdiYSgwLCAyNTUsIDI1NSwgLjEpXG4gIFUgLT4-IEI6IGZpbGwgZm9ybVxuICBCIC0-PiBHOiBjaGVjayBbSSdtIG5vdCBhIHJvYm90XVxuICBHIC0tPj4gQjogcmVzcG9uc2UgW3Rva2VuXVxuZW5kXG5cbnJlY3QgcmdiYSgyNTUsIDAsIDI1NSwgLjEpXG4gIFUgLT4-IEI6IHN1Ym1pdFxuICBCIC0tPj4rIEE6IHN1Ym1pdCBbZm9ybSBkYXRhXSBhbG9uZyB3aXRoIFt0b2tlbl1cbiAgQSAtLT4-IEc6IHZhbGlkYXRlIFt0b2tlbl0gdXNpbmcgW3NlY3JldCBrZXldXG4gIEcgLS0-PiBBOiBbc3VjY2Vzcy9mYWlsZWRdXG4gIEEgLS0-Pi0gQjogW3Jlc3VsdF1cbmVuZCIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In0sInVwZGF0ZUVkaXRvciI6ZmFsc2UsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)
