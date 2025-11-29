Admin:
docker run -p 8020:8020 -p 8021:8021 \
--network von_von \
ghcr.io/openwallet-foundation/acapy-agent:py3.12-1.2-lts \
start \
--inbound-transport http 0.0.0.0 8020 \
--outbound-transport http \
--endpoint http://host.docker.internal:8020 \
--genesis-url http://host.docker.internal:9000/genesis \
--admin 0.0.0.0 8021 \
--admin-api-key MySecretAdminKey \
--webhook-url http://host.docker.internal:8080/webhooks \
--auto-provision \
--wallet-type askar \
--wallet-name UniversityWallet \
--wallet-key MySecretWalletKey

Student:
docker run -p 8030:8030 -p 8031:8031 \
--network von_von \
--add-host=host.docker.internal:host-gateway \
ghcr.io/openwallet-foundation/acapy-agent:py3.12-1.2-lts \
start \
--inbound-transport http 0.0.0.0 8030 \
--outbound-transport http \
--endpoint http://host.docker.internal:8030 \
--genesis-url http://host.docker.internal:9000/genesis \
--admin 0.0.0.0 8031 \
--admin-api-key MyStudentsSecretKey \
--webhook-url http://host.docker.internal:8081/webhooks \
--auto-provision \
--auto-accept-invites \
--auto-accept-requests \
--auto-respond-credential-offer \
--auto-store-credential \
--label "Student Wallet" \
--wallet-type askar \
--wallet-name StudentWallet \
--wallet-key MyStudentWalletKey

Organisation:
docker run -p 8040:8040 -p 8041:8041 \
--network von_von \
--add-host=host.docker.internal:host-gateway \
ghcr.io/openwallet-foundation/acapy-agent:py3.12-1.2-lts \
start \
--inbound-transport http 0.0.0.0 8040 \
--outbound-transport http \
--endpoint http://host.docker.internal:8040 \
--genesis-url http://host.docker.internal:9000/genesis \
--admin 0.0.0.0 8041 \
--admin-api-key MyVerifiersSecretKey \
--webhook-url http://host.docker.internal:8082/webhooks \
--auto-provision \
--auto-accept-invites \
--auto-accept-requests \
--label "Verifier (Employer)" \
--wallet-type askar \
--wallet-name VerifierWallet \
--wallet-key MyVerifierWalletKey \
--auto-verify-presentation \
--preserve-exchange-records
