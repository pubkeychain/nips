# NIP-alpaca
## Key rotation for nostr users
This NIP defines a way to enable key rotation for nostr users. 


### Linking your current keypair to the cornersat

Have the public key of the keypair you are currently using on hand. 

Use a Bitcoin wallet of your choice to inscribe a satoshi with the current public key following the PKCP specification. 
Make note of the satoshi ordinal number and [name](https://docs.ordinals.com/overview.html#names).

Declare the satoshi as your cornersat in your nostr metadata using an optional property in the content of the event of kind 0 (user metadata):
'cornersat': the name of the inscribed satoshi.

The relays are expected to check that the cornersat listed actually has an inscription of the pubkey used in the event data as the last pubkey published and thus still counts as valid. 

You should not be able to retroactively claim a satoshi with a pubkey that is no longer the last inscribed. 

The relay should respond with an OK message and notify the client if the cornersat was accepted or not. not. 


### Rotating keys

When rotating keys, create a new keypair and inscribe the new pubkey on the same satoshi you used previously, your cornersat. 

When signing into a nostr client for the first time, the new keypair won't have any associated data.
You can claim your history by creating a user metadata event with the cornersat property set to the same satoshi name as in your previous profile. 

Any NIP-05 references to the previous pubkey will not be mapped automagically to the new pubkey after rotating keys.


### Inspiration

A nostr client might be able to offer various imports of previous settings, like profile and people you follow. 
It is a little trickier to let all followers of the previous pubkey switch to the new one. 
Maybe a client might offer the followers of the previous pubkey the option to switch to the new active one. 
A good optimization would also be to deduplicate follows that share the same cornersat. 

A nostr client might offer functionality to check the inscriptions and notify you of any key rotations for a given profile with a declared cornersat. 
