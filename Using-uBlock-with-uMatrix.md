_[I need to revise this article, it was heavily edited by someone else and I don't agree with some stuff in there -- and I do not even agree with my original version, as uBlock had changed a lot since the time this was written.]_

***

Keep in mind uMatrix and uBlock are two different extensions. Each can be used as a standalone extension, you do not have to use one if you use the other. uBlock is for everybody, uMatrix is for advanced users who understand that sites will easily break when using a firewall, and have good knowledge of how to un-break sites by editing firewall ruleset.

Nevertheless, a combination uBlock with uMatrix can make sense. So, if you choose to use uBlock with uMatrix, here are suggestions:

~~Un-select all _"Malware domains"_ lists in uBlock if the same lists are selected in uMatrix. uMatrix is more hardcore when it comes to block net requests from undesirable remote servers: when a hostname is blacklisted, even the root document will be prevented from downloading, while uBlock will only block secondary resources -- as per ABP-filter semantic.~~
This should be no more necessary in uBlock *Origin*, since uBlock *Origin* with activated strict blocking has the ability, to block the root document too.

So, if you leave _"Malware domains"_ selected in uBlock AND uMatrix, it can be a huge advantage for security, at least for following scenario: you allow a domain (at this time no malware domain) in uMatrix (change it to green) and leave this domain untouched in uBlock. After a while, this domain becomes a malware domain (comes on the malware domain list, THEN: uMatrix does not block this domain (because it's green) - BUT: uBlock blocks it (because the domain is on the malware list)!

**Restriction for Chrome:**
Do not use dynamic filtering for `script` tags in uBlock. The Chrome API allows only one extension to modify outgoing and incoming HTTP headers, and thus it is better to make sure uMatrix has full control of the HTTP headers. So make sure uBlock gets out of the way of uMatrix by disabling dynamic filtering for `script` tags. You can keep dynamic filtering for `iframe` enabled in uBlock if you wish though, there is no harm.