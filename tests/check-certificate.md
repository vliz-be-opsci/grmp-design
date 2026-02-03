# Check Certificate

1. Certificate expiration 
   1. is expired -> ERROR 
   2. is less than certificateExpiryDays days in the future -> WARN
2. Certificate revoked  
   1. Certificate Revocation List (CRL)
   2. Online Certificate Status Protocol (OCSP)
   3. Certificate other tests: see https://badssl.com/ 


### MoSCow:

| Number | Name                    | MoSCoW |
|--------|-------------------------|--------|
| 1      | Certificate expiration  | Should |
| 2      | Certificate Revoked     | Won't  |
| 3      | Certificate other tests | Won't  |
