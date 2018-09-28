# HomeQ Digital Signatures

Instructions on how to verify digital contracts generated on the HomeQ platform.

In order to verify the signature you need to do the following steps.


1. Remove everything from the beginning of '---BEGIN SIGNATORIES---' to the end of the document including 
   the EOF in the end and store the remaining bytestream back to file.
2. The resulting bytestream should be a valid PDF and can be hashed with the algorithm given in the METADATA section.
3. The attached signatures in the ---BEGIN SIGNATURES--- section are bas64 encoded json blobs that contain the BankID response (OCSP response and Signature). You can refer to the BankID documentation on how to verify the signatures.
        You will need the BankID root certificate that you can get from them to verify the certificate chains.
4. If the signatures are valid you can compare the hash of the document (step 2) with the hash given in the user non visible data within the XML-SIGNATURE of the BankID response for each user. If the hash matches, the signature was indeed referring to the bytestream version of this document.
5. Make sure that all signatures are there that were expected: See the METADATA for the expected signatures. Be aware that matching the expected signatories should be done with the user certificates issued by the Banks (within the certificate chain in the Signature in the BankID response), not with the users that are listed in the raw bank_id response, as this information is not signed. If there are any further questions please reach out to the support email mentioned in the META data, or raise an issue in this repository.
