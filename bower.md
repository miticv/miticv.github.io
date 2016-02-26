


if bower install gives error: self_signed_cert_in_chain     
create file `.bowerrc` with following content:
```
  {
  "strict-ssl": false,  
  "https-proxy": ""
  }
```
In windows create file bowerrc and rename it with: `ren bowerrc .bowerrc`

