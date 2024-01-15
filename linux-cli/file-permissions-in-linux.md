# File permissions in Linux

### Project description

I completed this during Google's Cybersecurity Certificate Program.

In the project directory, there are several files, including a hidden file, and a subdirectory that have permissions in need of being updated. I checked the directory and file permissions, identified what needed to be changed, then updated the permissions.

### Check file and directory details

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/SK5cQK9nTvMAJ3HjMrRu1qJTADoHdSJAzM8OgcmIFhVApYLqAIdSQSvUocv8j-WnKGme2aMNadAnYGOwoOF4UJ6Zb55vI7yG5Adysr3odG9sgK4oBObj13Q9uVK-uC6ijfqZmA82SZGMZLNZ5ykt776YGFsuCVcqlPqgk4v0NRH1fD6cUN9Wkuod7Hhud-w" alt="" width="563"><figcaption></figcaption></figure>

</div>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/blydW4g6r6Etag4A4CAEYId_2_g2u7_EIkJRYxInnbnXZ7k-EqOaqKR2zevDdR41qnj1JdzJufNCNuhnRbJF5i7ep7rVTicq7Z_NqC5Gk_NQuoDuG51oRGOj0R0ygsJYmV7RkNrnKSlbmepXO0DWVFqPTvAJaAUV8pCSk5bAwP2xstxK0tfQW22aXY3KCBg" alt="" width="563"><figcaption></figcaption></figure>

</div>

### Describe the permissions string

Above, I can see that project\_k.txt has read and write permissions for the user, group and other. However, other should not be able to write.

In project\_m.txt the group currently has read permission, but it should not.

In the hidden file, .project\_x.txt, the only permission should be the user and group having read permission.

Last, in the directory drafts, the group should not have executable permissions.&#x20;

Below are steps taken to verify the current permission and update them. At times, I look at permissions for only a specific file or directory to reduce the possibility of the error.&#x20;

### Change file permissions

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/fF86a5sNya3l5biUmyXml1zt3wnqSjRw5wfB8rVSB6zfQSHbUULDCibnVxJb5efB6pkIlxt-2yBTii1t7DPDuH7A8qxtNEwiqb5M9d_0ixFmnzK_wdfJCmV2l7mk2yRIknmgj8aqGMEERlg8Pa79__O1kzuIgvB829iMEJEGLS-UeMDFKJB1ccKqLEbH79E" alt="" width="563"><figcaption></figcaption></figure>

</div>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/zIzg-mUyVkca5SrTOh5NCv9GDzbW0AjZhZlEibGL5VWXMfS03ttbmt-X1oAy76H8uizgc-KIbURuOEuKGWmiEDjlyuA2F20O4OBTjZv88AclC7SM_-QNGY0-DUcXsAmAY5jOX5lkRjLGGmsQ00QYlNZ0dduPBx9af53VaP8tLYgkiLFFw-cBDGNC5xd6fDg" alt="" width="563"><figcaption></figcaption></figure>

</div>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/JnrS9EK3bajUoJwrSKlPAnNhsDWvVqhZd7635DD_aZ_JsybGP2CUy9KrRFF0ApJIv0hJhJCtNAJ-QivWCK8Yf9DSgUueM1UjPpc6G195HLiP3k1GLael32_7PdaODD6Qd6q5V5UES7pj4vyqCLzcYaVAlTWDROJnkRe4ATPB11tAaXqNoYEpK23Vk4keilI" alt="" width="563"><figcaption></figcaption></figure>

</div>

### Change file permissions on a hidden file

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/o7rXS2hG-GN816iqPvPDaAkuIMChFb6ifVvRkq5CxKZb7GD-zhBJRWRTzXFcfQoamA5Eqkflg_mnbIXcNfgA65cY6YZKGUiWwbdjHcxr5t91c-jwGTIYF6DGibjP-kE3c5AvsRDgyW5rxdFtzUMjmSbRE1TQumDqW0DNyOLN7XLaXx-FWXfVyEJ1L5ROTZ4" alt="" width="563"><figcaption></figcaption></figure>

</div>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/TbqC8eAeTgHv8OVu4Wvx5EYtp4LP4_bgBNMJQLL_p6lwdtZjtaIfgglwmWlCwJSGZ5koSA-4ra6_PgntZtdJ6Du_eNFEfRMIzALM39bpjSfepcGdg0cHF6BTWJUB1unksPF2AkisedT4cGpSOvDDp8GbSDrrXVoABFymEvxgnTeTHzLF7dTLilsesa94eDQ" alt="" width="563"><figcaption></figcaption></figure>

</div>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/gXIAL7X-m9DjZGP97szJR43VXWB-JrFIq4i4jFiWrLchT_lbk0vvIPamljNHS5MPfbPaXB-h9DWG51CwvPgsztrHTuCDcbX6mWdF4iaGZLIvDw5iPsaseEqvbqIcQEhMQQNP12elkfBC6o2r-7wGNJvKG2r1cW3EFWxQvKsZ57oCFW14uVgIHKMrYU0OvXc" alt="" width="563"><figcaption></figcaption></figure>

</div>

### Change directory permissions

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/uVnKEXuhLZUv1L-t3OQmL1sGuWTCvNPL_QdFY1OMUAQL45uE-M9loRxYv3l_6hw31YdU1kQa192SNrtn1t21JvYHp-N3aYpbUBNgllw1PgZOUQnMyaxdCyxcCwVYGqFeVMuP_KsZ1IOjpaTvjk9gg9dXruNMF92z7_2DOx99Sl6yrA6I-vPRJh1W7NhIkVQ" alt="" width="563"><figcaption></figcaption></figure>

</div>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/LKFXQsmsAzL5_Nxw6CYbuG99t9xxOLhG-_RiPAveIT4rDHmM1GdKvUvdCNXoa4fbc9J-aFgG0K4lAwsXy_R05bUmRE5Rcb4cFziiF3a2IWJH9Uk7BEw2af0r294n3FiP74yIHZNBBRJp-u_KdDWHNx-XnBzuwZeMfj3zx1HC3PyDrECbVpaU1KDcCdS4rC0" alt="" width="563"><figcaption></figcaption></figure>

</div>

### Summary

After reviewing and updating permissions, all permissions for the directory projects/ are updated and correct. The security team would be able to move forward confidently knowing that they are following the rule of least privilege.

\
