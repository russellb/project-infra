.phony: update-config update-plugins validate

update-config:
	kubectl create configmap config --from-file=config.yaml=config/config.yaml --dry-run -o yaml | kubectl replace configmap config -f -

update-plugins:
	kubectl create configmap plugins --from-file=plugins.yaml=config/plugins.yaml --dry-run -o yaml | kubectl replace configmap plugins -f -

validate:
	eval "$(go env)"
	CURDIR="$(pwd)" && cd "${GOPATH}/src/k8s.io/test-infra/prow" && bazel run //prow/cmd/checkconfig -- --plugin-config="${CURDIR}/config/plugins.yaml" --config-path="${CURDIR}/config/config.yaml"
