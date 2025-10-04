FROM hashicorp/terraform:latest

# Install dependencies
RUN apk add --no-cache bash curl git jq python3 py3-pip

# Install Terragrunt
RUN curl -L https://github.com/gruntwork-io/terragrunt/releases/download/v0.56.1/terragrunt_linux_amd64 \
    -o /usr/local/bin/terragrunt \
    && chmod +x /usr/local/bin/terragrunt

# Install gcloud SDK (for remote state later)
RUN curl -sSL https://sdk.cloud.google.com | bash -s -- --disable-prompts \
    && mv /root/google-cloud-sdk /usr/local/google-cloud-sdk
ENV PATH="/usr/local/google-cloud-sdk/bin:${PATH}"

WORKDIR /infra
ENTRYPOINT [ "bash" ]
