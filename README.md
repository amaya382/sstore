# :inbox_tray: :closed_lock_with_key: sstore

*Just a concept*

You can securely put/get text by only a ssh key from anywhere.


## Usage
### Server (can be a service)
1. Create a user
1. Register a ssh key
1. Set a command in `authorized_keys`
1. Create a directory for storage

## Client
1. Set server and key-pair info into `sstore`
1. Put text: `echo -n 'some-secret-text' | sstore put key1`
1. Get text: `sstore get key1`


## Use Case
By storing your slack webhook url in the sstore, you can post to slack from a remote server w/o explicit secure contexts (webhook url).

1. (Local) `echo -n 'https://hooks.slack.com/services/xxx/yyy/zzz' | sstore put slack-webhook-url`
1. (Local->Remote) Use ssh-agent for carrying your public key
1. (Remote) `curl -X POST -H 'Content-Type: application/json' -d '{"text": "hello!"}' $(sstore get slack-webhook-url)`

*NOTE: Using a public key from ssh-agent is NOT implemented*

