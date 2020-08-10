# lightning-app-boilerplate

## Install
```shell
npm install
```

## Private key generation
* Generate and save private key:
```bash
$ node -p "require('btcpay').crypto.generate_keypair().getPrivate('hex')"

>>> <Key priv: XXXXXXX pub: null >
```

Store the value of "priv" in a save place, e.g. environment variables

## Pairing

After generating your private key, you have to pair your client with your BTCPay store:

* On BTCPay Server > Stores > Settings > Access Tokens > Create a new token, (leave PublicKey blank) > Request pairing
* Copy pairing code:
* Pair client to server and save returned token:

```bash
# Replace the BTCPAY_XXX envirnoment variables with your values and run:

$ [space] BTCPAY_URL=https://mydomain.com/ BTCPAY_KEY=... BTCPAY_PAIRCODE=... node -e "const btcpay=require('btcpay'); new btcpay.BTCPayClient(process.env.BTCPAY_URL, btcpay.crypto.load_keypair(Buffer.from(process.env.BTCPAY_KEY, 'hex'))).pair_client(process.env.BTCPAY_PAIRCODE).then(console.log).catch(console.error)"

# (prepend the line with a space to prevent BTCPAY_KEY from being saved to your bash history)

>>> { merchant: 'XXXXXX' }
```

```powershell
# In Windows Powershell, execute these commands one by one:

$env:BTCPAY_URL='https://mydomain.com/'
$env:BTCPAY_KEY='KEY'
$env:BTCPAY_PAIRCODE='PAIRCODE'
node -e "const btcpay=require('btcpay'); new btcpay.BTCPayClient(process.env.BTCPAY_URL, btcpay.crypto.load_keypair(Buffer.from(process.env.BTCPAY_KEY, 'hex'))).pair_client(process.env.BTCPAY_PAIRCODE).then(console.log).catch(console.error)"
```

Store the value of "merchant" in a save place, e.g. environment variables
