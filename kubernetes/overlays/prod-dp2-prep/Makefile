SECRET_PATH ?= secret/rubin/usdf-ingestd
ENV = $(notdir ${CURDIR})

get-secrets-from-vault:
	mkdir -p etc/.secrets/
	set -e; for i in user password; do vault kv get --field=$$i ${SECRET_PATH}/${ENV}/postgres > etc/.secrets/$$i ; done

clean-secrets:
	rm -rf etc/.secrets/

run-dump:
	kubectl kustomize .

dump: get-secrets-from-vault run-dump clean-secrets

run-apply:
	kubectl apply -k .

apply: get-secrets-from-vault run-apply clean-secrets


