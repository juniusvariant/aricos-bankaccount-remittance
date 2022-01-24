# Data References

Below are some list of data references that you require to use our API's.

## Remittance Statuses

Key | Description
--------- | -----------
PENDING_RISK_ASSESSMENT | Request is being processed and assessed in the risk scoring system.
COMPLIANCE_VERIFICATION | Request is considered medium or high risk, and is being reviewed by our compliance team. Our team will contact you via email for extra information for enhanced due diligence.
COMPLIANCE_REJECTED | Request is rejected by compliance.
PROCESSING | Request has been approved and the remittance is queued to be transferred to the recipient.
COMPLETED | The sending bank has confirmed transmission of the remittance.
FAILED | Remittance could not be transferred to the recipient due to certain errors. See [Remittances Failure Codes](#remittance-failure-codes).

## Remittance Failure Codes

Key | Description
--------- | -----------
INSUFFICIENT_BALANCE | The balance in your account is insufficient to make the remittance in the desired amount.
UNKNOWN_BANK_NETWORK_ERROR | The bank networks have returned an unknown error to us. We are unable to predict whether the remittance will succeed should you retry the same remittance request.
TEMPORARY_BANK_NETWORK_ERROR | The bank networks are experiencing a temporary error. Please retry the remittance in 1-3 hours.
TEMPORARY_TRANSFER_ERROR | We’ve encountered a temporary issue while processing this remittance. Please retry the remittance in 1-2 hours.
SWITCHING_NETWORK_ERROR | At least one of the switching networks is encountering an issue. Please retry the remittance in 1-3 hours.
INVALID_DESTINATION | The banks have reported that the destination account is unregistered or blocked. If unsure about this, please retry again or contact the destination bank directly regarding the status of the destination account.
TRANSFER_ERROR | We’ve encountered a fatal error while processing this remittance. Certain API fields in your request may be invalid. Please contact our customer support team for more information.

## Agent Codes

ID | Key | Description
--------- | --------- | -----------
37c184a7-0fb8-4a06-b087-49f17163e863 | BCA                          | Bank Central Asia
0e765d93-9723-4ec8-98c1-23003143ef9a | BCA_SYR                      | Bank Central Asia Syariah
ca0295c6-6be7-4609-9606-c1bb25f7847e | BJB                          | Bank BJB
dcd08b39-f7af-445b-9643-c604de4a101d | BNI                          | Bank Negara Indonesia
4f672043-2b01-4fe0-a1f6-ad13962e48b7 | BNI_SYR                      | BNI Syariah
0766f37c-ae8d-4d86-ae06-e4b1ce236fd1 | BRI                          | Bank Rakyat Indonesia
686c0948-4338-44b6-90e2-364dc44f35ae | BRI_SYR                      | BRI Syariah
a225789f-d5c3-4e62-ad59-8599d2df5d0a | CENTRATAMA                   | Centratama Nasional Bank
e8f04b8b-244a-4a92-8175-0b8b5b40c3d0 | CIMB                         | Bank CIMB Niaga
497fac65-ffe5-4931-bc69-fb56f2c9fe1a | DANAMON                      | Bank Danamon
8863cd7c-719a-4a02-9766-a488c844aad4 | MANDIRI                      | Bank Mandiri
427c76de-0e9b-47fb-8200-c62390c5598a | MANDIRI_SYR                  | Bank Mandiri Syariah
3d46860d-8d96-4982-bb77-dc5e74ddd3d2 | RIAU_DAN_KEPRI               | BPD Riau Dan Kepri
4ec745a2-ab71-47d3-a67b-c3c5cadfa151 | ROYAL                        | Bank Royal Indonesia
286aa3e5-c747-41dd-965e-4df5ac792009 | SINARMAS_UUS                 | Bank Sinarmas UUS
b28a6020-5715-4fb0-8162-c8dba00dba1f | SUMUT                        | BPD Sumut
1168cf9b-a361-4ce8-b0c5-707d4d0e0f75 | TABUNGAN_PENSIUNAN_NASIONAL  | Bank Tabungan Pensiunan Nasional
7dbc1f29-0bf6-47af-b085-04b4898f7b40 | ACEH                         | BPD Aceh
1faa0310-d168-46b1-8a20-ed23d1106b7b | ACEH_UUS                     | BPD Aceh UUS
e8259b9c-1c48-4790-87d5-b4177c7fef2c | AGRIS                        | Bank Agris
2c5186f3-f3dc-4403-8b7c-633615c02d96 | AGRONIAGA                    | Bank BRI Agroniaga
1dc8787c-8ccb-4238-ba8d-b944fc82466c | AMAR                         | Bank Amar Indonesia (formerly Anglomas International Bank)
d7a3c514-122b-453f-84d7-a655a03973c5 | ANZ                          | Bank ANZ Indonesia
a5c7ed6a-3e9a-4ded-b468-311aa2f68e09 | ARTA_NIAGA_KENCANA           | Bank Arta Niaga Kencana
ed1492dc-2246-439b-92f5-05ce10d607a1 | ARTHA                        | Bank Artha Graha International
a37bd8bd-5cab-48c9-a3ec-7620980fc0a3 | ARTOS                        | Bank Artos Indonesia
cfdd6374-e9b4-45cb-a5da-7b69b67042de | BALI                         | BPD Bali
27dd6012-99a0-410e-b390-58e5ac5d0852 | BAML                         | Bank of America Merill-Lynch
e53972b7-3805-4739-a10f-1353c3ea3541 | BANGKOK                      | Bangkok Bank
f47428df-93d1-4e22-b20d-5027e9487f5f | BANTEN                       | BPD Banten (formerly Bank Pundi Indonesia)
770cda3d-28dc-4c5c-9278-07f7363a847a | BCA_DIGITAL                  | Bank Central Asia Digital (BluBCA)
259a5418-c3ec-4fd3-8e8b-54c83a27e87c | BENGKULU                     | BPD Bengkulu
707e77c9-8360-4a08-abde-e8e9ec57b63b | BISNIS_INTERNASIONAL         | Bank Bisnis Internasional
efb98175-f10d-4224-a95d-1660db2535f8 | BJB_SYR                      | Bank BJB Syariah
eb6e2cbe-1b5e-4c46-aeb4-10528b429ed0 | BNP_PARIBAS                  | Bank BNP Paribas
d517c60b-975a-4b3c-bf02-e0e37dff1c5a | BOC                          | Bank of China (BOC)
ab5462b4-20ef-4390-9d18-7d9e357a1528 | BSI                          | Bank Syariah Indonesia (BSI)
164d2066-6326-4bdb-b545-5530a59d854e | BTN                          | Bank Tabungan Negara (BTN)
1819473a-db73-4296-a470-bf5a3bbeb244 | BTN_UUS                      | Bank Tabungan Negara (BTN) UUS
2be61dc1-41c3-4947-b820-ec706de4be0a | BTPN_SYARIAH                 | BTPN Syariah (formerly Bank Sahabat Purba Danarta and Bank Tabungan Pensiunan Nasional UUS)
a1269069-1f69-498f-99c0-917fc6a9ca26 | BUKOPIN                      | Bank Bukopin
12135f0d-bda3-4e72-80ae-dc9eabd95c56 | BUKOPIN_SYR                  | Bank Syariah Bukopin
f9eaa3b0-9411-4adf-84ed-997a2b0753d1 | BUMI_ARTA                    | Bank Bumi Arta
0dd9909c-7549-4f7d-a65e-2237cdbd03c2 | CAPITAL                      | Bank Capital Indonesia
48eba4c8-d0b6-4067-8fc4-302f5f60bdf9 | CCB                          | China Construction Bank Indonesia (formerly Bank Antar Daerah and Bank Windu Kentjana Int)
b1464ebb-db6b-4ffb-be58-b8035de76a97 | CHINATRUST                   | Bank Chinatrust Indonesia
d930a8da-9ca3-4264-8af0-aa0adae50dfa | CIMB_UUS                     | Bank CIMB Niaga UUS
a39fdee9-8b51-48f1-9505-7463e34e3b69 | CITIBANK                     | Citibank
3c15a710-62d4-4df3-81e8-e4d660af8d23 | COMMONWEALTH                 | Bank Commonwealth
560fc226-0266-4d2c-9537-415a7191ad95 | DAERAH_ISTIMEWA              | BPD Daerah Istimewa Yogyakarta (DIY)
74940969-9838-46fb-87f1-348996e94047 | DAERAH_ISTIMEWA_UUS          | BPD Daerah Istimewa Yogyakarta (DIY) UUS
ecf31864-5fd6-47ac-a6f4-1fe5a9810fdb | DANAMON_UUS                  | Bank Danamon UUS
62e6a266-3aaf-4e96-bf34-6de8faeb3dbd | DBS                          | Bank DBS Indonesia
d46a5ba1-99d1-4c68-a53f-bb0c6d522ac3 | DEUTSCHE                     | Deutsche Bank
1909f88f-9751-4396-a41c-8373ddf78d59 | DINAR_INDONESIA              | Bank Dinar Indonesia
1bc83028-86e1-4a54-84d0-c092ad25d043 | DKI                          | Bank DKI
7a43da85-cee4-4de2-be74-83e8fbcb8a6d | DKI_UUS                      | Bank DKI UUS
1692293e-b6d8-4a74-860b-09d4653b1e9b | EXIMBANK                     | Indonesia Eximbank (formerly Bank Ekspor Indonesia)
e2efe4c7-b149-4158-9794-a33d595df1aa | FAMA                         | Bank Fama International
a90908ca-08bc-45a9-b6be-22d832a3a203 | GANESHA                      | Bank Ganesha
72e56a7d-9fe0-425a-b5c0-9c836350dbbb | GOPAY                        | GoPay
7aa069e2-1345-4e8b-917e-1743841b4aa8 | HANA                         | Bank Hana
baa92a9b-680e-4398-afcf-3b9eea03848a | HARDA_INTERNASIONAL          | Bank Harda Internasional
1f08d58e-01c4-402a-88d0-451e238eb29b | HSBC                         | Hongkong and Shanghai Bank Corporation (HSBC) (formerly Bank Ekonomi Raharja)
35eb92ec-4416-42d1-8c6f-f6962c3b60ee | ICBC                         | Bank ICBC Indonesia
51a3cde1-966c-47df-94b6-3073eabad300 | INA_PERDANA                  | Bank Ina Perdania
8ab225ce-fc13-47f6-b64c-30984f232c11 | INDEX_SELINDO                | Bank Index Selindo
ecb4542f-0d17-4e3a-b5ad-d7a9132e9edf | INDIA                        | Bank of India Indonesia
ba55253b-3bc3-4785-874c-f5deeeab7fba | JAMBI                        | BPD Jambi
c012a45a-c642-4a7d-baac-13cc4e38d9af | JAMBI_UUS                    | BPD Jambi UUS
93d356a1-b2c9-44bd-b2f4-844abc433724 | JASA_JAKARTA                 | Bank Jasa Jakarta
33378408-6284-4fce-834c-9721de3cc1bf | JAWA_TENGAH                  | BPD Jawa Tengah
6caa08a0-d6f8-42bd-b701-1275ca9106f1 | JAWA_TENGAH_UUS              | BPD Jawa Tengah UUS
a6ef5610-d6b9-41e7-aaa3-0a8a86992d3d | JAWA_TIMUR                   | BPD Jawa Timur
b1b499b4-d90c-4a17-9c31-fc317342ddc2 | JAWA_TIMUR_UUS               | BPD Jawa Timur UUS
c88314be-62e4-4ea3-bffb-20d11bbec5ee | JPMORGAN                     | JP Morgan Chase Bank
f20da36c-225d-4362-8445-36f671e8dc5f | JTRUST                       | Bank JTrust Indonesia (formerly Bank Mutiara)
3f5a9be6-4414-437a-927a-423fdcf84e64 | KALIMANTAN_BARAT             | BPD Kalimantan Barat
2b0921bb-f99d-42be-bf0c-90d6aa1b933c | KALIMANTAN_BARAT_UUS         | BPD Kalimantan Barat UUS
495bfad5-88be-4d0a-b1fc-52b410733678 | KALIMANTAN_SELATAN           | BPD Kalimantan Selatan
0929a540-1e41-40c6-824b-0b36adf43ea8 | KALIMANTAN_SELATAN_UUS       | BPD Kalimantan Selatan UUS
83a0e1a5-510a-4f38-8f6a-9390bed7880e | KALIMANTAN_TENGAH            | BPD Kalimantan Tengah
c8f30047-e3b9-433d-9be6-20de2636f5a8 | KALIMANTAN_TIMUR             | BPD Kalimantan Timur
d2cec9f3-092d-4eb2-8815-86238cd947c6 | KALIMANTAN_TIMUR_UUS         | BPD Kalimantan Timur UUS
c1ade29c-e09c-45aa-bfd7-28b3045be6e8 | KESEJAHTERAAN_EKONOMI        | Bank Kesejahteraan Ekonomi
b5dbfe03-835f-4a04-9aab-08a492e550ce | LAMPUNG                      | BPD Lampung
04df76a7-b7f1-4f96-945a-9a46166255d9 | MALUKU                       | BPD Maluku
cc995e02-b96b-4472-9f0d-959ab03b0645 | MANDIRI_ECASH                | Mandiri E-Cash
be77ec02-f995-4103-88c8-2e861f9ebf66 | MANDIRI_TASPEN               | Mandiri Taspen Pos (formerly Bank Sinar Harapan Bali)
fa34365e-3b26-4c78-bea2-31d7452c3c04 | MASPION                      | Bank Maspion Indonesia
ea74ddf4-71d1-4326-bbf6-b5405f9db18b | MAYAPADA                     | Bank Mayapada International
a6180c69-c22c-4d7d-aab8-a68b94ed0794 | MAYBANK                      | Bank Maybank (formerly BII)
4496121c-0665-4831-8d5d-69032127f1db | MAYBANK_SYR                  | Bank Maybank Syariah Indonesia
df3ec0ca-3e9c-4e1c-898c-6006c4f2aa05 | MAYORA                       | Bank Mayora
e36f5a2e-a6db-437f-98f0-a4c4e47e597b | MEGA                         | Bank Mega
e3c8f715-1b98-4d4c-af92-1a6fee743535 | MEGA_SYR                     | Bank Syariah Mega
e6c54ce8-51b1-46ee-b059-52fa7812b89f | MESTIKA_DHARMA               | Bank Mestika Dharma
7795b270-9144-4510-8f03-f3cc7f498140 | MITRA_NIAGA                  | Bank Mitra Niaga
6f338e2f-5abc-4b1f-a03d-529183acae6e | MITSUI                       | Bank Sumitomo Mitsui Indonesia
ed0318a9-b4b7-48d8-982f-823dda080d1a | MIZUHO                       | Bank Mizuho Indonesia
420315a6-72de-4498-90b3-f1eb2111ccf0 | MNC_INTERNASIONAL            | Bank MNC Internasional
76efc335-78fc-4d79-b5bc-90608696c324 | MUAMALAT                     | Bank Muamalat Indonesia
2071fbd2-a3d2-4209-903d-4509f9ab7ad9 | MULTI_ARTA_SENTOSA           | Bank Multi Arta Sentosa
e40c197e-06dc-4a78-9d37-f6f06ea7a916 | NATIONALNOBU                 | Bank Nationalnobu
072c24a9-86b8-429a-868b-812df568b383 | NUSA_TENGGARA_BARAT          | BPD Nusa Tenggara Barat
9b800a68-48e6-4a2b-81c8-779ccd587786 | NUSA_TENGGARA_BARAT_UUS      | BPD Nusa Tenggara Barat UUS
89f5b93c-61c2-4b20-99ea-29eb730457d0 | NUSA_TENGGARA_TIMUR          | BPD Nusa Tenggara Timur
8adbcc79-be0d-463a-8c76-1c06f4a7c276 | NUSANTARA_PARAHYANGAN        | Bank Nusantara Parahyangan
db02929c-8b6c-4869-9bdf-b180c8b80519 | OCBC                         | Bank OCBC NISP
65554d34-c6c6-490c-bed0-4b952509c4de | OCBC_UUS                     | Bank OCBC NISP UUS
22f14a7f-9ad7-4662-9490-f24864f29331 | OKE                          | Bank Oke Indonesia (formerly Bank Andara)
8e9760bb-cd33-4c09-8022-4b167b692929 | OVO                          | OVO
63eb6757-8132-4857-a0b7-6408552a384d | PANIN                        | Bank Panin
a2849ab2-ae5b-429c-9953-1aed6672f88e | PANIN_SYR                    | Bank Panin Syariah
486b6b0a-bacf-4f51-be65-a71374a31c0b | PAPUA                        | BPD Papua
cf66bddf-e95a-429d-9e8c-fc2b22cd4e8e | PERMATA                      | Bank Permata
bf036c1f-cd91-4469-8cb2-d5eccbc26841 | PERMATA_UUS                  | Bank Permata UUS
b27d52f6-5ccc-4faf-bcd7-e94b584bc6ab | PRIMA_MASTER                 | Prima Master Bank
2d8f8438-5330-4744-ba95-eb84b81ffdc6 | QNB_INDONESIA                | Bank QNB Indonesia (formerly Bank QNB Kesawan)
b06ccdc7-cdd7-4e1f-8af4-d73bb63f240b | RABOBANK                     | Bank Rabobank International Indonesia
97273366-2680-4490-962f-a488aa3a5270 | RBS                          | Royal Bank of Scotland (RBS)
44428fad-f06e-48c5-bae4-a5a35a8cca62 | RESONA                       | Bank Resona Perdania
2334a8e4-ed4a-4dd1-af84-dc32e41587c6 | RIAU_DAN_KEPRI_UUS           | BPD Riau Dan Kepri UUS
c258ff97-cc58-45e4-b279-b76ea5538389 | SAHABAT_SAMPOERNA            | Bank Sahabat Sampoerna
580dffdb-a48a-4818-bcd4-1fbe9541a5f7 | SBI_INDONESIA                | Bank SBI Indonesia
a9873043-790a-46bb-834d-88a9883b744d | SHINHAN                      | Bank Shinhan Indonesia (formerly Bank Metro Express)
24edb279-6c03-4bfa-a473-3f21b0df90f0 | SINARMAS                     | Sinarmas
c37bac90-7359-48eb-8bfa-ead08fb2fe65 | STANDARD_CHARTERED           | Standard Chartered Bank
23124c7d-8db6-4188-b054-2e4467bb8a61 | SULAWESI                     | BPD Sulawesi Tengah
116f1eea-866c-4f97-8fe5-10712b68a9fd | SULAWESI_TENGGARA            | BPD Sulawesi Tenggara
22bdacdc-b5a1-40a7-9d7f-b9df5bbcf1e3 | SULSELBAR                    | BPD Sulselbar
28e4d780-c558-4fcc-b9ae-89ab39203d34 | SULSELBAR_UUS                | BPD Sulselbar UUS
18ed5d88-f209-4846-a8f7-e42b722cd6a1 | SULUT                        | BPD Sulut
0fd53a54-0978-421c-85b4-f50d000611a4 | SUMATERA_BARAT               | BPD Sumatera Barat
2b65358c-c2de-457c-89ea-21c02a05054a | SUMATERA_BARAT_UUS           | BPD Sumatera Barat UUS
80cfe001-2953-4ced-bd80-a4400462442b | SUMSEL_DAN_BABEL             | BPD Sumsel Dan Babel
cc5b8df1-87f5-4d39-af98-9edccc982191 | SUMSEL_DAN_BABEL_UUS         | BPD Sumsel Dan Babel UUS
f4a98ac2-edf9-45cc-8edf-31bce2b80325 | SUMUT_UUS                    | BPD Sumut UUS
6a118182-2586-4381-b9f6-9e115b1b96c4 | TOKYO                        | Bank of Tokyo Mitsubishi UFJ
101df8a8-c12b-437e-834a-ead18f3bcafb | UOB                          | Bank UOB Indonesia
d97e5e39-c4de-4562-a000-6e56229ee7b4 | VICTORIA_INTERNASIONAL       | Bank Victoria Internasional
faf5a7a9-6ade-4ec7-9e76-ab6489bff1a1 | VICTORIA_SYR                 | Bank Victoria Syariah
1cbd6abe-e4b2-46c0-801e-1302a90e3133 | WOORI                        | Bank Woori Saudara Indonesia (formerly Bank Himpunan Saudara and Bank Woori Indonesia)
63d88c05-3141-46dd-81f3-572a00f18ff2 | YUDHA_BHAKTI                 | Bank Yudha Bhakti

## Purpose Codes

Key | Description
--------- | -----------
SELF | Transfer to own account
FAMILY | Family Maintenance
EDUCATION | Education-related student expenses
MEDICAL | Medical Treatment
HOTEL | Hotel Accomodation
TRAVEL | Travel
UTILITIES | Utility Bills
LOAN_REPAYMENT | Repayment of Loans
TAX_PAYMENT | Tax Payment
RESIDENCE_PURCHASE | Purchase of Residential Property
RESIDENCE_RENT | Payment of Property Rental
INSURANCE | Insurance
MUTUAL_FUND | Mutual Fund Investment
SHARES_INVESTMENT | Investment in Shares
DONATIONS | Donations
ADVERTISING | Advertising & Public relations-related expenses
ROYALTY_FEES | Royalty fees, trademark fees, patent fees, and copyright fees
BROKER_FEES | Fees for brokers, front end fee, commitment fee, guarantee fee and custodian fee
ADVISORS | Fees for advisors, technical assistance, and academic purpose, including remuneration for specialists
OFFICE | Representative office expenses
CONSTRUCTION | Construction costs / expenses
SHIPMENT | Transportation fees for goods
EXPORT | For payment of exported goods
DELIVERY | Delivery fees for goods
TRADES | General Goods Trades - Offline trade
SALARY | Salary
REFUND | Refund
LOAN | Loan

## Source of Funds

Key | Description
--------- | -----------
INVESTMENT | Bonds, fixed deposits, preference shares, business ownership/equity or property ownership
PERSONAL_SAVINGS | Funds kept in an account in a bank or a similar organization
BUSINESS_REVENUE | Income from a business or a company
LEGACY | Inherited money from a will
BUSINESS_ARRANGEMENT | Any understanding, procedure, course of dealing, or arrangement between a creditor and a seller
LOAN | A sum of money that is borrowed
SALARY | A fixed regular payment made by an employer
OTHER | Other
