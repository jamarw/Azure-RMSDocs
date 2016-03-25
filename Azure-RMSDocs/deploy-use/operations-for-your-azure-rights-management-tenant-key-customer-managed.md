---
title: Customer-managed - tenant key lifecycle operations
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
author: Cabailey
---

# Customer-managed: Tenant key lifecycle operations
If you manage your tenant key for Azure Rights Management (the bring your own key, or BYOK, scenario), use the following sections for more information about the lifecycle operations that are relevant to this topology.

## Revoke your tenant key
When you unsubscribe from Azure RMS, Azure RMS stops using your tenant key and no action is needed from you.

## Re-key your tenant key
Re-keying is also known as rolling your key. Do not re-key your tenant key unless it’s really necessary. Older clients, such as Office 2010, were not designed to handle key changes gracefully. In this scenario, you must clear the RMS state on computers by using Group Policy or an equivalent mechanism. However, there are some legitimate events that may force you to re-key your tenant key. For example:

-   Your company has split into two or more companies. When you re-key your tenant key, the new company will not have access to new content that your employees publish. They can access the old content if they have a copy of the old tenant key.

-   You believe the master copy of your tenant key (the copy in your possession) was compromised.

When you re-key your tenant key, new content is protected by using the new tenant key. This happens in a phased manner, so for a period of time, some new content will continue to be protected with the old tenant key. Previously protected content stays protected to your old tenant key. To support this scenario, Azure RMS retains your old tenant key so that it can issue licenses for old content.

To re-key your tenant key, generate and create a new key over the Internet or in person, by using the procedures in the [Implementing bring your own key (BYOK)](..\plan-design\planning-and-implementing-your-azure-rights-management-tenant-key.md#implementing-your-azure-rights-management-tenant-key) section from the [Planning and Implementing Your Azure Rights Management Tenant Key](..\plan-design\planning-and-implementing-your-azure-rights-management-tenant-key.md) topic.

## Backup and recover your tenant key
You are responsible for backing up your tenant key. If you generated your tenant key in a Thales HSM, to back up the key, just back up the Tokenized Key file, the World file, and the Administrator Cards.

If you transferred your key by following the procedures in the [Implementing bring your own key (BYOK)](..\plan-design\planning-and-implementing-your-azure-rights-management-tenant-key.md#implementing-your-azure-rights-management-tenant-key) section from the [Planning and implementing your Azure Rights Management tenant key](..\plan-design\planning-and-implementing-your-azure-rights-management-tenant-key.md) topic, Azure RMS will persist the Tokenized Key File, to protect against failure of any Azure RMS nodes. However, do not consider this to be a full backup. For example, if you ever need a plaintext copy of your key to use outside a Thales HSM, Azure RMS will not be able to retrieve it for you because it only has a non-recoverable copy.

## Export your tenant key
If you use BYOK, you cannot export your tenant key from Azure RMS. The copy in Azure RMS is non-recoverable. If you want to delete this key so it can no longer be used, contact Microsoft Customer Service Support (CSS).

## Respond to a breach
No security system, no matter how strong, is complete without a breach response process. Your tenant key might be compromised or stolen. Even when it’s well protected well, vulnerabilities might be found in current generation HSM technology or current key lengths and algorithms.

Microsoft has a dedicated team to respond to security incidents in its products and services. As soon as there is a credible report of an incident, this team engages to investigate the scope, root cause, and mitigations. If this incident affects your assets, then Microsoft will notify your Azure RMS tenant administrators by email by using the address that you supplied when you subscribed.

If you have a breach, the best action that you or Microsoft can take  depends on the scope of the breach; Microsoft will work with you through this process. The following table shows some typical situations and the likely response, although the exact response will depend on all the information that is revealed during the investigation.

|Incident description|Likely response|
|------------------------|-------------------|
|Your tenant key is leaked.|Re-key your tenant key. See [Re-key your tenant key](#re-key-your-tenant-key) .|
|An unauthorized individual or malware got rights to use your tenant key but the key itself did not leak.|Re-keying your tenant key does not help here and requires root-cause analysis. If a process or software bug was responsible for the unauthorized individual to get access, that situation must be resolved.|
|Vulnerability discovered in the current-generation HSM technology.|Microsoft must update the HSMs. If there is reason to believe that the vulnerability exposed keys, then Microsoft will instruct all customers to renew their tenant keys.|
|Vulnerability discovered in the RSA algorithm, or key length, or brute-force attacks become computationally feasible.|Microsoft must update the Azure RMS to support new algorithms and longer key lengths that are resilient, and instruct all customers to renew their tenant keys.|

## See Also
[Using Azure Rights Management](using-azure-rights-management.md)
