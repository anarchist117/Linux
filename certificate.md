openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout domain.com.key -out domain.com.crt \
  -subj "/CN=*.domain.com" \
  -addext "subjectAltName=DNS:*.domain.com,DNS:domain.com"
