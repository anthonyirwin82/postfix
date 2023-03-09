# postfix
A public list of my white/block list and spam block list for postfix 

I have added the following to my main.cf file for the extra config files some of which are not included in the public github repo. 

You will need to add the relevant check_sender_access lines to your main.cf file for things to work. 

The whitelist_addresses are individual email addresses of people I have whitelisted which have not been published on the public repo for obvious reasons.

The reject_rhsbl_helo and reject_rbl_client are public spam databases that I use and recommend to block unwanted known spammers.

You may need to register with some of them for you to be able to use their service. 

portion of main.cf file:
```
smtpd_recipient_restrictions =
        permit_mynetworks,
        permit_sasl_authenticated,
        reject_non_fqdn_recipient,
        reject_unknown_recipient_domain,
        reject_unlisted_recipient,
        reject_unauth_destination,
        check_sender_access hash:/etc/postfix/whitelist_addresses,
        check_sender_access hash:/etc/postfix/spam_senders,
        check_sender_access hash:/etc/postfix/sender_access,
        check_sender_access regexp:/etc/postfix/block_tlds,
        reject_rhsbl_helo dbl.spamhaus.org,
        reject_rhsbl_reverse_client dbl.spamhaus.org,
        reject_rhsbl_sender dbl.spamhaus.org,
        reject_rbl_client zen.spamhaus.org,
        reject_rbl_client bl.spamcop.net,
        reject_rbl_client dnsbl.sorbs.net,
        reject_rbl_client psbl.surriel.com
smtpd_sender_restrictions =
        permit_mynetworks,
        permit_sasl_authenticated,
        reject_non_fqdn_sender,
        reject_unknown_sender_domain,
        check_sender_access hash:/etc/postfix/whitelist_addresses,
        check_sender_access hash:/etc/postfix/spam_senders,
        check_sender_access hash:/etc/postfix/sender_access,
        check_sender_access regexp:/etc/postfix/block_tlds
```
