FROM alpine:latest AS build

# https://github.com/awslabs/amazon-ecr-credential-helper#installing
RUN apk add --no-cache libc6-compat gcc g++ git go \
	&& go get -u github.com/awslabs/amazon-ecr-credential-helper/ecr-login/cli/docker-credential-ecr-login

# Final image has to be alpine, scratch doesn't support our env vars or credentials file
FROM alpine:latest
COPY --from=v2tec/watchtower:0.3.0 / /
COPY --from=build /root/go/bin/docker-credential-ecr-login /bin/docker-credential-ecr-login

ENTRYPOINT ["/watchtower"]