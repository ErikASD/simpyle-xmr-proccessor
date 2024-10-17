# simpyle-xmr-processor
A simple Monero (XMR) payment processor that credits accounts using a pgp login system


GnuPG and monero wallet rpc Required:

Linux: https://gnupg.org/download/index.html

Windows: https://gnupg.org/ftp/gcrypt/binary/

Please notify me if there are any glaring/conceptual security holes

install monero folder
create wallet only intended for processor

Linux: ./monero-wallet-rpc --rpc-bind-port (wallet_rpc_port) --daemon-address (daemon_ip_with_port) --wallet-file (wallet_name) --prompt-for-password --disable-rpc-login

Windows: monero-wallet-rpc.exe --rpc-bind-port (wallet_rpc_port) --daemon-address (daemon_ip_with_port) --wallet-file (wallet_name) --prompt-for-password --disable-rpc-login

Loop Estimate: 

disabled by default

in config.json there is an option to enable a loop estimate that tries to estimate many times. Sadly the wallet RPC does not have an option to calculate fee before transfer.

Regular Estimate:

Sends a transaction with do not relay with requested amount.

fee is deducted and a transaction2 is sent to compensate for the fee.

if withdraw is same or lower than requested amount, relay_tx transfers and completes the withdraw.


Deposit:

No Sweep Architecture. Better for fees and ring signature privacy.

Keeps all outputs in subaddresses and keeps track of them with db with propper credit protocol.



Live Reload:

Useful in development. Recommended to turn off during production for less resource usage.


RPC is hosted on loopback 127.0.0.1 and any requests from host machine is trusted by wallet rpc. If someone hacks your server, rpc login does not protect much as login is stored on server 
anyways. Always treat wallets connected to internet as a hot wallet and only store as much needed for operation. The rest should be periodically sent to a cold wallet.
A hot wallet is always vulnerable to server exploits, server host access, and other ways to get on the server. Plan accordingly. 

Always run under reverse proxy/load balancer (nginx).

If you would like to donate to help me develop future monero projects:

monero:84wPRTvp1NVMHmgXBoYHd29Q3s7TNC48CWP3kqQHzdofKmy2XSbdNvaCZd1HevB9T77o4ZaAC65DFgckZzL9NfGeV8mKLfm
