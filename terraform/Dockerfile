# --- Base image: Debian stable ---
FROM debian:bullseye-slim

# --- Install dependencies ---
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        bash \
        curl \
        git \
        jq \
        python3 \
        python3-pip \
        unzip \
        ca-certificates \
        gnupg \
        lsb-release \
        openjdk-17-jdk && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# --- Install Terraform ---
RUN curl -fsSL https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" > /etc/apt/sources.list.d/hashicorp.list && \
    apt-get update && \
    apt-get install -y terraform && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# --- Install Terragrunt ---
RUN curl -L https://github.com/gruntwork-io/terragrunt/releases/download/v0.56.1/terragrunt_linux_amd64 \
    -o /usr/local/bin/terragrunt && \
    chmod +x /usr/local/bin/terragrunt

# --- Install Google Cloud SDK ---
RUN curl -sSL https://sdk.cloud.google.com | bash -s -- --disable-prompts && \
    mv /root/google-cloud-sdk /usr/local/google-cloud-sdk
ENV PATH="/usr/local/google-cloud-sdk/bin:${PATH}"

# --- Set Java env explicitly ---
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH="${JAVA_HOME}/bin:${PATH}"

# --- Working directory ---
WORKDIR /infra

ENTRYPOINT [ "bash" ]
