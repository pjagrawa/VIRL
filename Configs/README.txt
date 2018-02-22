
QUICK INSTALL NOTES
VIRL LAB
CA SERVER: XCA on Linux


==================================================================
PUT DAY0 INITIAL CONFIGS ON vEdge VNFs
==================================================================

-> Copy/paste configurations.



==================================================================
INSTALL ROOT CERTIFICATE
==================================================================

CA SERVER - Upload Root CA on controllers
-----------------------------------------

scp root-ca-chain.crt admin@10.60.19.42:
scp root-ca-chain.crt admin@10.60.19.45:
scp root-ca-chain.crt admin@10.60.19.43:
scp root-ca-chain.crt admin@10.60.19.80:


CA SERVER - Upload Root CA on vEdges
------------------------------------

scp root-ca-chain.crt admin@100.64.11.1:
scp root-ca-chain.crt admin@100.64.12.1:
scp root-ca-chain.crt admin@100.64.21.1:
scp root-ca-chain.crt admin@100.64.22.1:
scp root-ca-chain.crt admin@100.64.31.1:
scp root-ca-chain.crt admin@100.64.41.1:
scp root-ca-chain.crt admin@100.65.51.1:
scp root-ca-chain.crt admin@100.64.52.1:


CONTROLLERS AND VEDGES - Install Root CA
----------------------------------------

request root-cert-chain install /home/admin/root-ca-chain.crt



==================================================================
INSTALL CERTIFICATES ON CONTROLLERS
==================================================================

CONTROLLERS - Generate CSR
--------------------------

request csr upload scp://admin@10.60.19.12:certs/vmanage1.csr
request csr upload scp://admin@10.60.19.12:certs/vbond100.csr
request csr upload scp://admin@10.60.19.12:certs/vsmart100.csr
request csr upload scp://admin@10.60.19.12:certs/vsmart101.csr


CA SERVER - Sign and Upload certificates
----------------------------------------

-> Sign certificate on XCA using Root CA certificate.

scp vmanage2.crt admin@10.60.19.42:/home/admin/
scp vbond100.crt admin@10.60.19.45:/home/admin/
scp vsmart100.crt admin@10.60.19.43:/home/admin/
scp vsmart101.crt admin@10.60.19.80:/home/admin/


CONTROLLERS - Install Certificates
----------------------------------

request certificate install /home/admin/vmanage1.crt
request certificate install /home/admin/vbond100.crt
request certificate install /home/admin/vsmart100.crt
request certificate install /home/admin/vsmart101.crt



==================================================================
INSTALL CERTIFICATES ON VEDGES
==================================================================

-> Generate bootstrap configuration with vManage


VEDGES - Activate
-----------------

request vedge activate chassis-number <UUID> token <OTP>





