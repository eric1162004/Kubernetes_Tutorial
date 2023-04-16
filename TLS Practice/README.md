## Creating a Self-Signed Certificate
`openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout domain.key -out domain.crt`

## Create Certificate Authority
`openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout rootCA.key -out rootCA.crt`

## Decode cert into text
`openssl x509 -in domain.crt -text -noout`
